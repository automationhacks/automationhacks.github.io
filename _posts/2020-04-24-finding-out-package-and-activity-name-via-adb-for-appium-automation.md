---
title: Finding out package and activity name via adb for appium automation
excerpt: A post on how to use adb and aapt tools in android sdk to figure out the package and activity names for use in Appium desired capabilities.
permalink: /2020/04/24/finding-out-package-and-activity-name-via-adb-for-appium-automation/
Categories:
  - "Mobile testing"
tags:
  - "Appium"
  - "Android"
  - "Adb"
---

 ![Android head image by Wikimedia commons](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Android_robot_head.svg/1280px-Android_robot_head.svg.png)

Hey there,

A common problem when starting with 🤖 **android automation** with appium after you have learned basics is to find the **package name** and **activity name** to get started with Appium driver session

This is easy if you have access to the source code and friendly developers around but what if you want to know this information for any app from the Google play store? 🕵🏻‍♂️

Turns out its possible to get this info entirely using `adb`.

Let's see how.

## Ensure adb is set up and on path

* Ensure android SDK is installed and already in your path. It automatically gets installed if you <a href="https://developer.android.com/studio" target="_blank" rel="noopener">download Android studio</a>
* Add below entry in your `.zshrc` or `.bashrc` file followed by `source <file_name>` if you are on the mac otherwise add these in your windows system environment variables to allow all the common CLI to be available without having to type the fully qualified path every time

<pre class="wp-block-preformatted"># Android specific env vars
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$ANDROID_HOME/tools:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/tools/bin:$PATH</pre>

## Get app package name

* Open the app on a real device connected via USB (with USB debugging on) or on an android emulator
* Execute below:

<pre class="wp-block-preformatted">adb shell dumpsys window windows | grep -i "mCurrentFocus"</pre>

For example, Here is the output if you run above command with twitter app already open

<pre class="wp-block-preformatted">mCurrentFocus=Window{6c0629c u0 com.twitter.android/com.twitter.android.onboarding.common.CtaSubtaskActivity}</pre>

You should see `packageName/currentActivity` in the output.

As you can rightly guess our package name is:

<pre class="wp-block-preformatted">com.twitter.android</pre>

## Get start activity for use

While the above command gets you to name of the current activity, It might not be the activity that the app starts with and thus cause your appium test case to fail in driver initialization itself

How can we work around this?

We can use `adb` and `aapt` tools to figure this out. Let's see how to do this.

### Get a list of installed packages and path to base apk

We can execute the below command to get a list of **all installed packages** in the device and filter to get only the app for which we want to find out this info

<pre class="wp-block-preformatted">adb shell pm list packages -f | grep -i "&lt;app_name&gt;"</pre>

Here is a sample output for twitter app

<pre class="wp-block-preformatted">package:/data/app/com.twitter.android-eka4BzKX4Con18lwXr0yAQ==/base.apk=com.twitter.android</pre>

### Get the base.apk file for the app

Next, we need to get the base apk file into our local machine. We can easily do this via `adb pull`

<blockquote class="wp-block-quote">
  <p>
    Also, notice, I have passed the output of the above command after removing the app package name
  </p>
</blockquote>

<pre class="wp-block-preformatted">adb pull /data/app/com.twitter.android-eka4BzKX4Con18lwXr0yAQ==/base.apk</pre>

You should see a file getting downloaded on your current path. For example:

<pre class="wp-block-preformatted">/data/app/com.twitter.android-eka4BzKX.... 80.2 MB/s (19076098 bytes in 0.227s)</pre>

### Get the activity name using `aapt`tool

Android SDK comes with <a href="https://developer.android.com/studio/command-line/aapt2" target="_blank" rel="noopener">AAPT tools (Android asset packaging tool)</a> which allows us to compile and build into binary format. We can use this for our specific purpose of finding out the start activity

If `aapt` is already on your path then you can remove directly use it else choose the version which you want to use (usually the latest) under `build-tools` and run below command with your `base.apk` files name

<pre class="wp-block-preformatted">~/Library/Android/sdk/build-tools/28.0.3/aapt dump badging base.apk | grep -i "launchable-activity"</pre>

Voila! 🙆🏻‍♂️

You should output like below. This lets you know the activity which can be used to launch the app with which in this case is: **com.twitter.android.StartActivity**

<pre class="wp-block-preformatted">launchable-activity: name='com.twitter.android.StartActivity'  label='' icon=''</pre>

## Conclusion

ADB is a really powerful tool for android automation and with the use of `adb` and `aapt` we can very easily find out the package name and activity name to use to start with our appium automation.

If you found this tip useful, do share it with your friends or colleagues and until next time. Cheers! Happy testing.
