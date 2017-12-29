---
title: "Session State being lost in Web Farm"
date: 2016-06-21T16:06:44Z
draft: true
---

Investigating and issue with session data being lost on a load balance ASP.Net website the other day, users we''re losing items from a basket when bouncing between servers.

These issues have always been difficult to investigate but it turned out that when setting up the web servers there was multiple sites in IIS. These has been created in different order so had ended up with different site ids. A simple error but the symptoms were dramatic for users and difficult to recreate and trace.

This article details the issues [https://support.microsoft.com/en-us/kb/325056](https://support.microsoft.com/en-us/kb/325056) , although I did not have to use the described resolution.

I found that I could just change the site id through IIS, if a another site had the required id I renamed that until both web servers were is sync.

In IIS select the site and advanced settings; the edit the id to the required value

![](http://blogjongregory.blob.core.windows.net/blogimages/SessionsMissing/IISSiteId.PNG)