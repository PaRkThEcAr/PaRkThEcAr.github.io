---
layout: default
title: "HomeKit Apps"
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

A. I made a shortcut called HomePod Notification Recorder that helps with the process. It will help you record and kick the audio to a Mac or PC (macOS makes it easier but it can be a windows machine) Once you have done that you then upload it to your iCloud Music Library using Apple Music or iTunes (depending on the platform). You can then use it in an "control home" action for your HomePods. Turn off repeat and all that jazz and bam. You have a notification. You can then make a volume reset automation that you can call after 10 seconds or so (add it to a scene and use it for all notifications and Siri) DISCLAIMER: this requires an Apple Music Subscription. My understanding is it needs to be any tier other than the "Voice" plain. I can come through and correct this if it isn't accurate.

```
Q. Motion sensors on my cameras turn my lights on after motion is not detected
```

A. Yes. Camera's are imaged based motion sensors. This means that instead of using IR or other proximity sensing, they just look for changes in the image. This means that Panning, lights being turned off or on, doors being opened, blinking from certain devices, etc. will trigger it rather than a person, object, or animal physically walking in the room. If you do not like this you will need to use some clever trickery, or just use a traditional sensor :). the camera has the advantage of working over "theoretically" greater distances and being a multi-functioning device. Its just a shame they don't make GREAT motion sensors (in this application) but can be used in other applications (security systems etc)

```
Q. Why do(es) X automation(s) not work?
```

A. Sometimes there is an issue with a hub, condition, or device. Your method on diagnosis and treatment is basically the same. This method is PRETTY reliable.
1. Disable the automation in the home app, wait 10 minutes, then reenable it. If that fails...
2. Test and debug the automation. It may be possible that there is a conflicting condition or inaccessible accessory. Checking variables in the Shortcut portions is also helpful as some types are not accepted by IF statements for example.
3. Reboot all HomeKit Hubs. My suggestion is to power them down 2 minutes if you are not sure then turn them on (usually you get a "no home hubs responding notification")
4. Reboot the wireless network and Hubs (one more time). This is pretty self explanatory. 2 minutes for all of them is my suggestion :)
