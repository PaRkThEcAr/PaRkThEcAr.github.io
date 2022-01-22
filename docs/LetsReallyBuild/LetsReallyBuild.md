---
layout: default
title: "Let's REALLY Build"
permalink: /LetsBuildAdvanced/LetsReallyBuild/
parent: "Let's Build! (Advanced)"
nav_order: 5
---
# Let's Really Build!
### Okay, okay, we get it. You aren't basic. You are advanced. Here is the stuff for you!
---

Now that we got some building blocks, we need to go over a few techniques and theories when it comes to HomeKit automating.

for those who aren unfamiliar, HomeKit does not expose the full API to us users in the Home app. there are far more things we can do in third party apps ([seen here in HomeKit Apps](https://parkthecar.github.io/getting-started/homekit-apps/)) than are exposed such as multiple triggers, multiple conditions, and alternate triggers. in this section we will talk about how they work on top of covering some other technologies/bridges such as [Homebridge](https://homebridge.io), [Puschut Automation Server](https://www.pushcut.io/index.html), or the [json-server](https://www.npmjs.com/package/json-server) self hosted REST API. some of these things are intimidating and some are VERY simple. lets go over a few of the COMMON technologies. lets start with Homebridge.

## Homebridge

Homebridge is a very simple install. [If we go to their github wiki](https://github.com/homebridge/homebridge/wiki), you can see there are MANY ways and systems to install it on. chances are, you already have a computer ready to go! but for those looking to build from the ground up, a Raspberry Pi 4 is a cheap and easy way to go that can have it installed 3 of the ways listed here (docker, Rasbian/linux installs, or the official image). 2 things are needed though.

1. The machine needs to be always online and on network (no laptops that leave with you)
2. It needs to have enough power to run it. This isn't a high bar as you can install it on a Pi Zero. Just bare in mind that if you are driving cameras, a Pi Zero isnt going to cut it for more than 2.

### The HOOBS problem
It is heavily discouraged to buy a HOOBS kit if you want to build Homebridge. Homebridge's official raspberry pi image is more maintained and would actually be cheaper to build. at the end of the day, its about as easy to run.

### Docker
Docker is installable on ALL of these OS's (macOS, Windows, Linux) but Homebridge specifically cant be done with docker using macOS or Windows due to a broken/unsupported argument needed to make the pairing work. a docker install is totally worth it for other stuff on these platforms, but not for Homebridge (unless using linux).

### macOS
A macOS is easy to deploy and very cheap as MOST people have a Mac on network all the time. [The Official Homebridge documentation](https://github.com/homebridge/homebridge/wiki/Install-Homebridge-on-macOS) has install instructions that I feel are very easy as you can copy and paste most terminal commands, and download packages by hand if needed. Just assign your mac a Static Lease on the network and leave it on and awake. Simple enough!

WHAT DO THO?

Simple, it can be used to bridge unsupported accessories (famously, TP-Link Kasa Plugs) or create virtual accessories (dummy switches, Roomba's, Virtual Occupancy Sensors, etc) giving you more room to expand on HomeKit beyond native accessories. it can also be our gateway to creating more sophisticated automations in HomeKit. to install it, follow the directions on their GitHub :) and if you have troubles, you can reach out to their subreddit, discord, or Github issues tab. It's pretty easy these days though. so I wouldn't be too worried it will fail.
