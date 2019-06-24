---
title: "Automation With Ifttt Logicapps"
date: 2019-06-24T11:37:16+01:00
draft: true
tags: [azure,ifttt,automation]
---

Need - Send SMS at certain times when entering and exiting a location- free

IFTT - can have an app on phone for location tracking - but only one condition which is the location, cannot restrict by certain times

Logic Apps - Can have complex logic statements, but not track location

Solution;

1 - IFTTT applets for entering and exiting a location - call a web hook which is logic app
2 - Logic app checks time and if with the range calls a IFTTT webhook
3 - IFTTT web hook pushes to the IFTTT phone app and sends an SMS

Used when leaving and arriving at work to notify spouse, will only activate at start and end of day to reduce false notifications for lunch time work etc.
