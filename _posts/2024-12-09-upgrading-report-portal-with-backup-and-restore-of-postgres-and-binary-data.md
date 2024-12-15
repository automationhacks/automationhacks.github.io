---
title: "Upgrading ReportPortal with backup/restore of Postgres and binary data"
excerpt: "In this blog, learn how to take Postgres db, binary data backup, make upgrades in docker-compose.yml file, and then restore the DB data and binary data safely without losing launches and dashboards"
permalink: 2024-12-09-upgrading-report-portal-with-backup-and-restore-of-postgres-and-binary-data
published: true
image: assets/images/2024/12/chris-yates-iqELIpzpARI-unsplash.jpg
canonical_url: "https://newsletter.automationhacks.io/p/upgrading-report-portal-with-backup-restore-of-postgres-and-binary-data"
categories:
  - Software Testing
  - QA
  - SDET
  - Test observability 
  - ReportPortal
tags:
  - "Software Testing"
  - "SDET"
  - "QA"
  - "Test observability"
  - "ReportPortal"
---

<figure class="image">
    <img src="assets/images/2024/12/chris-yates-iqELIpzpARI-unsplash.jpg" alt="A CD being inserted into the drive of a laptop">
    <figcaption>Nothing speaks backup louder than a CD 💿 | Photo by Chris Yates on Unsplash</figcaption>
</figure>

## Why?

Once you have a running instance of ReportPortal with one or more teams using it successfully, it becomes important to keep patching it with upgrades and ensuring you get the benefits of bug fixes and new features.

But, If not done carefully, you can risk losing data (launches, logs, and dashboards) and having to set up integration again.

Trust me, You would not want to be the one who loses data for the company, especially when people depend on previous analysis, widgets, and dashboards for their day-to-day operations. 🤦

In this blog, I’ll help provide clear steps to achieve the below workflow:

1. Take backup of Postgres db
2. Take backup of binary data from Minio
3. Make changes in `docker-compose.yml` files (e.g. opening up ports, and adding new components like OpenSearch)
4. Ensure existing containers are updated.
5. Restore data into Postgres and binary

This blog is inspired by the guides published by the ReportPortal team.

I intend to explain nuances for someone new to Docker, Postgres, and Minio. If you are curious you can use them as additional resources

1. [Backup & Restore Guide ReportPortal Documentation](https://reportportal.io/docs/installation-steps-advanced/BackupRestoreGuide) for steps on how to backup and restore binary data
2. Follow [Upgrading PostgreSQL for ReportPortal v24.2 and later](https://reportportal.io/docs/installation-steps-advanced/UpgradingPostgreSQLForReportPortalV24.2AndLater) for steps on how to backup and restore Postgres

Let’s go 🏃

## Backup postgres

ReportPortal keeps most of the data in a Postgres instance including launches, filters, widgets, and dashboards. To backup Postgres, we can execute the `[pg_dump](https://www.postgresql.org/docs/current/app-pgdump.html)` command inside the docker container. This generates an SQL file with all the information needed to restore data after the upgrade.

```zsh
DB_USER=rpuser
DB_NAME=reportportal
DB_PASSWORD=rppass
DB_CONTAINER=postgres

docker exec -e PGPASSWORD=$DB_PASSWORD $DB_CONTAINER pg_dump -U $DB_USER -d $DB_NAME > reportportal_docker_db_backup.sql
```

Explanation:

* We first export required parameters like `DB_USER, DB_PASSWORD, DB_NAME`, and `DB_CONTAINER` to ensure what can vary is captured upfront and we have an easy to read command. In this example, I’m using the default values that you can see from the `docker-compose.yml` file here. You may want to change these and maintain another `docker-compose.yml` file
* `docker exec -e PGPASSWORD=$DB_PASSWORD $DB_CONTAINER`: Executes a command inside the specified Docker container while setting the Postgres database password upfront as an environment variable (using `-e`)
* `pg_dump -U $DB_USER -d $DB_NAME`: This command initiates a PostgreSQL dump, specifying the username and database name.
* `> reportportal_db_backup.sql`: Redirects the output sql to a file named `reportportal_docker_db_backup.sql.`

⚡Tip: This command may take time if the database has lots of data. Please be patient as that completes. **Do not exit out early**as you may have incomplete backup. Once this is completed, it would be a good idea to make a copy of this file by executing something like this:

```zsh
cp reportportal_docker_db_backup.sql YYYY_MM_DD_reportportal_docker_db_backup.sql
```

This will help avoid surprises if you somehow corrupt or delete the primary backup.

## Backup binary data

Next, we take a backup of binary data. ReportPortal uses [minIO](https://min.io/) as the **object store** to store additional data similar to how a file system would.

```zsh
VOLUME_NAME=reportportal_storage

docker run --rm -v "$VOLUME_NAME":/data -v "$(pwd)":/backup busybox tar -zcvf /backup/reportportal_storage_backup.tar.gz /data
```

Explanation:

* `docker run`: This command runs a Docker container.
* `--rm`: This flag removes the container once it completes its execution. This is useful for temporary containers, such as when performing a one-off task like creating a backup.
* `-v "$VOLUME_NAME":/storage_backup`: [This option creates a volume mount](https://docs.docker.com/engine/storage/bind-mounts/) between the host machine and the container. It mounts the Docker volume named by the `VOLUME_NAME`variable to the path`/storage_backup` inside the container.
* `-v "$(pwd)":/backup`: This option mounts the current working directory (`$(pwd))` on the host machine to the path`/backup` inside the container. This is where the backup file will be stored.
* `busybox`: This specifies the Docker image to be used for the container. In this case, it uses the BusyBox image, which is a lightweight and minimalistic Linux distribution often used for simple tasks.
* `tar -zcvf /backup/reportportal_storage_backup.tar.gz /data`: This part of the command runs the tar command inside the container to create a compressed tar archive `(reportportal_storage_backup.tar.gz)`.

## Remove all containers

We will now use docker-compose to**bring down** all existing containers. If any container is already running when you try to upgrade it, you must stop and manually remove it (using `docker stop &lt;container_name> && docker rm &lt;container_name>`)

This can be a tedious process to do one by one, as there could be dependencies between containers. Docker Compose simplifies this process for us

```zsh
docker compose -p reportportal down
```

## Remove Postgres volume

This step is optional, you should run this only if you want a clean slate in your DB. This would remove existing Postgres volume.

```zsh
docker volume rm reportportal_postgres
```

## Make changes in your docker-compose.yml file

Now that everything has been torn down, you can change the `docker-compose.yml` file.

For example, below are a few use cases when this may be relevant

### Upgrade versions

You may want to pull a new version of ReportPortal

```zsh
curl -LO https://raw.githubusercontent.com/reportportal/reportportal/master/docker-compose.yml
```

### Expose Postgres db

You may want to expose Postgres running in the container to the host machine to allow engineers to connect to it and make use of stored data for their purposes

```zsh
## Uncomment to expose Database
ports:
   - "5432:5432"
```

Below is how the full snippet looks like:

```zsh
## PostgreSQL as the main database for ReportPortal
postgres:
 image: bitnami/postgresql:16.4.0-debian-12-r7
 container_name: *db_host
 logging:
   <<: *logging
 shm_size: '512m'
 environment:
   POSTGRES_USER: *db_user
   POSTGRES_PASSWORD: *db_password
   POSTGRES_DB: *db_name
   POSTGRESQL_CHECKPOINT_COMPLETION_TARGET: 0.9
   WORK_MEM: 96M
   WAL_WRITER_DELAY: 20ms
   SYNCHRONOUS_COMMIT: off
   WAL_BUFFERS: 32MB
   MIN_WAL_SIZE: 2GB
   MAX_WAL_SIZE: 4GB
 volumes:
   - postgres:/bitnami/postgresql
 ## Uncomment to expose Database
 ports:
   - "5432:5432"
 healthcheck:
   test: [ "CMD-SHELL", "pg_isready -d $$POSTGRES_DB -U $$POSTGRES_USER" ]
   interval: 10s
   timeout: 120s
   retries: 10
 networks:
   - reportportal
 restart: always
```

### Add OpenSearch dashboards

You may want to add the capability also to serve open search dashboards so that I can add custom **search/visualization** capabilities on top of what ReportPortal provides out of the box

```zsh
## OpenSearch for search and analytical capabilities
opensearch:
 image: opensearchproject/opensearch:2.16.0
 container_name: *opensearch_host
 logging:
   <<: *logging
 environment:
   discovery.type: single-node
   plugins.security.disabled: "true"
   bootstrap.memory_lock: "true"
   OPENSEARCH_JAVA_OPTS: -Xms512m -Xmx512m
   DISABLE_INSTALL_DEMO_CONFIG: "true"
 ulimits:
   memlock:
     soft: -1
     hard: -1
 ## Uncomment the following lines to expose OpenSearch on ports 9200 and 9600
 ports:
   - "9200:9200"  # OpenSearch HTTP API
   - "9600:9600"  # OpenSearch Performance Analyzer
 volumes:
   - opensearch:/usr/share/opensearch/data
 healthcheck:
   test: [ "CMD", "curl","-s" ,"-f", "http://0.0.0.0:9200/_cat/health" ]
 networks:
   - reportportal
 restart: always

opensearch-dashboards:
 image: opensearchproject/opensearch-dashboards:2.16.0
 container_name: opensearch-dashboards
 ports:
   - "5601:5601"  # Dashboard UI
 environment:
   OPENSEARCH_HOSTS: http://opensearch:9200
   DISABLE_SECURITY_DASHBOARDS_PLUGIN: "true"  # Add this line to disable security
   OPENSEARCH_ALLOW_INSECURE: "true"          # Add this line to allow insecure connections
 depends_on:
   - opensearch
 networks:
   - reportportal
 restart: always
```

## Start only postgres

After your changes are done, we’ll first only bring up the database

```zsh
docker compose -p reportportal up -d postgres
```

## Restore Postgres

Next, let’s restore the data. To restore the data we use `psql`

```zsh
DB_USER=rpuser
DB_PASSWORD=rppass
DB_NAME=reportportal
DB_CONTAINER=postgres

docker exec -i -e PGPASSWORD=$DB_PASSWORD $DB_CONTAINER psql -U $DB_USER -d $DB_NAME < reportportal_docker_db_backup.sql > upgrade_db.log 2>&1
```

Explanation

1. `docker exec` This runs a command inside a running Docker container.
    1. `-i`: Keeps the input stream open so the SQL script can be passed to the `psql` command.
    2. `-e PGPASSWORD=$DB_PASSWORD`: Sets the `PGPASSWORD` environment variable inside the container. PostgreSQL uses this variable for authentication, so you don’t need to type the password interactively.
    3. `$DB_CONTAINER`: Refers to the name of the container (`postgres`).
2. `psql` is the [PostgreSQL command-line tool](https://www.postgresql.org/docs/current/app-psql.html). It connects to the database and executes SQL commands.
    4. `-U $DB_USER`: Specifies the database username (rpuser).
    5. `-d $DB_NAME`: Specifies the database name to connect to (reportportal).
    6. `&lt; reportportal_docker_db_backup.sql`: Redirects the contents of the SQL backup file (`reportportal_docker_db_backup.sql`) as input to psql. This restores the database from the backup file.
3. Redirect Output with `> upgrade_db.log 2>&1`
    7. `>`: Redirects the standard output of the command (success messages, etc.) to a file called `upgrade_db.log`.
    8. `2>&1`: Redirects the standard error (error messages) to the same file (upgrade_db.log) as the standard output. This captures all logs (success and errors) into a single file.

To verify the data is indeed restored, we should check the contents of the `upgrade_db.log` file

Also, you can connect to the postgres db server

Connect to the docker container

```zsh
docker exec -it postgres bash
```

Open psql

```zsh
psql -U rpuser -d reportportal
```

When prompted for the password, enter the postgres password from the `docker-compose.yml` file or the new one if you have reset it

Check if the below tables have values:

```sql
SELECT * FROM test_item limit 20;

SELECT * FROM test_item_results limit 20;
```

## Start all other services

Next, we should bring up all the other containers

```zsh
docker compose -p reportportal up -d
```

## Restore binary data

Finally, let's restore binary data as well

```zsh
VOLUME_NAME=reportportal_storage

docker run --rm -v $VOLUME_NAME:/data -v $(pwd):/backup busybox tar -xzvf /backup/reportportal_storage_backup.tar.gz -C /
```

We follow a similar process as the above to restore the gzip tar backup that we had taken back into minIO

Explanation

1. `docker run`
    * This command runs a temporary container from a specified image (busybox).
2. `--rm`
    * Automatically removes the container after it finishes running. This prevents leftover containers from cluttering the system.
3. `-v $VOLUME_NAME:/data`
    * Mounts a Docker volume named `$VOLUME_NAME` to the `/data` directory inside the container.
    * This allows the container to interact with the Docker volume's data.
4. `-v $(pwd):/backup`
    * Mounts the current working directory (represented by `$(pwd)`) to the `/backup` directory inside the container.
    * This makes files in the current directory, like the backup file, accessible to the container.
5. `busybox`
    * Specifies the Docker image to use for the container.
    * busybox is a lightweight image commonly used for basic utilities like file operations.
6. `tar -xzvf /backup/reportportal_storage_backup.tar.gz`
    * tar is a command-line tool used to extract files from archives.
        * `-x`: Extracts the files.
        * `-z`: Handles .gz (gzip-compressed) files.
        * `-v`: Enables verbose mode, showing the files being extracted.
        * `-f`: Specifies the input file, in this case, `/backup/reportportal_storage_backup.tar.gz`.
7. `-C /`
    * Changes the target directory for extraction to `/` (the root directory inside the container).
    * Files from the archive are extracted to their corresponding locations in `/`.

And you are done! 🎉

Congratulation! You have successfully managed to take a backup, upgrade the instance, and restore it all back now.

To verify login to ReportPortal [http://localhost:8080/ui/](http://localhost:8080/ui/) and check your launches, filters and dashboards are all available

## Connect to Postgres from the host machine

To verify if we can connect to [Postgres](https://www.postgresql.org/download/macosx/) running inside the docker container, you will need postgres on your local machine, on mac you can use homebrew to install

```zsh
brew install postgresql@16

# Postgresql
export PATH="/opt/homebrew/opt/postgresql@16/bin:$PATH"
export LDFLAGS="-L/opt/homebrew/opt/postgresql@16/lib"
export CPPFLAGS="-I/opt/homebrew/opt/postgresql@16/include"
```

Then start the postgres service

```zsh
brew services start postgresql@16
```

You can connect to Postgres from any client (like [DBeaver](https://dbeaver.io/)) by using the below details

```zsh
jdbc:postgresql://192.168.29.131:5432/reportportal
User name: rpuser
Password: rppass
```

Or, from the host machine, you can also connect to the PostgreSQL instance using psql to ensure the port is accessible:

```zsh
psql -h localhost -p 5432 -U rpuser -d reportportal
```

## OpenSearch dashboards

To test access to OpenSearch, you can hit `http://localhost:9200`

This should print details about the OpenSearch cluster

```zsh
{
  "name": "0fdbaba7ac12",
  "cluster_name": "docker-cluster",
  "cluster_uuid": "R0DM_scOSRuB0kba7Q6rGw",
  "version": {
    "distribution": "opensearch",
    "number": "2.16.0",
    "build_type": "tar",
    "build_hash": "f84a26e76807ea67a69822c37b1a1d89e7177d9b",
    "build_date": "2024-08-06T20:32:34.547531562Z",
    "build_snapshot": false,
    "lucene_version": "9.11.1",
    "minimum_wire_compatibility_version": "7.10.0",
    "minimum_index_compatibility_version": "7.0.0"
  },
  "tagline": "The OpenSearch Project: https://opensearch.org/"
}
```

Finally, you can open OpenSearch Dashboards via `http://localhost:5601`

## Summary

Let’s conclude on the workflow we learned today

1. **Backup Postgres:** Use the pg_dump command inside the Docker container to create an SQL file of your database.
2. **Backup Binary Data:** Create a compressed tar archive of your Minio data using the Docker run command.
3. **Remove Existing Containers:** Use docker-compose down to stop and remove all running containers. (Optional: Remove Postgres volume for a clean database.)
4. **Modify docker-compose.yml:** Update versions, expose ports, or add new components like OpenSearch.
5. **Start Postgres:** Use docker-compose up to start the Postgres container.
6. **Restore Postgres Data:** Use the psql command to restore data from the backup SQL file.
7. **Start Remaining Services:** Bring up all other containers with docker-compose up.
8. **Restore Binary Data:** Extract the tar archive into the Minio volume using the Docker run command.
9. **Verify**: Check ReportPortal, Postgres, and OpenSearch to ensure data and functionality are restored.

Thanks for the time you spent reading this 🙌. If you found this post helpful, please subscribe to the [newsletter](https://newsletter.automationhacks.io/) and follow my YouTube channel (@automationhacks) for more insights into software testing and automation. Until next time 👋, Happy Testing 🕵🏻 and Learning! 🌱

[Substack](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [X](https://twitter.com/automationhacks) | [BlueSky](https://bsky.app/profile/automationhacks.bsky.social)
