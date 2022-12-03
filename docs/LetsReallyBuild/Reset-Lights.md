---
layout: default
title: "Creating a Light Reset Automation"
permalink: /LetsBuildAdvanced/Reset-Lights/
parent: "Let's Build! (Advanced)"
nav_order: 12
---
# Creating a Light Reset Automation
### Resetting your lights based on Occupancy.
---

Many of us have fun color scenes. but sometimes, we just want everything to switch back to white in a pinch. so here is how you can achieve it too.
first, I need to keep 2 things in mind as we make this.

This needs to be accessible to EVERYONE in my home. i have a mixed mobile device home. so making an iOS shortcut to do this isn't practical, as not everyone has an iPhone. so not only does it need to work with my HomePods OOB, but it also needs to be useful with other stuff like my Dimmer Switch (pressing the top button if lights are on)

This needs to be reliable and responsive :) so making a scene with a billion lights in it might take a while to run. and even then, it may turn on lights in rooms i don't want it too. so we need to automatically determine if the room has people or not.

We need a [Homebridge](https://homebridge.io) instillation. we need 2 plugins, Homebridge-Dummy and Homebridge-Occpancy-Delay

With Homebridge Dummy, we need to make 1 virtual switch. Mine is set to auto off after 30 seconds :) but you could just set it to stateless if you wanted.
With Homebridge Occupancy Delay, we need to make a virtual occupancy sensor for EACH room. then, we need to rig the sensor dummy switch to turn on with motion, and off with no motion. how long the sensor stays active with no motion is entirely up to you :) mine turn off after about 300 seconds of no activity in a room.

Next, we create a scene. just add the switch and make sure its on :)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/LightResetSceneComp.png?raw=true)

now, we automate. first, I tend to like making this automation Multi Threaded. this way, if one room should fail due to a disconnected device, the others wont fail :)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/LightResetBuild.jpg?raw=true)

then we make an advanced automation (or HomeKit Shortcut) that will look like the image included. we create an IF statement to determine if the room has occupancy. then, IF there is, we set the lights to our default (in my case, its Adaptive lighting). if there is no occupancy, we turn the lights off. now, in the image i have 2 steps. i first set the lights to adaptive, then turn it off due to a glitch introduced in iOS 14.5 where lights when turned off will turn back to the color when you try to set them to adaptive. very odd, but hey, its a simple work around :)

And there you have it! simple, elegant, and useful! the end result is a scene that can be tapped on in HomeKit, invoked with Siri, or assigned to any HomeKit button. you can even use it in automatons. for example, when my wife arrives home, it will change the lights to Royal Blue for 10 seconds then reset the lights :) (if i am not already running a color scene. but more on that in another post).
