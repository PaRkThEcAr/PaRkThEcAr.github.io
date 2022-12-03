---
layout: default
title: "Custom Ciradian Rhythm for your home"
permalink: /LetsBuildAdvanced/CustomCircadianRhythm/
parent: "Let's Build! (Advanced)"
nav_order: 14
---
# Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect 
---

`TLDR: skip to III. Your home will redshift its light, taking in account when sunset starts.`

## I. Defintion

In biology, the circadian rhythm is defined as “the daily rhythmic activity cycle based on 24-hour intervals”. This rhythm is highly influenced by the immediate environment more specifically natural light. While it is suspected that reducing blue light from displays (artificial light) would help the brain disengage with daytime processes that keep it awake, a small study (n=167) by New-York’s Brigham Young University seems to show the iPhone’s NightShift feature (released in 2016) actually has little to no impact. It’s rather the active use of the smartphone that disrupt the sleeping rhythms. Worse: a study by the University of Manchester demonstrated that NightShift disturbed the internal clock of mice. Said to be applicable to humans, it would infer a decrease in quality/benefits of sleep.
Anyway, the difference with what we’re doing here is that we’re dealing with ambient lighting: even if artificial, we’re not staring at bulbs like we would a display. A softer ambiance helps putting us asleep.
For context, I’ve had my own automation from before Apple announced Adaptive Lighting for manufacturers who choose to support it. As everything Apple, the “Works with Apple Home” label equates more expensive for consumers but also for the manufacturer’s with very little incentive (more frameworks to implement, dependancies and little reward even before you being to turn a profit).
Anyway let’s proceed.

## II. Benefits
#### … of having your own automation are diverse:

- Universal compatibility*:
works with your existing installation
    - If you don’t have smart bulbs, spend that $ on the cheapest ones.
    - If some bulbs are wired to the same switch, replace the switch itself with the cheapest one (The bulbs will become as capable as the switch, and switches don’t manage color, only On/off and/or dim)
    - Or replace the electrical module behind the switch; again with the cheapest one. Same warning as above.
    - Light strips under the desk, bedside lamps, anything you can think of

Provided you own corresponding hubs if it’s not HomeKit compatible. More on that at the very end.

- Costs efficiency: Everything mentioned above.
    - Because universal, no extra $ to spend on extra equipment
    - Saving on bill as opposed to having all the lights turned on 100% til you go to sleep
    - If you do need extra equipment, purchase the cheapest, it’ll work. Lots of options cheaper than a single Hue bulb.

- Everyday life benefits
    - You won't get blinded by the kitchen lights if you go for that nightly glass of milk or to the bathroom
    - You won’t have to worry about the lights “waking you up so much that you can’t get back to sleep again”
    - You get the signal it’s getting late, time to wind-down on work and call it a night
    - Personally, I get the feel that my home is more organic. But that’s me living my sci-fi dreams where Siri is actually smart haha.

- Control
    - Apple being Apple, their solution must give very little control. Your own automation = your own triggers, conditions, intensity %s, etc

2 examples of benefits you get:

1. went an extra step to put a "Vibration sensor" (Aqara) in my couch so when I sit, it turns on the Philips TV Ambilight to an x% accordingly to how far into the night. Should I go to away, it turns off but keeps the TV on as in “I’m not actively watching so take the ambiance away but keep the movie going”
2. The flat I recently moved into had G10 to the ceiling that couldn’t be reached. Instead, I purchased a Smart Electrical box for $40, giving me control over them and now, my 8x G10s are included in my home’s circadian rhythm and can dim as opposed to the initial dumb On/Off switch.
For reference: 1 color hue + the bridge bridge = $44 + $44 as of today on Amazon.
Ok, I hope by now, you are convinced. Let’s get a move on!


## III. The How-To: A. Intent, B. Scenes, C. Hourly Automations, D. Motion-Based Automations

A. Intent
Before starting any big automation project, given how impractical HomeKit is to work with, I recommend writing down a clear intent as to what you are trying to achieve. Give it some thoughts so that when it comes down to complex equations of i.e. several if statements, naming variables, etc. you keep a clear mind and can easily remind yourself your objective and context. (It’s actually from my professional expertise). My intent behind this was the following:
```“When night comes, I want my lights to dim and redshift as it goes so that I can go improve my quality of sleep.”```
From there, details emerged organically:
```“I want lights to turn on at Sunset”
“I am in bed at midnight the latest”
“So I want lights to redshift through the night and turn off at midnight”
“For the room that I currently occupy”```
Sparing you the details, the challenge resides in the fact that Sunset moves with seasons. To factor that in, I divided the night into 5 periods arbitrarily and I created a scene for each (Decide your own but keep in mind: the more periods, the better gradience to the redshifting which is great but the lengthier the automation to write). Here go mine:

- Sunset: Sunset
- Evening: 8pm
- Late Evening: 9.45pm
- Night: 10.45pm
- Late Night: 11.30pm
- Good Night: Midnight

Now 2 types of automation will help articulate these periods around Sunset: Hourly and Motion based. Each will fire according to what Period is current.
- Hourly because when its time comes, the current period's scene turns on
- Motion because, say you come back home after work by 10.34pm, or you walked in a room where the lights were off; you want lights to turn on according to said current period

B. Scenes
Take the time you need to make your own periods and matching scenes. Like this, you won’t have to manipulate each bulb in the automation which makes it easier to write AND you can just ask Siri for the scene to set up an ambiance. As for an example, mines are:
- Sunset: not all but some bulbs, yellow, 80% intensity
- Evening: All, 100%
- Late Evening: All, Orange or redshifted a little, 80%
- Night: not all but some bulbs, 50%
- Late Night: Just one bulb, completely redshifted, 10%
- Good Night: shuts off everything
For those like me who live alone and/or who want to save on bill, make sure the automations that turn lights off behind you as you walk into another room or leave the home entirely are SEPARATE from what we're doing here. That way, if you have guests, you'll just need to deactivate the separated ones. Guests will walk around triggering Scenes without turning off lights on those behind. My gf hates it when the Apple TV pauses the movie and the lights go off because I walked into the bathroom :D

C. Hourly Automations

Fairly straightforward:

For Sunset:
- When: Sunset, repeat everyday, when I'm home
- Select Accessories and Scenes: Sunset
- Done

For Evening we need to adjust for a moving sunset (where there’s a *, repeat and adapt the following for Late Evening, Night, Late Night. NOT Good Night)
- When: *8pm, repeat everyday, when I'm home
- Select Accessories and Scenes: (scroll all the way down and tap “Convert into Shortcut”)
- Fetch Time of Sunset at your home address
- If Time of Sunset before *8pm
    - Then Turn on Sunset
    - Otherwise // Nothing: it's still daylight

For Good Night:
- When: Time of Day 12:00 AM, repeat everyday
- Select Accessories and Scenes: Good Night

Let us expand on the Evening one. I’ll write down the automation in layman's term for you:

Select Accessories and Scenes: (scroll all the way down and tap “Convert into Shortcut”)

- Get current Weather condition at [Home Address] // NOT current location because if your phone runs out of battery at work, work will be your last known location
- Get [Detail] from Weather Conditions // Make sure you tap on “Detail” and select Sunset
Format Sunset Time // Open it via the little arrow, tap “Short” in Date Format, select “Custom”. Just below, in “Format String”, erase everything and replace it by “Hmm”. Finally close it by tapping the little arrow
- Get numbers from Formatted Date
- Set variable [TimeSunset] to Numbers // Name your variable

The reason for formatting dates into military time is: when first created these automation years ago, Homekit was dodgy and still is and since dates are coming from online sources, I'd know the problem wouldn't be with the If statement; one less thing troubleshoot. Also, If statements + date force you to choose a calendar day which is irrelevant to us since we want the automation to work every day.
Military time means 9.43am = 943; noon = 1200; 10.23pm = 2223 and Midnight = 12am = 0.
Here are the screenshots:
![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img1?raw=true)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img2?raw=true)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img3?raw=true)

r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
Triggers at 8am if I'm home and run the shortcuts


r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
1. Fetch weather data your home address, (not your current location), 2. Collect Sunset Time specifically. 3. Formats Sunset Time to military, 4 retrieve string as numbers to pass into the var


r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
pass into var, compare var to time cue.


That'll do it for Evening. recreate on but for Late Evening, Night and Late Night. with their time cues (2130, 2245 and 2330)
Let’s review:
If SunsetTime is before Evening time cue, then all good, Sunset Scene will turn on at Sunset, followed by Evening Scene at 8pm and so forth. In Summer, sunset will get past 8pm AND 9.30pm. so Evening won't turn on at 8pm. Sunset Time will still turn on when it happens, until the next period which will be Late Evening.
Ok great, it all articulate around sunset. We have done the first part.
D. Motion-Based Automations
As we said, these are for situations when lights are off and should turn on accordingly to the current period of the night because you walked in. This also should account for Sunset time moving past our time cues. This should trigger only if the Sunset Time is in the past, then check what period is current and turn on the matching Scene. Without HomeKit formatting, that gives us this:
If TimeNow between TimeSunset and before 7.59pm // If the current time is after sunset started but before evening
Then current period is Sunset // so turn on Sunset Scene
If (…) between TimeSunset and before 9.29pm // (…) but before Late Evening
Then turn on Evening // you get the idea
(…) but before 2244
Then turn on Late evening
(…) but before 2329
Then turn on Night
(…) but before 2359
Then turn on Late Night
Notice 2 things:
In the time conditions, it's hour minus 1 min because the time cues are already covered by the hourly automations you wrote in the part above so the cues must be excluded here
The period from Midnight to Sunset is not covered: lights won’t turn on. However, you may go for a glass of milk, or to the bathroom and it's too dark in your home. To compensate for that, simply add a condition for that period that if met, turns on a bulb/scene of your choice. Beforehand, fetch the Sunrise Time instead of sunset as follow:
Fetch time of Sunrise at your home address
Format to military time
If TimeNow is between midnight and TimeSunrise, turn on said lamp. // remember Midnight = 12am = 0000 = 0 in military time.
Notice also how Sunrise become the right handle of the time interval in case your unfamiliar with IF+Between
Anyway, screenshots for Motion Triggered automations:

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img4?raw=true)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img5?raw=true)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img6?raw=true)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img7?raw=true)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img8?raw=true)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img9?raw=true)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/Circadian/img10?raw=true)

r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
My own automation is different (see at the very far of the post) but I created one for you Reddit.


r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
Same old: get the Sunset Time at your home address, format it, get the numbers into TimeSunset var


r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
As mentioned before, we also need Current Time, then to format it and get into TimeNow.

r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
Now let's confront TimeNow with TimeSunset and the earliest time cue to determine what period were in. Here we're checking if time now is after TimeSunset but before Evening, in which case, the current period is Sunset. Then we're checking if it's Evening.

r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
and so forth

r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
until 11.59 because midnight is covered by Good Night Time cue.

r/HomeKitAutomation - Circadian rhythm for your home: I. Definition, II Benefits III. How-To (with screenshots) IV. Fancier V. FANCIER! VI. Perfect
Done.

Let's review what we've done:
We created a Scene for each 6 periods.
We created Hourly Automations which adjust to TimeSunset so the system knows wether to turn the lights on or do nothing.
We created Motion-Based Automations that will turn the lights accordingly to the current period and only if past TimeSunset.
The results are:
if Sunset occurs before evening, all we go progress as normal.
If Sunset shifts past 2000 or even later, Sunset Scene still occur when Sunset starts but at the next hourly automation OR if motion is triggered, either way the current period’s Scene will take over. An example of that is: most of summer, Sunset Scene will occur past 9.30pm so if there's motion, it'll trigger Late Evening (skipping Evening since it was until 9.29pm). In winter, Sunset will start a lot sooner into the afternoon and last til 2000 (evening).
Aaaaaand…. You're done =)
Side notes:
You will have to recreate said Scenes for each room you want to have circadian rhythm. say “Bedroom Sunset”, “Bathroom Late Evening”, etc.
As well as the corresponding motion based automation but this time, using that new room's motion sensor and scenes. Tbh, I only need "Late Evening" in the bathroom so I made it easy on my and deleted the other conditions: "if TimeNow is between Sunset and 2359..."
In an ideal world, hourly automation would turn on the lights only in the room you occupy. I'm mostly spending time in my living room so my Hourly applies only there. Unfortunately, there's no "room capacity sensor" for us consumers so If you have lots of rooms, live with a family or else, you may just turn hourly automation for every room. EXCEPT bedrooms because if you go to bed before 2245: the hourly automation will wake you up.
If only there was a way to create ONE shortcut to check time and use its result in HomeKit automation instead of rewriting everything every time... or a way to just duplicate automations... Apple if you’re reading this
## IV. 4 ways to get fancier
A. When you come home at night or go get a nightly drink
Duplicate the hourly automation for Sunset, Evening, Late Evening, Night, Late Night and eventually “Glass of milk bulb” and change the trigger for "when I come home"
B. When you're not home
If you want to emulate human presence to deter robbers, create the same automations but with trigger condition “When I'm not home". Mine turns on only bulb at sunset, close to the window. Changes color next time cue, etc.
C. When you just left home
Same but on my way out: but not hourly, use instead “when I leave”. When you live, it’ll turn on that one bulb, etc.
D. Taking account natural light based on weather conditions
If, during the day, your home gets pretty dark just because it's cloudy, snowy, else, you may create an automation that triggers based on either or any:
Weather condition changes (could be a Homebridge plugin, Home Assistant, whatever float your boat, that regularly checks, or HomeKit weather station and fires if there’s change)
Luminosity (Some sensors report levels of light, in Lux and/or in Light/Dark binary. Homekit is pretty limited in what it wants to read so rather check on them using the Eve's Home App, called Eve)
These would fire a "Cloudy scene" or a Sunset. Well something that isn't like if it was full blown night time. Make sure that it fires only between Sunrise and Sunset which is, fortunately, HomeKit native
Then again, you'll have to write down motion triggered versions of them in case you come back home while cloudy.
E. Waking up in winter
In winter, you may wake up for work while it still night time. At this point, the "nightly glass of milk scene" isn’t what you need. Instead, create an Early Morning, Late Morning and Sunrise Scenes. Then create only their motion-based matches. Why not the hourly? Because you may choose to keep sleeping. (Or if you have trouble waking up, set the hourly anyway, at your alarm time). (Your phone/iPad also have shortcuts automations that can trigger when you snooze your alarm if you wish to further torture yourself into waking up). Finally, make sure those motion based automations trigger only between Wake alarm time and Sunrise Time. It gets slightly more complex at Sunrise. When a sunrise starts, it's still pretty dark and it lasts around 30min before daylight.
So say Sunrise occurs at 8.30am. an hourly automation will trigger Sunrise Scene at that time. Then any motion between Sunrise Time and Sunrise Time + 30min will trigger Sunrise Scene. Past that, nothing happens. (I just had that idea, I’ll try it for myself!). Fetch Sunrise from Weather Conditions Details at your home's address. Format it to military Hmm, and put the value into TimeSunriseStart and TimeSunriseEnd. Add 30min to the latter (homekit action: Add to var). Then you can work your conditions effectively. (If TimeNow is between TimeSunriseStart and TimeSunriseEnd Then turn on Sunrise Scene).
With all that fancy, you gave your home some swag and you cover I think 99% of use cases… But it can get fancier.
## V. Ultimate Fancy
A. Other kinds of sensors and lights
In my couch cushion, I have a vibration sensor (Aqara) which tells my system that I just sat. My TV has HomeKit compatible lights on its back but I don't want them to turn on during the day nor if I'm not watching TV. So I duplicated the Living Room’s Motion Based Automation, change the trigger to "When motion detected on couch" and unrolls like this: check if TV is ON, then check if Sunset is in the past, and turn on the lights accordingly. Pretty neat.
B. PS5
Thanks to some internet genius, I can ask Siri to turn on my PS5. Then, in HomeKit: When PS5 is turned on, wait 15s (for the Tv to turn on), then check if Sunset is in the past, and turn on Gaming Scene, with intensity according to current period.
C. Apple TV + Apps
Same as PS5 except that customised to the App I choose to ask Siri to open: If I say "hey Siri, open up TV+", it'll blink the lights and fade into Movie Scene. If Netflix, turn the lights red and fade into Movie scene. Prime? blue. Just fun. But those are Shortcuts from the Shortcut App. Not Home App.
D. Other things in the room like a dinner table or an office.
My computer desk is also in the same room. So I put a vibration sensor to the chair so that when I sit, the rest of the room dims whilst the desk lights turns on. you could do this with a well oriented motion sensor too.
E. Coordination between sensors and lights as I walk around.
Any other sensor turns off the desk or TV lights ex: if I go into another room. Or even, if I sit on the couch, it turns off the light at the desk but turns on the TV’s lights, all of which according to the period of night. IF it's day, nothing would've turned on anyway.
F. Fancy Light Switch
Aqara has this fancy Cube which has couple of interesting commands: Shake tap it twice on the table or spin it 90 or 180. I use one next to the TV, shake it to turn on Movie Scene, only if past Sunset. And with certain intensity. (Like I said, Fancy! Not useful). You may otherwise just ask Siri...
G. Fiddle with it
In the future, I’ll install HomeKit capable curtains rails so I can disregard the Sunset sunset part and close them on command in junction with activating Movie scene
But wait… if you didn’t think it could get fancier…

## VI. Give me perfection... I said, PERFECTION!
If we roll back to our first automations, there's one underlying inconvenient at the basis: they rely on Homekit’s ability to fetch data from the web. While it should work fine 99% of the time, the fact that the data isn't local brings risks of unreliability into your ecosystem. in addition to diverse manufacturers, bridges, Homebridge or HomeAssistant installed on a Raspberry, DeConz, etc, with bunch of communication protocols such as Wifi, Zigbee, Bluetooth, Thread, Matter, Ethernet etc.
That extra second in the dark when you walk into the room? That’s why. Prefer local data & wired connections always.
It's a lot. So even before I began with IoTs, I was cautious of getting any extra bridge or stuff. I decided to alleviate my system by design from the ground up: I used ONLY Homekit, Homebridge (on a Raspberry plugged in Ethernet and Phoscon+DeConz into its USB. Phoscon has a Daylight Virtual Sensor which collects data including Day/Night (binary), Time of Sunrise, Time of sunset, etc etc and keeps them local. Deconz adds Zigbee to my ecosystem. All here are the benefits:
Zigbee is Thread + Matter before Thread and Matter:
Self healing
Mesh network,
Low-Power
Low bandwidth
Highest responsiveness
Compatible with a ton of accessories: Philips, sOnOff, Ikea, etc. Saving you a TON of $$$ on extra bridges, no need to occupy extra sockets, no increase in electricity bill and no day-long troubleshooting just because this one bulb doesn’t work. Also, zigbee never ever failed me. I never had to troubleshoot in 4-5 years of homekit.
Since to the Virtual sensor data is local, no dependancy on my network’s or my internet access's performance
In short, I no longer fetch data online. I only check if it's night time, if yes, then I unroll the rest according to time period.
I don’t think it can get any better than fancy and high performing so there you go, everyone. I wish you a good night sleep.
7

Award

Share

Approve

Remove

Spam



Post Insights
Only the author of the post and mods can see this
1.9k
Total Views
90%
Upvote Rate
N/A
Community Karma
10
Total Shares
Comment as PaRkThEcAr1