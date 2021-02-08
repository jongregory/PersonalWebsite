---
title: "Automation With Ifttt Logicapps"
date: 2019-04-24T11:37:16+01:00
tags: [azure,ifttt,automation]
---

Following on from last months work wit Azure Functions and Azure Logic Apps I made a little side project to help solve a commuting problem.

When I cycling to and from work I had been asked to text home to say I had arrived safely and when I was setting off, I usually forgot and had to stop on the journey and dig the phone out from the bottom of the cycling rucksack. This was a great candidate for automation, but I didn't want to have to pay each time

[IFTTT](https://ifttt.com/) is a free tool for connecting apps and devices with simple work flows. The android application can use location tracking and a [Geo-Fence](https://ifttt.com/location) to trigger an event when I entered an area. 

The restriction however is that the only one condition can be set for the 'IF' part of IFTTT, so every time I entered the geofence it could trigger an event, so if I left for lunch the leaving office sms would get sent. 

Azure Logic Apps can have complex logic, but they cannot track my location so combining both technolgies together into three steps would provide the solution.

**Solution Overview**

![Example image](/images/IFTTT-Logic-Apps.png) 

**Solution Steps**

1. IFTTT applets set up for entering and exiting a location/geofence, when triggered makes a http call to a web hook which is Azure Logic App

1. When call the Azure Logic App checks timeof the call and if it within the usual commuting time range it calls another IFTTT webhook
 
1. The IFTTT web hook pushes a notification to the IFTTT phone app and sends an SMS from my phone.

The SMS could just as easily be triggered from the cloud, but using the IFTTT app on the phone means I have the message history and don't incur the charge of a SMS service.

The time range is set to my usual start and finsh time, so it cannot deal with exceptional circumstances like half day holidays etc, but its fine for 90% of the time and is just meant to be a bit of fun!
