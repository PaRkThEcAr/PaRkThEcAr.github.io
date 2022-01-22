---
layout: default
title: "Conditioning"
permalink: /LetsBuild/Conditioning/
parent: "Let's Build! (The Basics)"
nav_order: 8
---
## Not just for Pavlov's dogs.
---

Conditions in the Stock Home app really amount to 2 areas.

1. people presence
2. time of day/day of week

the second one is simple. you can set the automation to only occur after 3, or on a Wednesday-Friday or both. you can mix and match however you please :) it gets nuttier when we deal with people presence. People presence depends on WHO makes the automation (needs to be an admin in specific cases) let's work with an example home.

USERS:
PaRkThEcAr
Bo
Bun
Pepper

Here is our set of users. you can condition it like this:

Off (ignores presence and is default)
When SOMEBODY IS HOME (when any of these 4 users are home)
When NOBODY IS HOME (when none of those users are home)
when I am not home (when I, PaRkThEcAr am not home)
When I am home (when I, PaRkThEcAr am home)

These last 2 are interesting as they can only happen and be specified on the user's device (from their Apple ID) for example, if I wanted to make an automation for when only Pepper was home, i would need to make it from his profile and account. its silly, but it can be done.
