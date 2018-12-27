---
title: "Sql Server Management Studio Freezing On Start Up"
date: 2016-04-06T09:05:41Z
draft: false
tags: ["tips","sql server"]
---

For a few weeks I had a really annoying issue with Sql Server Management Studio freezing on start up, this happened a few times at crucial moments and caused me delays.

I tried several re-installs and repairs and even the 2016 RC version, but it would just keep happening randomly.

Until I found his blog and following the second option to clear the profile information.

[https://blogs.msdn.microsoft.com/andreasderuiter/2012/12/18/ssms-2012-freezes-when-being-launched/](https://blogs.msdn.microsoft.com/andreasderuiter/2012/12/18/ssms-2012-freezes-when-being-launched/)

An bingo it never happened again, turns out the profile data is not removed on a uninstall.