---
layout: default
title: "Using Device Responsiveness As A Trigger"
permalink: /LetsBuildAdvanced/ResponseTriggers/
parent: "Let's Build! (Advanced)"
nav_order: 9
---
# Using Responsiveness As A Trigger
### Trigger based on device unresponsiveness
This was submitted by an anonymous reddit user who asked they not be credited. the post is on our sub but has also been mirrored here. They did not provide images.
---

There are lots of reasons to want to be notified of a device going unresponsive, or to have an automation triggered by such an occurrence. I have a sensor in my detached garage that tells me if the garage door opens. And I have an automation that tells me if that sensor is not responding, meaning the garage could be opened without my knowledge.

I have an Aqara hub that occasionally goes unresponsive, and I have it plugged into a smart-plug that power-cycles the hub if it goes unresponsive for more than 2 minutes.

The reason this is at all challenging is that any automation that checks the status of an accessory just stops running when that accessory doesn't respond, instead of returning a value such as "no response". This makes a straightforward automation like “if no response from accessory, do Y” completely not feasible, because the automation just dies while trying to evaluate the first “if” condition. So we just have to work with that constraint, and the way to do it is to build something that functions like a canary- something that is pre-positioned such that its absence can be used as a definite signal, in this case, as a signal that the accessory isn’t responding.
This tutorial assumes you have homebridge and that you're familiar with the Dummy Switch and the Delay Switch plugins. Take a moment to grab them and look over the settings panes.

First, you build a clock / heartbeat. Make two dummy switches, Tic and Toc. Have them automatically turn off after 30 seconds of being on. Then have Tic turning off turn Toc on, and vice-versa. You now have a basic heartbeat, and you should turn it on by turning on either Tic or Toc. I augment this with another dummy switch named Heartbeat. Heartbeat turns itself off after 2 minutes and 30 seconds. Heartbeat turning off turns on Toc. Every time Toc turns off, it turns on the hearbeat. This is like having a watchdog timer. This way if there is a interruption like a homepod mini rebooting due to losing power, though the tic-toc will get interrupted and die, Heartbeat will still persist and stay on, because it is running on Homebridge, hopefully long enough for your device to finish rebooting and become responsive again. 2 minutes 30 seconds might not be long enough, I forget what mine is set to. You also need to make all three of these dummy switches resettable (it's a fairly new feature, kinda- it previously was the default behavior, before it was an explicit setting. But now it defaults to NOT resettable, which is weird and makes things unpredictable. So don't leave this setting out, or testing will be quite confusing.) The self-turn-off times mentioned above are configured in homebridge plugin properties, not in homekit.

Note: The reliability of this is somewhat aided by your Homebridge not being vulnerable to momentary power outages. My homebridge instance that I use for this runs on a RasPi Zero W that is plugged into a UPS. So it will not get power cycled when the lights flicker. This has a downside, mentioned below.

Now let's say you want a notification of unresponsiveness. Make a Delay Switch- these are the best, and I think only, way to get native homekit notifications, and they don't require an internet connection to work. Call this delay switch Pumpkin, and set it to turn off after 4 minutes (this is done in homebridge). Set it so that if pumpkin turns off, you get a notification on a device, this is done in Home.app on the motion sensor that comes with your Delay Switch, since the way delay switches give you notifications is by acting as a contact sensor / motion detection device.

Now you have it set such that if Pumpkin is turned on, but then goes ignored for a few minutes, you will get a notification. So we just need to make sure Pumpkin is normally on, but will turn off if the device you care about goes unresponsive. This is easy. Have Toc turning off trigger an automation. You'll make it using the "convert to shortcut" functionality. The automation will look something like this:

1. Get status of the device you care about (it does not matter which status item you are getting).
2. Turn on Pumpkin.

And that's it. If the device is responding, its status will be received, and the automation will then turn on pumpkin (which is probably already on) thereby resetting Pumpkin's timer. If you care about how often a device goes unresponsive, one way to track that is to collect these notifications.

Next step: power cycling

It's probably obvious how you modify this to power-cycle a device that's on a smart-plug. To do this, you could configure Pumpkin as a Delay Switch or as a Dummy Switch, it doesn't matter much. You just do everything as before, and then have Pumpkin turning off trigger an automation. My automation looks like this:

1. if pumpkin turns off (this is the trigger condition, not actually an “if” statement
2. Power off the outlet
3. wait three seconds
4. Power on the outlet.
5. Turn one of my living room bulbs green to let me know that it was necessary to power-cycle my device. (Step 5 is optional, of course.)

Augmentations: There are several ways to make this more robust. I mentioned the Heartbeat addition above when talking about Tic and Toc. This is also useful because Siri can be told to turn on the heartbeat, or asked about the heartbeat.

Automated Startup: There is very little you can do to turn your clock / heartbeat back on if your homepod mini / other home hub is off long enough for Heartbeat to turn off. You could have Heartbeat2, which has a longer turnoff time. But that's finite. One way around this is to have Heartbeat turned on in a time-based automation. I have my Heartbeat turned on every day at 5 past noon.

Also, if you reboot your homebridge, it will kill your heartbeat. One way around this is to have it jump-start it. With a Delay Switch, you can configure it to be turned on at startup. Do this, configure it to wait a few minutes, and then turn off. Have it turning off trigger Heartbeat to turn on. I also have this trigger turn on Pumpkin because if Pumpkin is not responding, I want to hear about it or trigger the power-cycle. If Pumpkin is just off at startup and stays that way, then I'll never hear about it / force it to power cycle.

Having Homebridge on a backup power supply does have a downside. If power is off for a while (longer than the timeout for Heartbeat or whatever other watchdogs you've built) then when your home hub turns back on, it won't turn Heartbeat back on until the next time you have a time-triggered automation to do that. I guess one way around this would be to have TWO homebridges running on different hardware, one using backup power and the other inteitonally NOT using backup power, and either of them can start-up the heartbeat. But that sounds like overkill.
Usage recommendations:

After playing around with this for a while, I have a few other recommendations, some obvious and others less obvious. First, your home probably does not need more than one alternating tic-tic/ heartbeat. It can be used to trigger lots of things. I have one automation that runs when Tic turns off and a separate one that runs Toc turns off, both tending different things. If these were combined in one automation, that automation would error out whenever one of the devices I care about went unresponsive, making it impossible to monitor the other device. One could alleviate this by running two separate automations from the same trigger (such as Toc turning off) but you then have no control over the order in which they run, and I haven’t been able to tell if the order they run in is even repeatable. So you’d potentially have a similar situation to having only a single automation.

Another recommendation is that if you are just trying to get a notification of an unresponsive device (using a single delay switch), and not trying to take some specific action, you can pile a bunch of devices into one automation, as follows:

1. Get state of device 1
2. Get state of device 2
3. Etc.
4. turn the delay switch on.

This will cause any of those devices not responding to kill the automation, and then you’ll get the notification from the delay switch. You won’t know which device isn’t responding, but you were notified so you can just open the home app and look.
