---
layout: default
title: "Temperature Automations"
permalink: /LetsBuildAdvanced/tempAutomations/
parent: "Let's Build! (Advanced)"
nav_order: 10
---
# Temperature Automations
### Rising, or with EACH change
---

There are 2 kinds of Temperature automations that have different reasons for being.

1. Rising and falling
2. with EACH change

Here we will cover the uses for each and how to build them.

## Rising and falling

![jtd](docs/LetsReallyBuild/Images/RiseFallTempStock.png)

this image contains the trigger. for both Rising AND falling, it is only executed ONCE when it runs through the threshold. so, in this example if the temperature drops below 62 degrees, it will then execute the automation until the temperature rises ABOVE 62, then back down below 62 again. it will not execute with each change or each change BELOW or AT 62 degrees.

---

## With EACH change

first, you will need to make this automation in one of the [third party HomeKit Apps](https://parkthecar.github.io/getting-started/homekit-apps/). So grab one if you don't have one! In this example, I will use Controller for HomeKit.

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsBuild/Images/RiseFallTempStock.png?raw=true)

This kind of automation will execute with EACH change. So to make sense of it, we need to filter the results. We have 2 methods. We could add a condition here and make a simple action. This will mean we may have to make multiple automations for each result. The benefit here being you can back up the automations. the Latter, we could save this without changing anything and open it in the stock Home App and convert it to shortcut. we could also do a mix of the two to speed it up. but for now, we will keep it simple. Just know that shortcuts in HomeKit DO pull conditions created in third party apps (even if they don't show correctly)

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsBuild/Images/ControllerTempAutomation.png?raw=true)

If we pump it into a shortcut, we can then create all sorts of logic. From `REPEAT` actions, to `IF` statements. we can even add additional things like API calls or call upon the weather... Or in my case turn on my AdGuard Home server for some reason.

![jtd](https://github.com/PaRkThEcAr/PaRkThEcAr.github.io/blob/main/docs/LetsBuild/Images/TemperatureConvertedShortcut.png?raw=true)
