---
layout: default
title: "FAQ"
permalink: /getting-started/FAQ/
parent: "Getting Started"
nav_order: 7
---
# FAQ
### Things that are regularly asked on r/HomeKitAutomation
---
```
Q. How do I create a notification on my HomePod?
```

A. I made a shortcut called [HomePod Notification Recorder](https://www.reddit.com/r/HomeKit/comments/ev67it/homepod_notification_recorder_a_shortcut_to_let/) that helps with the process. It will help you record and kick the audio to a Mac or PC (macOS makes it easier but it can be a windows machine) Once you have done that you then upload it to your iCloud Music Library using Apple Music or iTunes (depending on the platform). You can then use it in an "control home" action for your HomePods. Turn off repeat and all that jazz and bam. You have a notification. You can then make a volume reset automation that you can call after 10 seconds or so (add it to a scene and use it for all notifications and Siri) DISCLAIMER: this requires an Apple Music Subscription. My understanding is it needs to be any tier other than the "Voice" plain. I can come through and correct this if it isn't accurate.

```
Q. Motion sensors on my cameras turn my lights on after motion is not detected
```

A. Yes. Camera's are imaged based motion sensors. This means that instead of using IR or other proximity sensing, they just look for changes in the image. This means that Panning, lights being turned off or on, doors being opened, blinking from certain devices, etc. will trigger it rather than a person, object, or animal physically walking in the room. If you do not like this you will need to use some clever trickery, or just use a traditional sensor :). the camera has the advantage of working over "theoretically" greater distances and being a multi-functioning device. It's just a shame they don't make GREAT motion sensors (in this application) but can be used in other applications (security systems etc)

```
Q. Why don't my automations work?
```

A. Sometimes there is an issue with a hub, condition, or device. Your method on diagnosis and treatment is basically the same. This method is PRETTY reliable.
1. Disable the automation in the home app, wait 10 minutes, then reenable it. If that fails...
2. Test and debug the automation. It may be possible that there is a conflicting condition or inaccessible accessory. Checking variables in the Shortcut portions is also helpful as some types are not accepted by IF statements for example.
3. Reboot all HomeKit Hubs. My suggestion is to power them down 2 minutes if you are not sure then turn them on (usually you get a "no home hubs responding notification")
4. Reboot the wireless network and Hubs (one more time). This is pretty self explanatory. 2 minutes for all of them is my suggestion :)

```
Q. How does HomeKit Secure Video (HKSV) work?
```

A. The concept is simple, but I will reduce it even more so. Using a HomeKit hub like an Apple TV or HomePod, when a camera detects a motion event, the main home hub in charge will initiate a connection to that camera. It will then analyze the footage it sees to determine if anything should be recorded based on the conditions you lay out. It will then take the footage it has, analyze faces if needs be, encrypt the data, then send it off to apple (encrypted). When you access your footage, you communicate with your primary Home Hub for the encryption key which is then used to decrypt the footage for you to see it.

```
Q. Can I control HomeKit Secure Video cameras?
```

A. Generally? No. HomeKit Secure Video cameras dont have lots in terms of recording control they are designed to be online constantly so that the main HomeKit Hub in control can do the image processing, encrypt it, then send it to Apple for storage. if you want to control its recordings, you need to go int o the camera settings in the Home app and look over the Recording Settings. There you can define how it records between either a specified motion type (vehicles, packages, people, and animals) or to do any and all motion with HomeKit identifying the type after recording. some general things you should NOT do to control recording:
1. Use a smart plug to turn your camera off and on. Cameras require constant hub activity. They also take a while to initialize that connection. Using a contact sensor, motion sensor, or anything else to determine when to record will result in a loss of footage as there isnt enough time to start it up, start image processing, then record in a lot of cases.
2. Turnicating network access unless there is activity. This is also a bad idea. HomeKit starts and connects to your hub when the camera itself identifies a "motion" event. This motion event is monitored by the hub in question which initiates a connection to analyze the feed and send a potential recording off to Apple. doing this will only result in HomeKit not getting a motion event because no network access was allowed between the hub and camera or fragmented footage due to the up time.
its almost never a good idea to automate the capture of footage beyond the official scope due to a lot of technical limitations. The BEST thing we can do is to submit feedback to Apple requesting additional features.