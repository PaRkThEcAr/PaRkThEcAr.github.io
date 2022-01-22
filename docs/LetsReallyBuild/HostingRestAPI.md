---
layout: default
title: "Hosting Your Own REST API Using Docker"
permalink: /LetsBuildAdvanced/HostingRestAPI/
parent: "Let's Build! (Advanced)"
nav_order: 8
---
## Okay, so lets go about hosting this and using it.
---

JPrerequisites

my most recent implimentation is done using Docker. if you dont have it installed, you can do so here :) macOS and Windows Users need Docker Desktop which can be found on [their site.](https://docs.docker.com/engine/install/)

With that, you now need to make a db.json file in your user/home directory. You can use [jsonlint](https://jsonlint.com) to verify it. But there are a few keys you need to have. Here is an example of what i use. (Not the full thing, but just a taste :)

```{
  "Roomba": [
    {
      "lastRan": "Jan 20, 2021 at 12:06 PM",
      "lastFinish": "Jan 20, 2021 at 12:39 PM",
      "id": 1,
      "running": false
    }
  ],
  "bednight": [
    {
      "id": 1,
      "lastRan": "Jan 19, 2021 at 8:08 PM",
      "morningLock": false
    }
  ]
}
```

Here are 2 Arrays that i use. One contains information on when my Roomba was last ran, when it last completed, and IF it is running. Every Array needs an “Id” key. This key is used in a PATCH call you will see in a minute. This will be our example.

you can then build your docker container with this command. we are using the williamyeah/json-server container as it deploys quickly. we will also run this detached so we dont have to keep the command running.

```docker -d run  \
      -p 3000:3000  -v `pwd`:/data  \
      williamyeh/json-server        \
      --watch db.json            \
      --restart-unless-stopped
```

This will start the service and pull your database. If you ever make a change with this outside of API calls, you will need to stop the script, and reload it.
It will then pull up a few examples of API calls. For our Roomba, our url will be as such

- For GET requests, it will be http://MY.IP.HERE.PLS:3000/Roomba
- For PATCH http://MY.IP.HERE.PLS:3000/Roomba/1

Now for the PATCH call, you need to specify the “id” key in the URL which in this case is 1. if you want to play around with DELETE or POST, you can check the NPM page as it has lots of documentation.

With this up and going, lets get to automating for our Roomba! Each of these automations will be shared as a “shortcuts” link. To make these into HomeKit actions, you will need to make HomeKit advanced automations and add the actions (sorry). [This shortcut](https://www.icloud.com/shortcuts/66300ea4cae9441cb2b768cddc5e783c) contains several example calls you can make. You can use one action for each automation.

Now, when the Roomba turns on, it registers the date it ran, as well as its Running Status as being TRUE. When off, it will register the date it finished, as well as setting the running status to FALSE. These Booleans can be used for a myriad of stuff not exclusive to HomeKit. But it can give you more to work with. It is important however to note that we are using a PATCH request so we don't create duplicate entries under new ID’s.
Now that we have a system for recording when the Roomba ran, what can we use it for? For me, i want the Roomba to turn on when both my wife and i leave, but i also want it to go off at noon. but not BOTH in a single day. So we can use the date it last ran or completed to tell both automations to skip if the Roomba ran in the last 12 hours! [Here is an example of one such automation.](https://www.icloud.com/shortcuts/ca55b0652bf84073a5eed0d1c1bc1998)

This is a simple example you can apply to a leave, and a timed based automation. But effectively, the technique is the same. You can even work harder to make it more fancy. In my own personal ones, I use Pushcut notifications (which are put in as API calls) to inform me if the Roomba was unable to start or what have you.

hat’s it! That’s all you need to do! You can get real fancy with this if you want too! Allowing yourself to create “Global Variables” or make shortcuts that can call that data [like this one!](https://www.icloud.com/shortcuts/fca4f5d419494df7bf41bf476ba43349)

Or you can do one like my “bednight” key. Which allows me to execute a scene once per day when I walk in the bedroom.
