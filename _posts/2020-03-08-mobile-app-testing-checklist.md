---
title: Mobile app testing checklist
excerpt: |
  A testers brain requires a lot of creativity and the no of scenarios that we test on a day to day basis are innumerable. Expecting the brain to remember all the ways of testing an application whether it be from a mobile, a web or an API interface is tough and an overhead. This mobile testing checklist is a brain dump of the different ways that I approach and think about testing apps in different conditions and hopefully reduces the cognitive load to remember these.
layout: post
permalink: /2020/03/08/mobile-app-testing-checklist/
image: /assets/images/wp-content/uploads/2020/03/page1.png
categories:
  - Testing
---

A checklist of things to test on a mobile app

A tester's mind is typically filled with lots of heuristics developed over years of learning and
interacting with different applications and situations.

Developing an understanding of what breaks the flow of an application, what mistakes
Developers/PMs/Designers typically make takes time and in many cases learning things hard way.

During the past couple of years, I have been heavily involved in testing mobile apps on Android and
IOS for my current employer Gojek and during this time have developed a keen sense of what are some
of the areas where bugs lie in mobile apps.

Wouldn't it be nice if we have a checklist to go through to **serve as a lens** with which we can
inspect the app from different angles to evaluate if it indeed does its job and does it well?

I got inspired to come up with this checklist after reading a
<a href="https://www.ministryoftesting.com/dojo/lessons/checklist-for-testing-web-page-functionality" target="_blank" rel="noopener">blog
post on the ministry of testing dojo site by the wonderful Lena Pejgan Wiberg,</a> Would highly
recommend reading this if you want to improve your testing skills on web pages.

Without any further adieu, here is the full checklist. Obviously, I think we can do better as a
community and hence have created a Github repo where these would be updated as my knowledge and
experiences increase. You can check it out on
<a href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md" target="_blank" rel="noopener">testing-checklists</a>

## App gestures

What actions can the user do on the app?

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Swipes
  </li>
  <li class="task-list-item">
    &nbsp;Taps
  </li>
  <li class="task-list-item">
    &nbsp;Pinches
  </li>
  <li class="task-list-item">
    &nbsp;Type
  </li>
  <li class="task-list-item">
    &nbsp;Hold
  </li>
  <li class="task-list-item">
    &nbsp;Drag and drops
  </li>
</ul>

## <a id="user-content-visuals" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#visuals" aria-hidden="true"></a>Visuals

Do the icons, images look okay and help the user in using the app?

<ul class="contains-task-list">
  <li class="task-list-item">
    Do the apps, icons, images convey the correct info to the user?
  </li>
  <li class="task-list-item">
    &nbsp;Images should fit the screen
  </li>
</ul>

## <a id="user-content-push-notifications" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#push-notifications" aria-hidden="true"></a>Push notifications

Does the app generate and handle push notifications correctly?

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Correct text for different app states?
  </li>
  <li class="task-list-item">
    Tap on PN to redirect the user to correct screen
  </li>
</ul>

## <a id="user-content-interruptions" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#interruptions" aria-hidden="true"></a>Interruptions

How does the app respond to any interruptions while using?

<ul class="contains-task-list">
  <li class="task-list-item">
    If put in the background and resumed
  </li>
  <li class="task-list-item">
    &nbsp;If killed and restarted
  </li>
  <li class="task-list-item">
    &nbsp;If Incoming call, message, PN causes the user to switch context
  </li>
</ul>

## <a id="user-content-app-permissions" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#app-permissions" aria-hidden="true"></a>App permissions

Does the app require the correct level of permissions and the behavior around those

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Behavior when the user grants/revokes certain permissions
  </li>
  <li class="task-list-item">
    &nbsp;Only necessary permissions are requested
  </li>
</ul>

## <a id="user-content-user-input" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#user-input" aria-hidden="true"></a>User Input

Does the app handle different types of inputs and allows the user to enter invalid inputs?

### <a id="user-content-boundary-values" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#boundary-values" aria-hidden="true"></a>Boundary values

Check for value/length as per below:

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;min
  </li>
  <li class="task-list-item">
    &nbsp;min &#8211; 1
  </li>
  <li class="task-list-item">
    &nbsp;max
  </li>
  <li class="task-list-item">
    &nbsp;max + 1
  </li>
</ul>

### <a id="user-content-inputs" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#inputs" aria-hidden="true"></a>Inputs

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Overflow values (Enter value > max allowed value for a given data type of the field)
  </li>
  <li class="task-list-item">
    &nbsp;Null/Empty/Blank
  </li>
  <li class="task-list-item">
    Non-ASCII characters (Swedish/Russian)
  </li>
  <li class="task-list-item">
    Copy-paste values
  </li>
  <li class="task-list-item">
    &nbsp;Special Chars (!@#$%^&*())
  </li>
  <li class="task-list-item">
    &nbsp;Leading or trailing whitespaces
  </li>
  <li class="task-list-item">
    &nbsp;Line breaks
  </li>
  <li class="task-list-item">
    &nbsp;String characters (If numeric) and numeric (If String)
  </li>
  <li class="task-list-item">
    &nbsp;Numeric separators (1000, 1.000, 1,000)
  </li>
</ul>

### <a id="user-content-date-and-times" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#date-and-times" aria-hidden="true"></a>Date and Times

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Future datetimes
  </li>
  <li class="task-list-item">
    &nbsp;Past datetimes
  </li>
  <li class="task-list-item">
    Invalid datetimes (32 days, 13 months, 25 hours, 61 minutes, 61 seconds)
  </li>
  <li class="task-list-item">
    &nbsp;Holidays
  </li>
  <li class="task-list-item">
    &nbsp;Weekends
  </li>
  <li class="task-list-item">
    &nbsp;Leap days
  </li>
  <li class="task-list-item">
    &nbsp;Timezones
  </li>
  <li class="task-list-item">
    Different DateTime formats
  </li>
</ul>

## <a id="user-content-onboarding-flows" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#onboarding-flows" aria-hidden="true"></a>Onboarding flows

<ul class="contains-task-list">
  <li class="task-list-item">
    UX when a first-time user engages with the app (Introduction flows)
  </li>
  <li class="task-list-item">
    &nbsp;These flows should be shown only a certain no of times
  </li>
  <li class="task-list-item">
    How do we introduce the user to new features in the product? Ease of comprehension
  </li>
  <li class="task-list-item">
    &nbsp;Check different user personas
  </li>
</ul>

## <a id="user-content-app-upgrades" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#app-upgrades" aria-hidden="true"></a>App upgrades

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Does app work when upgraded to a new version?
  </li>
  <li class="task-list-item">
    Can the user proceed with any in-flight flows after app upgrades?
  </li>
</ul>

## <a id="user-content-screen-sizes" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#screen-sizes" aria-hidden="true"></a>Screen sizes

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;How does the app look when opened in devices with different screen sizes (4, 5, 6 inches)
  </li>
  <li class="task-list-item">
    &nbsp;Does it look okay on a tablet?
  </li>
  <li class="task-list-item">
    &nbsp;Does it look okay on a Desktop/Laptop screen (If applicable)
  </li>
</ul>

## <a id="user-content-feature-toggles" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#feature-toggles" aria-hidden="true"></a>Feature Toggles

How does the app respond to future toggles

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Feature turned ON
  </li>
  <li class="task-list-item">
    &nbsp;Feature turned OFF
  </li>
  <li class="task-list-item">
    &nbsp;Any data created with old/new app should be compatible and should not lead to app crashes
  </li>
</ul>

## <a id="user-content-error-conditions" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#error-conditions" aria-hidden="true"></a>Error conditions

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Correct error messages are displayed in different conditions
  </li>
  <li class="task-list-item">
    CTA (Call to action) should be as per the application flow (e.g. Do not ask the user to retry in case of any terminal state in the app)
  </li>
</ul>

## <a id="user-content-navigations" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#navigations" aria-hidden="true"></a>Navigations

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Back button
  </li>
  <li class="task-list-item">
    Sorting on columns (In case of a list/table control)
  </li>
  <li class="task-list-item">
    &nbsp;Pagination (Move forward on last or move backward on first)
  </li>
</ul>

## <a id="user-content-security" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#security" aria-hidden="true"></a>Security

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;SQL Injections
  </li>
  <li class="task-list-item">
    The app should never show sensitive DB, server information
  </li>
  <li class="task-list-item">
    The app should handle different user roles and ensure correct information is displayed to the user with his role/privileges
  </li>
  <li class="task-list-item">
    &nbsp;Local storage should not show sensitive information
  </li>
</ul>

## <a id="user-content-performance" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#performance" aria-hidden="true"></a>Performance

How responsive is the app when:

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;When too many apps are open
  </li>
  <li class="task-list-item">
    When the app is used in low memory configs/devices
  </li>
  <li class="task-list-item">
    &nbsp;Normal load
  </li>
  <li class="task-list-item">
    &nbsp;X times normal load
  </li>
  <li class="task-list-item">
    &nbsp;Extremely high load from concurrent users
  </li>
</ul>

## <a id="user-content-backend-responses-and-conditions" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#backend-responses-and-conditions" aria-hidden="true"></a>Backend responses and conditions

<ul class="contains-task-list">
  <li class="task-list-item">
    &nbsp;Status codes check
  </li>
  <li class="task-list-item">
    &nbsp;2XX (Success)
  </li>
  <li class="task-list-item">
    &nbsp;3XX (Redirects)
  </li>
  <li class="task-list-item">
    4XX (Client-side errors &#8211; Bad requests)
  </li>
  <li class="task-list-item">
    5XX (Server-side errors)
  </li>
  <li class="task-list-item">
    &nbsp;Does the app block the user from proceeding when waiting for an API when not needed?
  </li>
  <li class="task-list-item">
    Does the app engage the user while waiting for an API response (with an animation/loader)
  </li>
  <li class="task-list-item">
    &nbsp;How the app handles when the API times out?
  </li>
  <li class="task-list-item">
    How the app handles cases when the server is undergoing deployments?
  </li>
</ul>

## <a id="user-content-usability" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#usability" aria-hidden="true"></a>Usability

How easy and friendly is the UI for use?

<ul class="contains-task-list">
  <li class="task-list-item">
    Text/font is readable in different mobile sizes
  </li>
  <li class="task-list-item">
    Font colors should enhance readability
  </li>
  <li class="task-list-item">
    Show numeric Numpad when nos have to be entered
  </li>
  <li class="task-list-item">
    &nbsp;Correct use of colors should be made on UI controls
  </li>
  <li class="task-list-item">
    &nbsp;Spelling and grammar
  </li>
  <li class="task-list-item">
    &nbsp;Localization
  </li>
  <li class="task-list-item">
    &nbsp;Links should not be broken
  </li>
  <li class="task-list-item">
    &nbsp;Scroll bars should be displayed when needed
  </li>
  <li class="task-list-item">
    &nbsp;Scroll bars should be hidden when not needed
  </li>
</ul>

## <a id="user-content-accessibility" class="anchor" href="https://github.com/gaurav-singh/testing-checklists/blob/master/mobile_testing.md#accessibility" aria-hidden="true"></a>Accessibility

Think about how the app can be friendly to people with deficiencies (Blind, deaf, dumb,
vision-related issues)

<ul class="contains-task-list">
  <li class="task-list-item">
    The app should be accessible via screen readers/voice commands
  </li>
  <li class="task-list-item">
    &nbsp;Accessibility ids should be available with valid text
  </li>
  <li class="task-list-item">
    &nbsp;Color should not be relied upon as the single way of identifying content (meaningful texts)
  </li>
  <li class="task-list-item">
    &nbsp;Clearly shows when an object on the screen is active
  </li>
  <li class="task-list-item">
    Links/buttons with the same text but different targets should be uniquely identifiable
  </li>
  <li class="task-list-item">
    &nbsp;Sufficient instructions for all interactive elements on the page
  </li>
  <li class="task-list-item">
    Sound/video should have text alternatives to explain the context
  </li>
  <li class="task-list-item">
    The contrast of texts, icons, images should be accessible to people with vision deficiencies
  </li>
  <li class="task-list-item">
    &nbsp;User should get prompted if a flow gets timed out
  </li>
</ul>

Below is the original checklist created on notability app:

![](/assets/images/wp-content/uploads/2020/03/page1-2.png)
![](/assets/images/wp-content/uploads/2020/03/page2-1.png)
![](/assets/images/wp-content/uploads/2020/03/page3-1.png)
![](/assets/images/wp-content/uploads/2020/03/page4-1.png)
![](/assets/images/wp-content/uploads/2020/03/page5-1.png)

If you found this useful. Do share with a friend or colleague. Until next time Cheers!
