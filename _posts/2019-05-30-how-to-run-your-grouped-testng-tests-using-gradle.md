---
id: 51
title: How to run your grouped testNG tests using Gradle
date: 2019-05-30T17:20:10+00:00
author: Gaurav
layout: post
guid: http://automationhacks.blog/2019/05/30/how-to-run-your-grouped-testng-tests-using-gradle/
permalink: /2019/05/30/how-to-run-your-grouped-testng-tests-using-gradle/
publicize_twitter_user:
  - __gaurav_singh
publicize_linkedin_url:
  - null
categories:
  - Kotlin
  - Programming
  - Test frameworks
  - Testng
---

Walking through how to group and run your testNG tests via gradle and to avoid common pitfalls.

Hello people,

When building a test framework, one of the most crucial decisions to make is the choice of the test
framework in your language ecosystem. For Instance in Kotlin/Java world we could choose JUnit,
TestNG, Cucumber or pure kotlin frameworks like
<a href="https://github.com/kotlintest/kotlintest" target="_blank">kotlintest</a>,
<a href="https://github.com/spekframework/spek" target="_blank">spek</a>. Each of these frameworks
offer some basic constructs to achieve similar results along with their own implementation
idiosyncrasies.

For my current organization i chose to work with TestNG as the framework since it is fairly mature
and many devs/testers who work with JVM languages are already well aware of its different features
hence resulting in lower learning curve.

Once you have wired up some tests and they work fine inside the IDE (IntelliJ in this case) the next
logical step is obviously to promote them into your CI env and run via gradle. While doing so i
faced a small hiccup and this blog is a way to educate others in order to step a little into how i
debugged and finally arrived at the solution.

### Grouping of&nbsp;tests:

Another often used feature of any test framework is their support for grouping similar tests
together and providing the ability to run this subset of tests at will.

Let’s take an example to understand this a bit better

Hypothetically lets say, we need to test a Person class having name and age properties such that we
expect the Person to have certain fixed name and age. Also we would want to run all the cases which
belong to **person_test** group.

PersonTest.kt

```kotlin
import org.testng.Assert
import org.testng.annotations.AfterMethod
import org.testng.annotations.BeforeMethod
import org.testng.annotations.Test

class PersonTest {
    private var name = "Rob"
    private var age = 23

    @BeforeMethod()
    fun before() {
        println("Performing setup...")
        name = "John"
        age = 25
    }

    @Test(groups = ["person_test"])
    fun personNameTest() {
        Assert.assertEquals("John", name)
    }

    @Test(groups = ["person_test"])
    fun personAgeTest() {
        Assert.assertEquals(25, age)
    }

    @AfterMethod()
    fun after() {
        println("Performing teardown...")
    }
}
```

In TestNG, we can pass a list of group names to the Test annotation to unique identify them under
this common term.

```kotlin
@Test(groups = ["person_test"])
```

Next step is to setup a simple **build.gradle** file which should be able to run these tests. We can
follow a structure like below. Note: This config sets up your IntelliJ project to work with Kotlin

```gradle
plugins {
    id 'org.jetbrains.kotlin.jvm' version '1.3.31'
}

group 'com.example.testnggradle'
version '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

tasks.withType(Test) {
    systemProperties = [
            tag: System.getProperty('tag', 'person_test')
    ]
}

task runTests(type: Test) {
    useTestNG() {
        testLogging.showStandardStreams = true
        includeGroups System.getProperty('tag', 'NONE')
    }
}

dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk8"
    compile group: 'org.testng', name: 'testng', version: '6.14.3'
}

compileKotlin {
    kotlinOptions.jvmTarget = "1.8"
}
compileTestKotlin {
    kotlinOptions.jvmTarget = "1.8"
}
```

Couple of things to note here are:

We would want to pass a command line flag while running the **runTests** gradle task as **-Dtag** to
be able to run the tests belonging to the group that we want.

We achieve this by adding below line in useTestNG() method inside our task:

```gradle
includeGroups System.getProperty('tag', 'NONE')
```

And we are setting this as defaulted to `person_test` in order to ensure that all our tests are run.
This could be set to a sensible default like `regression` in case that is what you use to tag all
your cases.

```kotlin
tasks.withType(Test) {
    systemProperties = [
            tag: System.getProperty('tag', 'person_test')
    ]
}
```

Lets try to run this via command line to perform the ultimate check that this would work fine when
we push this as a command line job on some CI.

```zsh
./gradlew clean runTests -Dtag=person_test
```

Wait a minute. Why did the below fail? If you go back and see PersonTest.kt, you can see the test
should pass since we are setting up the correct value for Person’s name and age in `@BeforeMethod`
annotation. So what went wrong here?

```text
> Task :runTests FAILED

Gradle suite > Gradle test > PersonTest.personAgeTest FAILED
    java.lang.AssertionError at PersonTest.kt:24

Gradle suite > Gradle test > PersonTest.personNameTest FAILED
    java.lang.AssertionError at PersonTest.kt:19

2 tests completed, 2 failed

FAILURE: Build failed with an exception.
```

Let’s get into investigation mode and run the same command with `--info` CMD line switch to get more
info.

```zsh
./gradlew clean runTests -Dtag=person_test --info
```

Hmm. 🤔, We can see the actual value for name and age is still the initialization value and also the
`println` methods content is not printed. This is basically a hint that the setup/teardown methods
are not getting executed causing these failures.

```text
Gradle suite > Gradle test > PersonTest.personAgeTest FAILED
    java.lang.AssertionError: expected [23] but found [25]
        at org.testng.Assert.fail(Assert.java:96)
        at org.testng.Assert.failNotEquals(Assert.java:776)
        at org.testng.Assert.assertEqualsImpl(Assert.java:137)
        at org.testng.Assert.assertEquals(Assert.java:118)
        at org.testng.Assert.assertEquals(Assert.java:652)
        at org.testng.Assert.assertEquals(Assert.java:662)
        at PersonTest.personAgeTest(PersonTest.kt:24)

Gradle suite > Gradle test > PersonTest.personNameTest FAILED
    java.lang.AssertionError: expected [Rob] but found [John]
        at org.testng.Assert.fail(Assert.java:96)
        at org.testng.Assert.failNotEquals(Assert.java:776)
        at org.testng.Assert.assertEqualsImpl(Assert.java:137)
        at org.testng.Assert.assertEquals(Assert.java:118)
        at org.testng.Assert.assertEquals(Assert.java:453)
        at org.testng.Assert.assertEquals(Assert.java:463)
        at PersonTest.personNameTest(PersonTest.kt:19)

2 tests completed, 2 failed
```

This was a really weird issue for me since it was initially beyond my comprehension why testNG and
gradle are behaving this way.

After couple of hours of googling and running across multiple discussions on GitHub, Stack Overflow
and gradle docs. I finally came across the solution to fix this and get the behavior that we want.

In order for setup/teardown methods to work with above config we need to add `alwaysRun = true` in
them.

If we follow
<a href="https://testng.org/doc/documentation-main.html#annotations" target="_blank">TestNG
documentation for alwaysRun</a> we can see below:

_For before methods (beforeSuite, beforeTest, beforeTestClass and beforeTestMethod, but not
beforeGroups):_ **_If set to true, this configuration method will be run regardless of what groups
it belongs to_**_.&nbsp;  
For after methods (afterSuite, afterClass,&nbsp;…): If set to true, this configuration method will
be run even if one or more methods invoked previously failed or was skipped._

Here is the final code with the changes.

```kotlin
import org.testng.Assert
import org.testng.annotations.AfterMethod
import org.testng.annotations.BeforeMethod
import org.testng.annotations.Test

class PersonTest {
    private var name = "Rob"
    private var age = 23

    @BeforeMethod(alwaysRun = true)
    fun before() {
        println("Performing setup...")
        name = "John"
        age = 25
    }

    @Test(groups = ["person_test"])
    fun personNameTest() {
        Assert.assertEquals("John", name)
    }

    @Test(groups = ["person_test"])
    fun personAgeTest() {
        Assert.assertEquals(25, age)
    }

    @AfterMethod(alwaysRun = true)
    fun after() {
        println("Performing teardown...")
    }
}
```

And surely gradle build and test passes (validated by the debugging messages printed from setup and
teardown methods)

```text
Gradle suite > Gradle test > PersonTest STANDARD_OUT
    Performing setup...

Gradle suite > Gradle test STANDARD_OUT
    Performing teardown...
    Performing setup...
    Performing teardown...
Finished generating test XML results (0.0 secs) into: .../build/test-results/runTests
Generating HTML test report...
Finished generating test html results (0.003 secs) into: .../build/reports/tests/runTests

:runTests (Thread[Task worker for ':',5,main]) completed. Took 0.527 secs.

BUILD SUCCESSFUL in 1s
3 actionable tasks: 3 executed
```

Hopefully if you have the same problem then this blog might help you save some time.

If you are interested more into what links was referred to for arriving at this solution you can
refer below:

- <a href="https://docs.gradle.org/current/userguide/java_testing.html#test_grouping" target="_blank">Gradle
  docs — Test grouping</a>
- <a href="https://github.com/cbeust/testng/pull/1575" target="_blank">GitHub</a>

That’s it folks. Until next time. Happy coding. If you liked this or feel someone else can also
benefit from this, why not share it with a friend or colleague.
