---
title: Testing Android/IOS apps under network conditions
author: Gaurav
excerpt:
  Mobile apps should be tested not just under WiFI but under "more" realistic network conditions. In
  this post we see how we can simulate these conditions on Android and IOS native apps.
permalink: /2020/07/06/testing-android-ios-apps-under-network-conditions/
image: /assets/images/wp-content/uploads/2020/07/leon-seibert-2m71l9fa6mg-unsplash.jpg
categories:
  - "Mobile testing"
tags:
  - "Android"
  - "iOS"
---

![](/assets/images/wp-content/uploads/2020/07/leon-seibert-2m71l9fa6mg-unsplash.jpg)

Photo by
[Leon Seibert](https://unsplash.com/@yapics?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
on
[Unsplash](https://unsplash.com/s/photos/slow-internet?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

It's 2020 and mobile phones are ubiquitous. Everyone has it and uses it constantly. Most of times as
testers, we test our mobile apps in office Wifi conditions with a ideal high quality internet
connections in terms of app performance.

However, we all know real life network is far from this ideal. We/our consumers mostly use our apps
on the Go (travelling in a bus, sometimes even when walking) and the network conditions will rarely
be the conditions that we test under.

In such cases, a carefully thought out and tailored UX can be the difference between a happy
consumer who would like to use your app again Vs a frustrated or confused consumer who eventually
uninstalls the app and move on to something else.

So hopefully, by now you must feel convinced that it is quite **important** to get _feedback about
your apps quality under different network conditions_.

However, since we can't really travel to different parts of the office/home/city in search of such
pockets of bad network areas every time we want to test right?

Luckily both Apple/Google gives us ways to simulate these network conditions. Let's take a look at
how:

## Simulate network conditions on IOS

Apple provides a handy utility to help to simulate network conditions called **network conditioner**

### Setup network conditioner

Connect your iPhone real device to your laptop via USB or start the simulator via Xcode

Open **Windows > Devices and Simulator**

![](/assets/images/wp-content/uploads/2020/07/nwc_1.png)

Under Device conditions select **Network Link**

![](/assets/images/wp-content/uploads/2020/07/nwc_2.png)

Once selected, You can choose a network in the range of _Very poor to Edge, 2G, 3G and what not_. 🥳

![](/assets/images/wp-content/uploads/2020/07/nwc_3.png)

Also, Once this setting has been set via Xcode, You can now access **Developer** section in your
iPhone settings and enable as well as change these conditions easily

> Remember to enable the network conditioner and then choose whichever condition you want to test on.

![](/assets/images/wp-content/uploads/2020/07/nwc_4.png)

![](/assets/images/wp-content/uploads/2020/07/nwc_5.png)

## Simulate network conditions on Android

### On emulator

If you are running an emulator image via android studio, then changing the network speed is as
simple as going to **Emulator settings > Cellular > Select Network Type > Select Signal Strength**
as per your test scenario requirement

![](/assets/images/wp-content/uploads/2020/07/android_studio_cellular.png)

You can also control this
[setting via adb](https://developer.android.com/studio/run/emulator-commandline.html) by updating
`netdelay` option of **emulator utility** with values like `gprs`, `edge`

<pre class="wp-block-syntaxhighlighter-code">~/Library/Android/sdk/emulator/emulator -avd &lt;avd_name&gt; -netdelay none -netspeed full</pre>

### On a real device

If you real device has a SIM, then you can go into **Network settings** (Wifi & internet on
Android 10) > **SIM and network** and then select the **Preferred network type** to either 2G, 3G or
4G

Other possible approaches could be to use a proxy tool to throttle network calls by introducing some
programmatic delays. Thought not the most realistic way to set this up but nonetheless effective.
More details on this in a future post.

## Conclusion

Next time when you feel your app works perfectly under perfect network conditions, maybe try using
one of these above to test the app under less reliable network and see if the app still offers a
graceful experience to the user.

If you found this useful, Do share with a friend or colleague. Until next time, Happy testing.

## Further read/References

In case you want to read a bit more about this topic, feel free to checkout any of these excellent
articles for more details.

- <https://developer.android.com/studio/run/emulator-commandline.html>
- <https://stackoverflow.com/questions/7026251/simulate-low-network-connectivity-for-android>
- <https://appiumpro.com/editions/63-capturing-android-emulator-network-traffic-with-appium>
- <https://blog.bam.tech/developer-news/simulate-poor-network-test-mobile-apps-device>
