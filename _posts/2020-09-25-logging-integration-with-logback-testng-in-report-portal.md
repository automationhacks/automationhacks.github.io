---
title: How to do logging integration with logback and testng in ReportPortal
excerpt: "How to push logs into ReportPortal using logback in a Kotlin/TestNG/Gradle project"
permalink: /2020/09/25/logging-integration-with-logback-testng-in-report-portal/
image: /assets/images/2020/09/rp_logback_images.png
categories:
  - "Software Testing"
  - "ReportPortal"
  - "Test observability"
tags:
  - "Reporting"
  - "ReportPortal"
  - "Test observability"
---

![ReportPortal logback main image](/assets/images/2020/09/rp_logback_images.png)

Image Attribution: [ReportPortal logo](https://twitter.com/reportportal_io),
[logback logo](http://logback.qos.ch/),
[Gradle logo - wikipedia](https://en.wikipedia.org/wiki/Gradle#/media/File:Gradle_logo.png)

Hi there, friend 👋,

ReportPortal is a quite unique open-source reporting solution available and seamlessly integrates
with the test runner of youR choice

I've been using ReportPortal in my current company and have quite recently started looking into its
features in more detail.

If you new to ReportPortal and want to get started with setting up a basic instance on docker and
play around then you might find my earlier post on this topic useful

Check out: [How to setup ReportPortal on a local docker
instance]({% link _posts/2020-03-02-how-to-setup-reportportal-on-a-local-docker-instance.md %})

Once you have setup ReportPortal, and have started pushing some test runs into it, you would want
to get more detail about the test execution. While ReportPortal will display the stack trace for a
failed assertion, it won't really give you all the console logs of the sequence of action that
happened above

As a simple example, let's say an API request fails wit a 500 and you have written an assertion on
the response code, while ReportPortal will let you know about the mismatch, it won't give you the
API request ,etc even though that might have been printed into the console with a TestNG
`Reporter.log()` message

So how do we push logs into ReportPortal? Let's see how to set this up.

## Setup logging using logback

I write my tests in Kotlin and run them using Gradle/TestNG. However, the process should be very
similar if you are on the JVM stack (Java etc)

On a high level, we need to do 4 steps

1. Add desired logger dependency into gradle
2. Add listener in your tests job in gradle
3. Add `.xml` properties file with the ReportPortalAppender specified
4. Add the class level logger and then write some messages to it.

## Add Maven/Gradle dependencies

We will use [`logback`](https://github.com/reportportal/logger-java-logback) as the logger of choice
however there is support even for [`log4j`](https://github.com/reportportal/logger-java-log4j) if
you prefer that.

Add below dependencies in your `build.gradle` file

```groovy
compile group: 'com.epam.reportportal', name: 'agent-java-testng', version: '5.0.7'
compile group: 'com.epam.reportportal', name: 'logger-java-logback', version: '5.0.3'
compile group: 'ch.qos.logback', name: 'logback-core', version: '1.2.3'
compile group: 'org.slf4j', name: 'slf4j-api', version: '1.7.30'
testCompile group: 'ch.qos.logback', name: 'logback-classic', version: '1.2.3'
```

## Add ReportPortal listener to you tests job

While you must have added this (if you followed my last post), ensure that ReportPortal listener is
added in your `test` gradle job, Below is an example, where we have `runTests` gradle test task,
where we have added the listener classes path

```groovy
task runTests(type: Test) {
    useTestNG {
        testLogging.showSt)ndardStreams = true
        useDefaultListeners = false
        listeners << 'com.epam.reportportal.testng.ReportPortalTestNGListener'
        listeners << 'listeners.ExtentReporterNG'
        includeGroups System.getProperty('tag', 'NONE')
    }
}
```

## Add a logging configuration file

Logging frameworks would either come with a configuration XML file or a properties file to allow you
to configure them. Since we are using logback, we need to use add a `logback.xml` file anywhere on
our classpath

Logback basically has different destinations that it could write logs to called `appenders`

Here is how a sample configuration file would look like:

{% gist 183d95d202b0065e50ee8bf72ad382e9 %}

This has 3 appenders defined

- STDOUT which uses ConsoleAppender from logback to write any logs to the command line
- (Optional) FILE which uses RollingFileAppender from logback to write logs to a physical file and
  then rotates these in a daily basis so that every new day, you would get a new log file while also
  keeping a history of max 30 days
- ReportPortalAppender which pushes logs to the ReportPortal

To understand how logback works in detail, refer to this excellent guide on
[Baeldung](https://www.baeldung.com/logback)

## Add some loggers

The last piece of the puzzle is to add some loggers into your source code. Let's assume you want to
write some logs in a test class, here is a basic Class and function in Kotlin to demonstrate that

```kotlin
@Test(groups = [TestGroups.ALL])
class LogbackTests {
    private val logger: Logger = LoggerFactory.getLogger(this::class.java)

    // This test can be flaky and non deterministic
    // Done on purpose to see variation in ReportPortal history
    @Test
    fun simpleLoggingTest() {
        logger.info("Example log from ${this::class.java.simpleName}")
        val random = ThreadLocalRandom.current().nextInt(30000)
        val limit = 20000

        logMessage(random, limit)
        Assert.assertTrue(random > limit, "No was greater than $limit")
    }

    private fun logMessage(random: Int, limit: Int) {
        if (random > limit) {
            logger.info("$random is > $limit")
        } else {
            logger.info("$random is < $limit")
        }
    }
```

Basically we want to add `static final` logger as a class member

```kotlin
private val logger: Logger = LoggerFactory.getLogger(this::class.java)
```

And then use any of the available methods to log at different log levels

Below are the available log levels that you can use

```kotlin
@Test
fun differentLogLevelsTest() {
    logger.trace("OMG trace level detail")
    logger.debug("Minute level detail")
    logger.info("This is just an info")
    logger.warn("Something bad happened")
    logger.error("Something catastropic happened")
}
```

Once you run this test you would see logs show up in ReportPortal under the log message section,
you can also filter between the level of detail that you need for your logs using the slider control
given

![ReportPortal launches](/assets/images/2020/09/rp_results.png)
![ReportPortal logs](/assets/images/2020/09/rp_logs.png)

## Summary

In this post, we learned how can we enhance our reporting in ReportPortal by adding logback as a
logging framework of choice.

If you found this post useful, Do share it with a friend or colleague. Until next time. Happy
Testing/Coding ☮️

### References

Here are some further links that you can refer to:

- You can find the entire sample project on my Github under
  [grasp-reporting](https://github.com/automationhacks/grasp-reporting) repo
- [Details about how the listeners in ReportPortal (agent-java-testNG)](https://github.com/reportportal/agent-java-testNG)
- Read about Test framework integration on
  [ReportPortal docs](https://reportportal.io/docs/log-data-in-reportportal/test-framework-integration/)
