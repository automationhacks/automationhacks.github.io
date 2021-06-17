---
title: How to work with redis for test automation
excerpt: Redis is a powerful in-memory data store that could be used for a variety of test automation use cases. In this post, we setup a redis server on an ubuntu VM and see how we can use redis-cli and a simple Kotlin class to interact with our server.
permalink: /2020/05/30/how-to-work-with-redis-for-test-automation/
categories:
  - "Test automation"
---

![Redis - Wikipedia](https://upload.wikimedia.org/wikipedia/en/thumb/6/6b/Redis_Logo.svg/1200px-Redis_Logo.svg.png)


<a rel="noopener" href="https://redis.io/" target="_blank">Redis</a> is an in-memory data structure store which can be used as a database cache and supports different <a rel="noopener" href="https://redis.io/topics/data-types-intro" target="_blank">data types</a>, most notably a simple key, value pair (aka dict), lists, etc.

It could be used for any relevant purpose within your test automation framework, for instance, one of the use cases that I found helpful was that we could use it as a **cache of temporary auth information for test user accounts**, which could be retrieved by tests running in parallel and avoid calling the actual auth APIs every time, Thus cutting a bit of external dependencies and making your tests faster.

Redis provides a **server** and a **CLI&nbsp;**interface if you want to play with the data and a bunch of <a href="https://redis.io/clients" target="_blank" rel="noopener">client libraries</a> for different programming languages to use them in your solution

In this post, we would see how to set up redis on an existing Ubuntu VM and how to interact with it for a very simple use case via redis-cli and then see what a simple kotlin file could look like to have an abstraction over this.

## Installation and setup of redis server on an Ubuntu VM

### Pre-requisites:

  * Ensure you have ubuntu already setup on your machine or have a VM created.
  * SSH into the VM or open terminal app
  * Execute `sudo su`to elevate your permissions to root
  * Ensure you have the <a rel="noopener" href="https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/" target="_blank">GCC compiler</a> <span style="color:var(--color-text);">already installed, if not, follow the below steps to set it up.</span>

<pre class="wp-block-syntaxhighlighter-code">sudo apt update
sudo apt install build-essential
gcc --version</pre>

### Install Redis via sudo apt

<pre class="wp-block-syntaxhighlighter-code">sudo apt update
sudo apt install redis-server</pre>

### Expose the redis server to outside the VM

By default, redis would start running on `localhost (127.0.0.1)` , however, if you want to use it for your use cases, you would need to update the IP which it binds to in **redis.conf** file

Open the file in your comfortable editor of choice

<pre class="wp-block-syntaxhighlighter-code">sudo vim /etc/redis/redis.conf</pre>

Inside `redis.conf` file, update

<pre class="wp-block-syntaxhighlighter-code">bind 127.0.0.1</pre>

to

<pre class="wp-block-syntaxhighlighter-code">bind 0.0.0.0</pre>

### Restart redis service

<pre class="wp-block-syntaxhighlighter-code">sudo systemctl restart redis.service</pre>

Once done, check if the redis service is running

<pre class="wp-block-syntaxhighlighter-code">sudo systemctl status redis</pre>

You should see an output like below:

<pre class="wp-block-syntaxhighlighter-code">redis-server.service - Advanced key-value store
   Loaded: loaded (/lib/systemd/system/redis-server.service; enabled; vendor preset: enabled)
   Active: active (running) since ... ;machines_local_timezone...;; 4min 15s ago
......</pre>

<blockquote class="wp-block-quote">
  <p>
    Note: I have intentionally removed some part of this output as it held sensitive information, However, you should see details around your VM/machines hostname and CPU/memory stats for your current redis instance.
  </p>
</blockquote>

Cool, 🥳 with this we have already set up a **redis server&nbsp;**on Ubuntu.

## 🤾🏻‍♂️ Play with redis-cli

To open redis-cli just type below

<pre class="wp-block-syntaxhighlighter-code">redis-cli</pre>

We can create a dummy key and set its value via the `set` command and get its value.

<pre class="wp-block-syntaxhighlighter-code">127.0.0.1:6379&gt; set "test-key" "test-value"
OK
127.0.0.1:6379&gt; get "test-key"
"test-value"</pre>

And that’s it.

If you want to connect to this from your local machine or runner, enter below command (provided you have redis-cli already setup)

<pre class="wp-block-syntaxhighlighter-code">redis-cli -h host_name_or_ip -p 6379</pre>

## How do we interact with this in our automation code?

Redis supports multiple clients to interact with the redis server. In below example, we have chosen to use `<a href="https://redis.io/clients#java">Jedis</a>`, however based on your needs you could go with any other client as well.

Add below line in your `build.gradle` file

<pre class="wp-block-syntaxhighlighter-code">compile group: 'redis.clients', name: 'jedis', version: '2.9.0'</pre>

In below class, we create a class `RedisHandler` which accepts a host and port (where your redis server is running) and then has simple `get(key)` and `put(key, value)` methods to work with redis (quite similar to how we used the `cli` above)

{% gist 38a345e245585904f27b9d5f67377e5f %}

Simple Kotlin file with an abstraction over jedis (JVM support library for redis)


And that's a wrap 🥳. Hopefully you would find creative use cases to use redis augment your automated tests. If you found this useful, do share with a friend or colleague. Until next time. Happy testing and automating! 

## Related articles

<ul class="ak-ul">
  <li>
    <a href="https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-redis-on-ubuntu-18-04">How to install Redis on ubuntu</a>
  </li>
  <li>
    <a href="https://stackoverflow.com/questions/19091087/open-redis-port-for-remote-connections">How to open Redis port for remote connections</a>
  </li>
</ul>

Further read on Redis, its data types and cli utility:

<ul class="ak-ul">
  <li>
    <a href="https://redis.io/topics/quickstart">Redis quickstart</a>
  </li>
  <li>
    <a href="https://redis.io/topics/data-types-intro">Redis data types</a>
  </li>
  <li>
    <a href="https://redis.io/clients#java">Redis client libraries</a>
  </li>
</ul>