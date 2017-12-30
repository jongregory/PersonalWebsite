---
title: "Getting Started with Xamarin - Setup"
date: 2016-05-02T21:05:02Z
draft: false
tags: ["xamarin","cs"]
---

I wanted to learn [Xamarin](https://www.xamarin.com/) for a while and with recent purchase by Microsoft and inclusion in Visual Studio now was the time.

This blog is not meant to reinvent the wheel and there are many excellent guides out there on how to get started. This is my experience following the [MSDN setup documentation](https://msdn.microsoft.com/en-us/library/mt613162.aspx)  and the tweaks I had to make. As much of personal record as a blog post.

**Issues I had along the way following the setup; **

Has errors  with the Andriod SDK after the initial install trying to create a new Android app, followed this blog to resolve. Had to launch the SDK Manager after install and run  to install the full SDK components

[http://stackoverflow.com/questions/32618851/unable-to-create-new-blank-app-android-in-visual-studio-2015](http://stackoverflow.com/questions/32618851/unable-to-create-new-blank-app-android-in-visual-studio-2015)

Needed to enable Hyper-V on Windows 10, it was showing as enabled but it wouldn''t work on my PC . Followed the blog post below and had to disable and reenable through windows features which meant a few restarts!

[https://msdn.microsoft.com/en-us/virtualization/hyperv\_on\_windows/quick\_start/walkthrough\_install](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/quick_start/walkthrough_install)

To check everything had installed properly I ran through these verification steps which really helped, I found I needed to install the Windows Phone Emulator and when connecting to the Mac had to set remote access to all users to get working

[https://msdn.microsoft.com/en-us/library/mt488769.aspx](https://msdn.microsoft.com/en-us/library/mt488769.aspx)

Hurrah all the projects all run!

Next step is to create a simple app with shared code approach  [https://msdn.microsoft.com/en-us/library/dn879698.aspx](https://msdn.microsoft.com/en-us/library/dn879698.aspx)