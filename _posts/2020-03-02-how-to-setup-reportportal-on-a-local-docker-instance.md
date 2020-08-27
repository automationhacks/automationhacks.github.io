---
id: 538
title: How to setup ReportPortal on a local docker instance
date: 2020-03-02T02:30:17+00:00
author: Gaurav
excerpt: Report portal is one of the new reporting solutions available. It supports multiple different test frameworks like TestNG, Cucumber, Pytest and many more. This post is the first in a series of posts on how to set up report portal effectively and leverage the best use out of it.
layout: post
guid: http://automationhacks.blog/?p=538
permalink: /2020/03/02/how-to-setup-reportportal-on-a-local-docker-instance/
jabber_published:
  - "1583116223"
timeline_notification:
  - "1583116225"
email_notification:
  - "1583116225"
image: /wp-content/uploads/2020/03/report_portal_login.png
categories:
  - Framework development
  - Testng
---
Report portal is one of the new reporting solutions available. It supports multiple different test frameworks like TestNG, Cucumber, Pytest and many more.

This post is the first in a series of posts on how to set up report portal effectively and leverage the best use out of it.

Let&#8217;s get started.

## Setup with Docker

I have created a sample project on Github which would have all the examples from this project. You can find it <a href="https://github.com/gaurav-singh/grasp-reporting" target="_blank" rel="noopener">here</a> and would also have the code snippets in GitHub gists.

The instructions that I am describing here can also be found on <a href="https://reportportal.io/docs/Deploy-with-Docker" target="_blank" rel="noopener">report portal docs</a>

  * As a pre-requisite, you should <a href="https://www.jetbrains.com/help/idea/getting-started-with-gradle.html" target="_blank" rel="noopener">set up an empty Java/kotlin project with Gradle</a>. The easiest way to set this up is with the use of IntelliJ wizard, however, feel free to use the method of your choice
  * Report portal uses services like **PostgresSQL, RabbitMQ, and Traefik** behind the wraps and while there is an option to <a href="https://github.com/reportportal/shell-installation" target="_blank" rel="noopener">set these up individually without docker</a>, the quickest and simplest way to start using **Report portal is to use Docker**
  * Make sure you have a **docker engine and <a href="https://docs.docker.com/compose/install/" target="_blank" rel="noopener">docker-compose</a>** already installed. If you are on Mac, Using Docker for mac would make the quickest sense however Docker is available on the platform of your choice (Windows, Linux) and docker docs are a good resource to set these up
  * Download latest docker-compose.yml from <a href="https://github.com/reportportal/reportportal/blob/master/docker-compose.yml" target="_blank" rel="noopener">here,</a> a quicker way to download this is to use below command

<pre class="wp-block-preformatted">curl https://raw.githubusercontent.com/reportportal/reportportal/master/docker-compose.yml -o docker-compose.yml</pre>

  * Once downloaded, execute below command to pull the required images and start containers

<pre class="wp-block-preformatted">docker-compose -p reportportal up -d --force-recreate</pre>

Report portal recommends you use allocate at least 3 GB of ram and this could be set up via the Docker desktop console. There are a bunch of other configurations we can make but let&#8217;s go with a minimal setup first

We would revisit these in a future post.

## Verify login

With the above steps, report portal containers are already spun up.

To verify, it is running fine. You can navigate to <a href="http://localhost:8080/ui/#login" target="_blank" rel="noopener">http://localhost:8080</a>, you should be able to see the login screen.<figure class="wp-block-image">

<img loading="lazy" width="750" height="501" src="https://i1.wp.com/automationhacks.blog/wp-content/uploads/2020/03/report_portal_login.png?resize=750%2C501&#038;ssl=1" alt="report_portal_login.png" class="wp-image-567" data-recalc-dims="1" /> </figure> 

You can log in with the default user or admin passwords below:

<pre class="wp-block-preformatted">default\1q2w3e
or
superadmin\erebus</pre>

<blockquote class="wp-block-quote">
  <p>
    Please remember to change these as soon as you login for security sake
  </p>
</blockquote>

## Create a blank project

After logging in as admin, Let&#8217;s create a blank project for our test setup

Go to the top-right icon, select Administrate and then create a new project. I have created a dummy project by the name of **test_project**

Once created, select the project from the drop-down list and then again click on the login information section and select Profile.<figure class="wp-block-image">

<img loading="lazy" width="750" height="99" src="https://i0.wp.com/automationhacks.blog/wp-content/uploads/2020/03/rp_project_selection.png?resize=750%2C99&#038;ssl=1" alt="rp_project_selection.png" class="wp-image-570" data-recalc-dims="1" /> </figure> 

Make a note of the **information in the Profile section**, we are going to need it later on

## Setting up Gradle, dependencies, and listener

Report portal can easily be set up with any build tool of your choice.

In this example, we are going to use Gradle and then set up the required dependencies and the report portal listener which would be able to capture the test execution events and send them in real-time to our dashboard

Below is the basic configuration to set up the required agent and listener via gradle<figure class="wp-block-embed is-type-rich">

<div class="wp-block-embed__wrapper">
  <div class="gist-oembed" data-gist="4c58cb3c7054af57f4c52400368bfc3d.json" data-ts="8">
  </div>
</div></figure> 

## Explanation:

  * Ln 10 &#8211; 13 sets up the maven repository for report portal on the bintray site
  * Ln 15 &#8211; 21 sets up an overridden task of type `Test` with logic to print all output on the console (Ln 17), disable the use of default listeners (Ln 18) and registers the report portal TestNG listener (Ln 19)
  * Ln 25 Set up a basic TestNG agent
  * Ln 26 Setup the latest version of TestNG

## Setup properties file

Create a file named `reportportal.properties` under `test/resources` and paste the earlier copied content from the **profile** section of your created project

## A simple test

I have a verify basic TestNG test setup in the test folder which should always fail (for demo purposes)<figure class="wp-block-image">

<img loading="lazy" width="750" height="324" src="https://i1.wp.com/automationhacks.blog/wp-content/uploads/2020/03/calc_test.png?resize=750%2C324&#038;ssl=1" alt="calc_test.png" class="wp-image-572" data-recalc-dims="1" /> </figure> 

## Let&#8217;s run

Now, let&#8217;s run the suite. Execute below command:

<pre class="wp-block-preformatted">./gradlew clean runTests</pre>

Once the suite executes, we can observe the failure in the report portal as a launch

### Launches:

Every unique test run is called a launch in the report portal.

We can now select the launch to see an overview of the run. We can also see that our suite failed as expected.<figure class="wp-block-image">

<img loading="lazy" width="750" height="211" src="https://i0.wp.com/automationhacks.blog/wp-content/uploads/2020/03/result_1-1.png?resize=750%2C211&#038;ssl=1" alt="result_1.png" class="wp-image-575" data-recalc-dims="1" /> </figure> 

We can select the failure to see more details and mark each test under different categories (Product bug, automation bug, system issue). By default, every test is marked as **To investigate**<figure class="wp-block-image">

<img loading="lazy" width="750" height="265" src="https://i2.wp.com/automationhacks.blog/wp-content/uploads/2020/03/result_2.png?resize=750%2C265&#038;ssl=1" alt="result_2.png" class="wp-image-574" data-recalc-dims="1" /> </figure> 

Also, we can click on the test and see the full stack trace of the failure similar to the Gradle report. However, as more tests are run, we are able to easily see a historical snapshot of the same test and how it behaved in different launches.<figure class="wp-block-image">

<img loading="lazy" width="750" height="346" src="https://i2.wp.com/automationhacks.blog/wp-content/uploads/2020/03/resullt_3.png?resize=750%2C346&#038;ssl=1" alt="resullt_3.png" class="wp-image-576" data-recalc-dims="1" /> </figure> 

## Conclusion

Report portal is an exciting new tool and gives you the ability to have a central dashboard for all your different test runs regardless of the framework you have used to author it.

In future posts, we would see

  * How to set up logging in the test
  * Create widgets on the dashboard
  * Configure report portal for optimum use

In case you found this post useful. Do share it with your friends or colleagues.

### References:

There are many resources already available about the Report portal. Check them out.

  * [Report portal website](http://reportportal.io/)  
    <a href="https://www.youtube.com/c/ReportPortalCommunity" target="_blank" rel="noopener">YouTube</a>  
    <a href="https://github.com/reportportal/reportportal" target="_blank" rel="noopener">GitHub</a>  
    <a href="http://reportportal.io/docs/Installation-steps" target="_blank" rel="noopener">Installation steps</a>