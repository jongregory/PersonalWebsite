---
title: "Consuming RSS Feeds in C#"
date: 2017-07-14T14:10:02Z
draft: false
tags: ["tips","cs"]
---

I have never consumed an RSS feed in code before and assumed it would be a bespoke process, but the **System.ServiceModel.Syndication **library has a everything you need in a few lines of code;

{{< highlight csharp "linenos=table" >}}
 string url = "http://blog.jongregory.net/syndication.axd";
            XmlReader reader = XmlReader.Create(url);
            SyndicationFeed feed = SyndicationFeed.Load(reader);
            reader.Close();
            foreach (SyndicationItem item in feed.Items)
            {
                Console.WriteLine("Title {0}",item.Title.Text);
                var summary = HttpUtility.UrlDecode(item.Summary.Text);
                Console.ForegroundColor = ConsoleColor.White;
                Console.WriteLine("Summary {0}", summary);
             }
 {{< / highlight >}}  

 Quick and simple can also be used to create RSS feeds.

