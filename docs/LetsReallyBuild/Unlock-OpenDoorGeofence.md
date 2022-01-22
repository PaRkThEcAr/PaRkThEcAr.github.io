---
layout: default
title: "Unlock/Open A Door With Geofenced Automation"
permalink: /LetsBuildAdvanced/Unlock-OpenDoorGeofence/
parent: "Let's Build! (Advanced)"
nav_order: 11
---
# Unlock/Open A Door With Geofenced Automation
### Granting Access to your home in a (risky) way
---

## DISCLAIMER!!!
You SHOULD NEVER rely on an automation to secure your doors. Computers are imperfect devices made by imperfect Ape beings who's fur fell off one day and smash sticks together to burn stuff (the damn pyromaniacs)! As such while you CAN do this, do so at your own risk. automatically opening/unlocking or closing a door can grant access to someone inadvertently or damage things.
---

## Automating a Garage Door With a Switch

Okay, so you want to have a door unlock/open when you arrive home? great! Let's explain why you cant by default. In simple terms, it's a restriction put in by our glorious overlord Tim. all security devices have this restriction from Doors and locks, to security systems. but these are the only restrictions and they CAN be worked around. We will need a few things.

1. An on network install of [Homebridge](https://homebridge.io)
2. A [dummy switch plugin](https://github.com/nfarina/homebridge-dummy). there are many, but this one is easy. you can take your pick!
3. A secure device we wish to control (in our example we will do a garage door).

Homebridge is optional here by the way. any accessory you have lying around can be a trigger for it. this is just a good way to free up a smart plug if you have the means to build the server. but if you are unsure how you will like this, you could just do it to anything else you have and build the install of Homebridge later.

This plugin is rather easy to work with. you can make the dummy stateful should you want, but I would recommend stateless with a 10-30 second toggle time max.

once you have your switch, you just need to build a basic accessory automation like this!

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsBuild/Images/GarageDoorAutomation.png?raw=true)

## Skip Siri Authenticating using this technique

But let's take this one step further. What if you wanted to open the garage door using Siri without authenticating on an iPhone? all we need to do is add it to a scene and name it something you will say like "Open the Pod Bay Doors" or in my case, "Open the Garage Door". Just be advised that by doing this, you could open yourself up to issues such as unwanted entry. So if you would rather NOT open yourself up to this, don't.

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsBuild/Images/NoAuthDoor.png?raw=true)
