---
title: Viewing network traffic calls on IOS real device using MITM Proxy
permalink: /2018/09/07/viewing-network-traffic-calls-on-ios-real-device-using-mitm-proxy/
categories:
  - "Test tooling"
  - "Mobile testing"
tags:
  - "mitm proxy"
---

### Getting Started

If you have used android studio for helping in setup emulators, you would have realized how nifty
the `Logcat` feature is. It allows us to see all network calls being made as we perform any user
journey on the mobile device. Ever wondered how to do this on an IOS real device? `Xcode`? Sadly we
do not have such a feature in Xcode. So what is the solution. Enter
<a href="https://mitmproxy.org/" target="_blank">MITM Proxy</a>. For the uninitiated MITM is a
powerful HTTPS proxy which can be used for multiple use cases. Today lets see how we can use it to
capture traffic on an IOS real device.

### Lets setup MITM

### Installing and starting MITM proxy on mac

- Install MITM using homebrew `brew install mitmproxy`
- Run mitm proxy by typing `mitmproxy` in terminal
- Type `ifconfig` and make a note of the machines IP address, printed in `en0` section.
  Alternatively you can also get the IP address by navigating to
  `System Preferences > Network > Wifi > Advanced > IPV4`

### Setting up IOS real device to pass traffic via proxy

- Open `Settings > Wifi > <your_wifi_name> > Tap on Configure proxy under HTTP proxy`
- Select `manual` and enter the mac machines IP address in Server and default port as `8080`. For
  now leave `Authentication` turned off

![Configure proxy](/assets/images/wp-content/uploads/2018/09/56f52-1jb1p2scv7g2trj3qgsassa.png)

- Open `mitm.it` on any browser in real device and tap on `Apple icon` followed by tapping `install`
  couple of times to install `mitmproxy certificate` on the device
- After setup verify certificate profile is setup by navigating to
  `Settings > Profile and Device Management` and verifying `MITM proxy` is listed in list of
  certificates

![Profile and device management](/assets/images/wp-content/uploads/2018/09/4ee92-1ydo2blcajvc6a-hjfk0c7w.png)

- Finally ensure for MITM proxy, Full trust is enabled for root certificate the installed
  certificate by navigating to `About > Certificate Trust Settings`

![About certificate trust settings](/assets/images/wp-content/uploads/2018/09/3c118-1jcqnjz0dp9t6geffwxixxw.png)

### How to see logs

- Once MITM is running in terminal you would start seeing network calls having all requests,
  response and header info captured.
- Navigate to the call that you want to see the response for and then press enter

> _Tip: If you want to see calls made by your apps with a specific pattern in the URL type_
> `<strong><em>f</em></strong>` _and then enter a pattern, this would filter out all other captured
> network calls._

- To see all available commands, press `?` to see a summary of available commands.

That’s it. Enjoy! Do revert in case you have any specific questions on this and lets figure them out
together
