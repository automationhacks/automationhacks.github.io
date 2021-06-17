---
title: How to do logging integration with logback and testng in report portal
excerpt: "How to push logs into report portal using logback in a Kotlin/TestNG/Gradle project"

permalink: /2020/09/25/logging-integration-with-logback-testng-in-report-portal/
image: /assets/images/2020/09/rp_logback_images.png
categories:
  - "Test automation"
  - Testing
tags:
  - Reporting
---

Hi there,

This post talks about how to show up certain attributes on 

Two ways

- At launch level, add below to `reportportal.properties`

```text
#rp.attributes="helloAttributes,lola"
```

Or

- Add below attributes to your tests, this would add the tag at an individual test level, can be only done at a method level
  - Read more in [client-java wiki](https://github.com/reportportal/client-java/wiki/Test-item-attributes)


```kotlin
@Test(dataProvider = "numbers", groups = [TestGroups.SHOULD_PASS])
@Attributes(attributes= [Attribute(key="additional", value = "should_pass")])
fun testAddition(first: Int, second: Int, expected: Int) {
    Assert.assertTrue(first + second == expected)
}
```


```groovy
systemProperty "rp.attributes", System.getProperty("tag")
```

https://stackoverflow.com/questions/23689054/problems-passing-system-properties-and-parameters-when-running-java-class-via-gr
https://docs.gradle.org/current/dsl/org.gradle.api.tasks.JavaExec.html