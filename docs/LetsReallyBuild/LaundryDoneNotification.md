---
layout: default
title: "Get a Notification When Laundry Finishes"
permalink: /LetsBuildAdvanced/LaundryDoneAlert/
parent: "Let's Build! (Advanced)"
nav_order: 13
---
# Get a Notification When Laundry Finishes
### Originally written by [u/Old_Expression_1853](https://www.reddit.com/user/Old_Expression_1853/).
---

I thought I’d share an automation which gives me a notification when the washing is done. After a little trial and error, I think it’s working as I anticipated, and it helps me be more aware about helping my wife out with the washing.
I've also heard of people using Aqara vibration sensors to do the same thing, but I feel like this is a probably more accurate way of going about it (I also don't have any spare vibration sensors but have heaps of smart plugs)
---
To do this, you’ll need:
Smart plug with energy monitoring [smart plug]. I used this one running through [Homebridge](https://homebridge.io)
Homebridge Dummy Switch Plugin [dummy switch]
[Pushcut](https://pushcut.io)
[Home+](https://hochgatterer.me/home+/) or [Eve](https://apps.apple.com/us/app/eve-for-homekit/id917695792)
Stock HomeKit (Home) app
---
Step 1:
Plug in the smart plug between the washing machine and your wall. (lol)
---
Step 2:
Create a dummy switch in Homebridge that will turn off after the maximum time you would do a load (mine is 40 mins, or 2400000 milliseconds).
---
Step 3:
In Home+, create an automation called ‘Washing Start’ with the following conditions:
When this happens:
[Smart plug] Current Consumption changes to greater or equal 2.0w
Control Accessories:
[Dummy Switch] ON

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/WashingAutomationTrigger1.png?raw=true)

---
Step 4:
Create a Pushcut notification. Copy URL from bottom left.
I called mine ‘Washing is done’, which has a Shortcut attached as an action that adds ‘Take the washing out’ to my reminders. You can download the shortcut here.
For more information on Pushcut, I highly recommend watching this video by Shane Whatley. It’s an incredibly useful app.

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/washingPushcutNotification.png?raw=true)

---
Step 5:
in Home+, create an automation called ‘Washing Finish’ with the following conditions:
When this happens:
[Smart plug] Current Consumption changes to less of equal 2W
Under the condition (IMPORTANT)
[Dummy switch] is ON
Hit save, move over to the stock HomeKit (Home) app and find the same automation (it’ll say it’s disabled)
Select Accessories and Scenes > Scroll to the bottom, hit ‘Convert to Shortcut’.
Add ‘Get contents of’ and paste your Pushcut URL in the area for URLs. IMPORTANT, hit the down arrow and change ‘Method’ to POST.
Add ‘Control [home name]’, set [Dummy Switch] OFF
Next > Done

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/WashingNotificationAutomation3.png?raw=true)

---
And we’re finished!
---
Improvements
I’m considering creating an automated reminder on an old iPhone, which is running a continuous Pushcut Automation Server - this will add a reminder to my reminders instead of just a notification. I’m just thinking this could be a bit annoying if I’m at work and my wife is home, but it could be a good alternative.

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/WashingShortcutforPAS.png?raw=true)
