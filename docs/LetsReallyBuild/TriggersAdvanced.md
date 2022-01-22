---
layout: default
title: "Triggers (Advanced)"
permalink: /LetsBuildAdvanced/TriggersAdvanced/
parent: "Let's Build! (Advanced)"
nav_order: 6
---
# Triggers (Advanced)
### NOW I AM TRIGGERED (like a sensor ;) )
---


Great! so you are here and you wanna know the deeper side of HomeKit. if you wanna get anywhere, I would first start by grabbing any one of the third party HomeKit apps listed in the [HomeKit Apps Section](https://parkthecar.github.io/getting-started/homekit-apps/). for our cases here, I am going to use Controller for HomeKit as it has a native macOS app.

in the previous section talking on [triggers](https://parkthecar.github.io/LetsBuild/BasicsTriggers/), I made the allusion that there are more types of triggers rather than off/false on/true. and that is absolutely the case. and while a few of these are exposed, you have a LOT to work with for each accessory type. because there are SO many, I am going to stick to a few types of accessories so as to keep it brief. it is important to check all the types of triggers in these apps and what conditioning is allowed. lets use a color light bulb as our first example a Nano Leaf Canvas panel group.

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/AdvancedTriggers1.png?raw=true)

in Controller, you can see there are LOTS of different options when we chose "event based trigger" all of these are technically actionable. a lot of the common ones people use are Brightness, Hue, Saturation, Color, and of course Power State. for example...

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/AdvancedTriggers2.png?raw=true)

we can here do it based on Hue. we can then have a few options. Each Value Change, Value Is, Value is Greater than or equal too, Value is between, Value is less than or equal too. In this case, i selected Value is which looks for a SPECIFIC value of 69 (nice). You could also simply set a range using Between or Greater than. how you wanna do it is specific to the use case. The elephant in the room however is the Each Value Change type. this will run the automation for EACH change of this quality. so if the hue changed to 1, to 2, then 3, you would have an execution for each of those.  this is particularly useful for automations that are converted to shortcut/advanced automation as setting these triggers liek this allows us to parse the data later in action :)

a hidden magical thing however, is that you can set multiple triggers :) as seen here.

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsReallyBuild/Images/AdvancedTriggers3.png?raw=true)

this one will execute when ONE of these two actions happens. so if you have 2 senarios you want an automation to run in, you can do this. bare these in mind, as we can use all this stuff for automations.

just be careful not to step on other stuff :)
