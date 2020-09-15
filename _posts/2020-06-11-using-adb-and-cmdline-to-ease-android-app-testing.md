---
id: 793
title: Using adb and cmdline to ease android app testing
date: 2020-06-11T04:19:21+00:00
author: Gaurav
excerpt:
  Using adb and command line can simplify and ease many tasks that are otherwise performed via a UI.
  In this post, we cover how to use adb/scrcpy to perform some common workflows which are usually
  done during app testing
layout: post
guid: http://automationhacks.blog/?p=793
permalink: /2020/06/11/using-adb-and-cmdline-to-ease-android-app-testing/
jabber_published:
  - "1591849163"
advanced_seo_description:
  - ""
amp_status:
  - ""
spay_email:
  - ""
publicize_twitter_user:
  - automationhacks
email_notification:
  - "1591849167"
timeline_notification:
  - "1591849167"
publicize_linkedin_url:
  - null
image: /assets/images/wp-content/uploads/2020/06/android_phone-1.jpg
categories:
  - Mobile
---

![Android phone](/assets/images/wp-content/uploads/2020/06/android_phone.jpg)

Photo by Christian Wiediger on Unsplash

Hello there,

If you have been testing mobile apps on android platform, chances are there are some common
workflows/steps that you follow to enable you to test effectively.

Most of these are done as you get setup or are in the middle of actually testing the
feature/functionality on the app.

Some of these include:

- Copy the apk file over to the real device using **Android File Transfer** (on mac) while ensuring
  that the MTP mode is enable the file transfer in the first place
- Installing the build by finding it in the **sdcard** folder
- Capture any crash logs that occur while you are testing the app
- If you notice a bug, then take a screenshot
- While pairing with another dev/tester, require to share the real device screen, (You might be
  using **Vysor** for this but the loss of quality in the free version is simply annoying)
- Take videos of the test execution cycle.

Now, some or most of these flows can be performed via **Android studio** by using the `logcat`
control, however the caveat is that Android Studio/running emulator is quite performance intensive
task and captures a lot of memory

If you are running other demanding applications like IntelliJ, Pycharm and possibly Docker then it
can quickly slow down your machine considerably and bring you close to the point of frustration.

![](/assets/images/wp-content/uploads/2020/06/logcat.png)

Well we don't want that to happen to us do we?

As testers, we owe it to ourselves to solve some of these pains or to make it easy. Turns out after
a little bit of digging and some pointers from friendly android devs in my current team, I was able
to figure out some easy workarounds to accomplish all these tasks _All via command line and
adb&#8230;_ 👨🏻‍💻

Sweet. Lets get started.

## Pre-requisite

<blockquote class="wp-block-quote">
  <p>
    Most of the commands in this section requires <code>&lt;strong>adb&lt;/strong></code> to be setup and <strong>available in your path</strong>.
  </p>
  
  <p>
    Also ensure the device has <strong>USB debugging</strong> enabled in <strong>Developer Options</strong>
  </p>
</blockquote>

### Open emulator via adb

What if you wanted to open an emulator directly via command line? A way to do this is to go to AVD
manager in android studio and then click on play for the relevant emulator image you want to start.

However this could just as easily be done via CMD line using `emulator` with `-avd` option

If you are on other platforms like Windows/Linux, then find the directory where the
`Android/sdk/emulator` is present and replace that in below command.

<pre class="wp-block-code"><code>Library/Android/sdk/emulator/emulator -avd &lt;emulator_image_name&gt; -netdelay none -netspeed full</code></pre>

### How to copy a file over to you device

Assuming you have a single android device connected via USB, You can execute below command, this
would copy the **any file** from your local dir to a connected emulator or real device.

Huge time saver ⏰ and very quick compared to manually dragging the file over using Android File
Transfer mac app.

<pre class="wp-block-code"><code>adb push &lt;file&gt; /sdcard/</code></pre>

However, If you have multiple emulators/devices connected on executing above command you would get
an error like below:

<pre class="wp-block-code"><code>adb: error: failed to get feature set: more than one device/emulator</code></pre>

To workaround, We need to tell adb, which device we want to send the file over to.

First, we need to know what devices are connected. Execute below

<pre class="wp-block-code"><code>adb devices -l</code></pre>

This would return a list of connected device. Notice adb provides a unique string for all real
devices (`5200d275428186b3`) and for all the running emulators (`emulator-<TCP_PORT>`)

<pre class="wp-block-code"><code>List of devices attached
5200d275428186b3       device usb:342097920X product:m30ltedd model:SM_M305F device:m30lte transport_id:1
emulator-5554          device product:sdk_gphone_x86_arm model:AOSP_on_IA_Emulator device:generic_x86_arm transport_id:2</code></pre>

Cool, so to transfer the file over, we need to tell `adb` to use the device that we are interested
in with the `-s` option and the remaining command remains same.

<pre class="wp-block-code"><code>adb -s &lt;emulator_or_real_device_id&gt; push &lt;file&gt; /sdcard/</code></pre>

### Installing APK via adb

Given that you have the APK file in a dir on your local machine, you can use `install` command in
`adb` to directly stream the file over and install on the device

<pre class="wp-block-code"><code>adb -s &lt;emulator_or_real_device_id&gt; install &lt;file_name&gt;.apk</code></pre>

Simple and sweet! 🙌🏼

### Uninstalling the previously installed app

Running the above command would install the app every time, but if you wanted to do a clean install
and ensure the app is not already installed (Simulate a first time users experience)

Then we can easily uninstall the app via `pm` (package manager) command

You would first need to know the package name for the app that you want to uninstall, Run below

<pre class="wp-block-code"><code>adb -s &lt;emulator_or_real_device_id&gt; shell dumpsys window windows | grep -i "mCurrentFocus"</code></pre>

This would give an output like below:

<pre class="wp-block-code"><code>mCurrentFocus=Window{253d2d3 u0 com.example.app.staging/com.example.app.RootActivity}</code></pre>

Here the package name would be `com.example.app.staging`

To uninstall, we can run below command:

<pre class="wp-block-code"><code>adb -s &lt;emulator_or_real_device_id&gt; shell pm uninstall &lt;package_name&gt;</code></pre>

So, now we know how to copy a file over, and also install an app on any device (real or emulated).

## Testing the app

Given we are testing the application, the 3 main tasks that we need to perform are:

- Take a screenshot
- Record a movie
- Capture crash logs
- Share the real device screen on your system (during a pairing session)

### Capturing a screenshot

Lets say, I have the Fake GPS on the real device screen and I noticed a bug, I would want to share
this with the devs in the bug report

We can use `screencap` utility to capture and store the screenshot

To directly take the screenshot and copy to your local machine execute below:

<pre class="wp-block-code"><code>adb exec-out screencap -p &gt; &lt;file_name&gt;.png</code></pre>

### Recording a video:

To record a video we can use `screenrecord` command with adb

Firstly open `adb shell`

<pre class="wp-block-code"><code>adb -s &lt;emulator_or_real_device_id&gt; shell</code></pre>

Then execute below to start recording

<pre class="wp-block-code"><code>screenrecord --verbose /sdcard/demo.mp4</code></pre>

Finally when you are done, Press `Control + C` to exit

and finally copy the file to your local machine via `adb pull`

<pre class="wp-block-code"><code>adb pull /sdcard/demo.mp4</code></pre>

### Sharing your screen

Often when you are pairing with a dev or doing a mob testing session with the team, You would want
them to see what you are trying on the real device. Android studio currently does not include any
tool to cast the screen.

Many people use Vysor tool for this, however the free version gives a very bad casting experience.

Recently I came across `<a href="https://github.com/Genymobile/scrcpy">scrcpy</a>` a wonderful open
source tool to do this without any quality loss.

You can quickly [install it via `homebrew`](https://github.com/Genymobile/scrcpy#macos)

<pre class="wp-block-code"><code>brew install scrcpy</code></pre>

And once installed to share your screen, just run:

<pre class="wp-block-code"><code>scrcpy --show-touches</code></pre>

And you quickly get a screen on your machine with your device screen (which you can even control via your mouse and keyboard, how sweet is that 😉). Enjoy pairing and sharing stuff with ease. 🙆🏻‍♂️

![](/assets/images/wp-content/uploads/2020/06/image.png)

`scrcpy` is a quite powerful and useful tool and I would highly recommend checking it out. It made
my life so much simpler and better while testing on android real devices

### Logging crashes via logcat

What if you are testing and the app crashes in the middle. Unless its a easily reproducible crash,
sometimes its very difficult to isolate that exact log in the middle of a sea of logs that `logcat`
utility generates.

However fret not, with a single command we can get the logs for the last crash via this simple
command.

<pre class="wp-block-code"><code>adb -s &lt;emulator_or_real_device_id&gt; logcat -b crash &gt; &lt;file_to_which_you_want_to_write&gt;</code></pre>

## Conclusion:

Challenge yourself to use more of command line utils and you would realize there is immense value
and comfort in using them.

In case you want to learn more about the wonders of adb, Checkout
[developers.android.com](https://developer.android.com/studio/command-line/adb)

If you found this post useful, Share it with a friend or colleague. Until next time. Happy testing!
