---
title: "How to setup report portal dashboards using attributes for test observability"
excerpt: "This blog will give a technical walkthrough on how to create rich and interactive report portal dashboards such that data can be grouped by different dimensions using attributes"
permalink: 2024-11-22-how-to-setup-report-portal-dashboards-using-attributes
published: true
image: /assets/images/2024/11/report-portal-chart.png
canonical_url: "https://newsletter.automationhacks.io/p/inside-test-observability-how-to-setup-report-portal-dashboards-using-attributes"
categories:
  - "Test observability"
tags:
  - "ReportPortal"
---

<figure class="image">
    <img src="assets/images/2024/11/report-portal-chart.png" alt="A man applying a chart with some label having black and purple data bars">
    <figcaption>Created by microsoft copilot using DALL.E 3</figcaption>
</figure>

## What is a report portal?

Successful QA engineering teams use data and test observability (o11y) to their advantage to identify areas or tests that need attention and have scope for optimization and drive corrective measures

Suppose you don’t have a good way to measure and visualize how reliable your test suites are.

It is easy to be overwhelmed by your suite's many broken or flaky tests.

Engineers often struggle with:

1. Resorting to ad-hoc local spreadsheets to track bugs for a failing test
2. Maintain a record of which cases are broken/flaky

[ReportPortal](https://reportportal.io/) is a free and open-source solution that elegantly solves this exact problem.

I’ve personally evangelized it at scale-ups like Gojek and CRED, and have been impressed by its power and flexibility with engineering teams deriving a ton of value.

Quite often, engineering teams spend a lot of time setting up Extent reports, and Allure reports stored in S3 or GCP buckets which while good for static and presentable reports lack a lot of modern real-time analysis features that the report portal provides out-of-the-box

There is a better way; why not try it? 🤷

## ⚙️ Setup

### Install report portal

I had previously written a few blogs on how to set ReportPortal on a single machine using docker and set logging integration using log back for a Java-based project or with Pytest for a Python-based project

You can read them below:

1. [How to set ReportPortal on a local docker instance - automation hacks](https://automationhacks.io/2020/03/02/how-to-setup-reportportal-on-a-local-docker-instance/)
2. [How to do logging integration with logback and testng in ReportPortal - automation hacks](https://automationhacks.io/2020/09/25/logging-integration-with-logback-testng-in-report-portal/)
3. [Python API test automation framework (Part 8) Adding reporting with ReportPortal](https://automationhacks.io/2021/02/03/python-api-automation-framework-part8-adding-reporting-with-report-portal)

Here, I’ll just recap the main steps quickly so that this blog is a good starting point and self-enclosed, but will encourage you to read [Deploy with Docker](https://reportportal.io/docs/installation-steps/DeployWithDocker) for more complete intuition.

You can skip point 2 since we have a usable docker-compose.yml file already in the Git repo that we’ll work with for this tutorial

- Install Docker Desktop on your operating system (OS) from the Docker website. Instructions for Mac can be found on [Install Docker Desktop on Mac](https://docs.docker.com/desktop/setup/install/mac-install/)
- Download the latest `docker-compose.yml` file

```zsh
curl -LO https://raw.githubusercontent.com/reportportal/reportportal/master/docker-compose.yml
```

Bring up docker containers by running:

```zsh
docker-compose -p reportportal up -d --force-recreate
```

Create a directory for OpenSearch and give permissions

```zsh
mkdir -p data/opensearch
chmod 775 data/opensearch
chgrp 1000 data/opensearch
```

Verify ReportPortal containers are up by running below and checking that all containers are in a healthy state

```zsh
docker ps -a
```

Next access ReportPortal using [http://localhost:8080](http://localhost:8080) and use the default username and password `superadmin\erebus` to login

![Report portal login screen](/assets/images/2024/11/1-report-portal-login-screen.png)

In the bottom left, click on the Superman logo and then on Administrate

![Administrate](/assets/images/2024/11/2-admin-section.png)

This will take you to All Projects, click on **Add New Project** and type the project name as **test-infra**

![Add new project](/assets/images/2024/11/3-all-projects.png)

![Add project name](/assets/images/2024/11/4-create-new-project.png)

Next in the bottom left, again click on the Superman logo and then on Profile

![Click on profile](/assets/images/2024/11/5-admin-section.png)

This will take you to the User profile section, click on API keys and then on Generate API Key

![Generate API key](/assets/images/2024/11/6-api-keys.png)

Enter a key name like **test-infra**and then make a copy of the generated key. Please note: This key will not be accessible after this screen so it's important to **note it down** somewhere safe

![Type API key unique name](assets/images/2024/11/7-generate-new-key.png)

### Clone git repo

We’ll use [https://github.com/automationhacks/test-infra](https://github.com/automationhacks/test-infra) repo on my Github account.

You can clone the repo using either HTTPS/SSH or Github CLI and then open the build.gradle file using IntelliJ IDEA

You’ll notice this project already has a docker-compose.yml file in the root directory, if you want to use the same for your setup, you could run the command to set up docker containers.

```zsh
docker-compose -p reportportal up -d --force-recreate
```

Once Gradle downloads all the dependencies

Search for `reportportal.properties`

and replace the `rp.api.key=<your_api_value>` copied in step 10 of previous section

Required gradle dependencies are already set up in the build.gradle

```groovy
testImplementation 'org.testng:testng:7.10.2'
testImplementation 'com.epam.reportportal:agent-java-testng:5.4.2'
testImplementation 'com.epam.reportportal:logger-java-logback:5.2.2'
```

And logback.xml with configuration for logging is present in src/test/resources/logback.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
   <appender name="ReportPortalAppender" class="com.epam.reportportal.logback.appender.ReportPortalAppender">
       <encoder>
           <pattern>%d{HH:mm:ss.SSS} [%t] %-5level - %msg%n</pattern>
       </encoder>
   </appender>

   <appender name="ASYNC_RP" class="ch.qos.logback.classic.AsyncAppender">
       <appender-ref ref="ReportPortalAppender"/>
       <!-- Sets the maximum number of log events in the queue -->
       <queueSize>512</queueSize>
       <discardingThreshold>0</discardingThreshold>
       <!--  Set to true to include information about the caller of the logging method. -->
       <includeCallerData>true</includeCallerData>
   </appender>

   <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
       <encoder>
           <pattern>%d{HH:mm:ss.SSS} [%t] %-5level - %msg%n</pattern>
       </encoder>
   </appender>

   <root level="INFO">
       <appender-ref ref="CONSOLE"/>
       <appender-ref ref="ASYNC_RP"/>
   </root>
</configuration>
```

The gradle test job looks like below which registers the report portal listener

```groovy
test {
   useTestNG() {
       useDefaultListeners = true
       listeners << 'io.automationhacks.testinfra.alerting.TestListener'
       listeners << 'com.epam.reportportal.testng.ReportPortalTestNGListener'
       parallel = 'methods'
       threadCount = 6


       includeGroups System.getProperty('includedGroups', '')
       excludeGroups System.getProperty('excludedGroups', '')
   }


   // pass system properties from commandline
   systemProperties = System.properties


   // show stdout and stderr of test JVM on console
   testLogging.showStandardStreams = true


   finalizedBy jacocoTestReport
}
```

You can recap the blogs mentioned at the top for more details on these setups however this is sufficient to get started with pumping data into ReportPortal

## Let’s run some tests

If you navigate to `src/test/java/io/automationhacks/testinfra/reqres` package

You’ll see that I’ve written some rest-assured tests to test the R[eqRes API](https://reqres.in/), in general, either get/put/post/delete certain resources and assert their outcomes.

We can run the test to push the results in the report portal and see how the launches look like by running the below commands

These are also mentioned in the README.md

```zsh
./gradlew test -DincludedGroups=identity -Drp.launch=identity_tests

./gradlew test -DincludedGroups=onboarding -Drp.launch=onboarding_tests

./gradlew test -DincludedGroups=performance -Drp.launch=performance_tests
```

Notice here I’m filtering tests that are tagged with a certain TestNG group like identity, onboarding, and performance using `-DincludedGroups`, and also using the `-Drp.launch` param to give the launch (or test run) a meaningful name

![Launches](/assets/images/2024/11/8-launches.png)

## Attributes as metadata

ReportPortal supports adding additional metadata as key-value pairs either via the command line or as test annotations

### At launch

If you open Launches, you’ll see the 3 launches show up for identity_tests, onboarding_tests, and performance_tests and they also have some default attributes or tags like those below which are specified in `reportportal.properties` for `rp.attributes`

```zsh
group:test_infra;test_type:backend
```

These attributes and tags are very useful to filter launches and create informative dashboards

In a real project, you may want to add even more attributes to a given test suite

You can override `rp.attributes` while running the tests via the Gradle command by appending the below

```zsh
-Drp.attributes="group:test_infra;test_type:backend;team:identity"
```

Each key: value pair is separated by a colon and delimited by a semi-colon

Here we have added another attribute called team so that we can derive some team-level metrics using this

Our test commands look like the below now

```zsh
./gradlew test -DincludedGroups=identity -Drp.launch=identity_tests -Drp.attributes="group:test_infra;test_type:backend;team:identity" --info

./gradlew test -DincludedGroups=onboarding -Drp.launch=onboarding_tests -Drp.attributes="group:test_infra;test_type:backend;team:onboarding" --info

./gradlew test -DincludedGroups=performance -Drp.launch=performance_tests -Drp.attributes="group:test_infra;test_type:backend;team:performance" --info
```

You can observe that now we have another attribute at the Launch level to filter results by.

![Attributes on launches](/assets/images/2024/11/9-after-launch-attributes.png)

### At test

We can also add these attributes at a test level

Say, you want to store who is the on-call or maintainer of a given test so that seeing a failing test indicates the current owner for context

We can annotate the test with below

```java
@Attributes(attributes = {@Attribute(key = "team", value = "identity")})
```

The complete test looks like below:

```java
public class ReqResCreateUserTest {

   @BeforeClass(alwaysRun = true)
   public void setup() {
       RestAssured.baseURI = "https://reqres.in/api";
   }

   @Test(groups = {Team.IDENTITY, Groups.SMOKE})
   @Attributes(attributes = {@Attribute(key = "team", value = "identity")})
   public void testCreate() {
       String requestBody = "{\"name\": \"morpheus\", \"job\": \"leader\"}";

       given().contentType(ContentType.JSON)
               .body(requestBody)
               .when()
               .post("/users")
               .then()
               // TODO: Broken test example, change to 201 to fix
               .statusCode(200)
               .body("name", equalTo("morpheus"))
               .body("job", equalTo("leader"))
               .body("id", notNullValue())
               .body("createdAt", notNullValue());
   }
}
```

Now if we look at the test in launches, you’ll notice the attribute is also stored at a test level.

![Attribute at test level](/assets/images/2024/11/10-test-level-attribute.png)

It is possible to add multiple attributes at a test level or have multiple keys with the same value or one key with multiple values. You can read the details in [test item attributes wiki from ReportPortal](https://github.com/reportportal/client-java/wiki/Test-item-attributes)

Below are quick snippets taken fromthe above wiki for reference

Many keys to one value

```java
@Test
@Attributes(multiKeyAttributes = { @MultiKeyAttribute(keys = { "k1", "k2" }, value = "v") })
public void third() {
 Assert.assertEquals(1, 1);
}
```

One key to many values

```java
@Test
@Attributes(multiValueAttributes = { @MultiValueAttribute(key = "k", values = { "v1", "v2" }) })
public void fourth() {
 Assert.assertEquals(1, 1);
}
```

Multiple attributes

```java
@Test
@Attributes(attributes = {@Attribute(key = "key1", value = "value1"), @Attribute(key = "key2", value = "value2")})
public void sixth() {
 Assert.assertEquals(1, 1);
}
```

## Dashboards

Let’s unpack the power of visualization using dashboards

There are a couple of distinct personas report portal supports

### 🤹 As a leader

I may want to see broad metrics for the 3 teams that I’m leading and identify hotspots that need attention.

A few widgets make a lot of sense such as:

1. **Component health check (table):** See component level health by splitting them using attribute **team** and observe overall pass/failed metrics in a tabular format
2. **Component health check:** See the split of the last test suite at a team level into visual cards with the option to open actually failed tests
3. **Launch statistics chart - bar view:** Bar chart with a summary of how many cases passed/failed/skipped
4. **Overall statistics - donut view for latest launches:** Donut chart with a summary of failed/passed cases and how many cases are left to investigate

![Report portal dashboards](/assets/images/2024/11/11-pass-broken-metrics.png)

You can also see additional charts like

1. **Test-cases growth trend chart:** to see how many tests were added or removed from the suites over time
2. **Failed cases trend chart:** to analyze the status of your broken tests

![Test growth and broken tests](/assets/images/2024/11/12-growth-broken-test-trend.png)

How can you configure these?

The magic lies in **creating filters** with a combination of certain attributes and then using them to create the visualization you desire.

I promise it's pretty intuitive once you play with it.

For instance, below is how you can set up the component health check table

1. Select a **filter** that filters all launches having **group equal to test_infra**
2. Select the **latest launches** to see the last launch
3. Select **team attribute** as a way to split the data

![Edit component health widget](/assets/images/2024/11/13-component-health-configuration.png)

And say you want to configure the Overall statistics widget

1. Select **filter** as **“group as test_infra”**
2. Select **Donut view**
3. Select **Latest launches**

And you are done.

![Overall statistics widget configuration](/assets/images/2024/11/14-overall-statistics-configuration.png)

You can also edit the filter by adding more conditions, like below

![Edit filters](/assets/images/2024/11/15-edit-filters.png)

### 🧑🏻‍💻 As an engineer

The previous visualizations are great for getting a bird's eye view of how a given group with multiple teams or a product is doing.

Often you as an engineer would rather focus more on how are your tests behaving and may have a team-specific or flow-specific dashboard.

There are a few more dashboards that are more useful for analysis.

These are focussed mostly at a launch (or one test suite level) and can be used as lower-level dashboards to drive analysis and fixes in a focussed area.

1. **Component health check:** sliced for services to find the health of fine-grained services
2. **Passing rate per launch:** to find the overall status for the last launch
3. **Flaky test cases table (top 50):** identity the top flaky cases to look at
4. **Most failed test cases table (top 50):** identify all the broken tests

![Services broken and flaky](/assets/images/2024/11/16-services-flaky-broken.png)

- **Launches duration chart:** to see which launches take how much time in order to find slow-running suites
- **Most time-consuming test cases widget (top 20):** to find slow-running tests to be optimised

![Test duration](/assets/images/2024/11/17-test-duration.png)

## Recap

To summarize

1. Report portal is an excellent test observability solution adhering to true FOSS (free and open source software) spirit that can be installed over Docker containers on your private network
2. Setup is quick and frictionless with running docker-compose, creating a project, getting the API key, and setting up logging integration
3. Launches provide you last test run status with support to analyse cases
4. Use attributes at the launch or test case level to add rich filtering capabilities
5. Create dashboards with either aggregated metrics or low-level analysis metrics suitable both for a leader or engineer persona

So what are you waiting for?

Go ahead and have a much better picture of your test suites and keep them in good health 🫶

Thanks for the time you spent reading this 🙌. If you found this post helpful, please subscribe to the substack [newsletter](https://newsletter.automationhacks.io/) and follow my YouTube channel (**@automationhacks**) for more such insights in Software **Testing** and **Automation**. Until next time 👋, Happy Testing 🕵🏻 and Learning! 🌱| [Newsletter](https://newsletter.automationhacks.io/) | [YouTube](https://www.youtube.com/@automationhacks) | [Blog](https://automationhacks.io/) | [LinkedIn](https://www.linkedin.com/in/automationhacks/) | [Twitter](https://twitter.com/automationhacks).
