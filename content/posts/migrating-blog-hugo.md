---
title: "Migrating my Blog to Hugo & Netlify"
date: 2018-01-08T19:44:55Z
draft: false
---

New Year, New Blog! I have never been very happy with my blog, it was very heavy weight a full ASP.Net based tool called BlogEngine.Net and a SQL Server database. There is nothing wrong with either of these but I didn't use most of the features.

They cost a lot to run, I was hosting on Azure and had to use a Standard Web App to be able to use a custom domain, the blog posts were stored as HTML in the database and where not very portable.

I wanted a simple site where I could just put up one or two posts a month, that would look clean and simple, and more importantly be free to run and easy to maintain.

A couple of blog posts spurred me into action [https://dev.to/chinjon/de-bloating-my-developer-portfolio](https://dev.to/chinjon/de-bloating-my-developer-portfolio) had a great clear design, but I didn't want to write my own site as I don't have time. 

The comments section in this post [https://dev.to/chinjon/de-bloating-my-developer-portfolio](https://dev.to/chinjon/de-bloating-my-developer-portfolio) on [https://dev.to/](https://dev.to/) pointed me in the direction of a static site generator.

### Site

For the site I looked at [https://gohugo.io/](https://gohugo.io/) and [https://jekyllrb.com/](https://jekyllrb.com/). I went with HUGO as it has a great choice of [themes](https://themes.gohugo.io/) and the documentation was easy to follow. Content is created in markdown and HUGO generates the pages. After trying a few out I went with the [minimal theme](https://themes.gohugo.io/minimal/). Its easy to change the theme later and they are installed as git submodules.

The Hugo sites are driven by a [configuration file](https://gohugo.io/getting-started/configuration/), I got a bit lost in the docs here but using a completed file from one of the theme sample sites got me back on track.

There are lots of options for [content management](https://gohugo.io/content-management/) and [template management](https://gohugo.io/templates/) for future improvements. I haven't strayed too far of the provided theme yet.

The first change I did make was adding a specific css for [syntax highlighting](https://themes.gohugo.io/minimal/) which was easy to do, but I had to specify it in the config file. The syntax highlighting does not show up in a markdown editor but looks great on the screen.


The second was to set up [taxonomies](https://gohugo.io/content-management/taxonomies/) for post tags so I can organise and navigate.

Creating a new post is done from the command line;

{{< highlight powershell >}}

hugo new SamplePost.md

{{< / highlight >}}

To migrate my existing blog I used an online HTML to markdown editor which took about an hour.

The blog is stored in [GitHub](https://github.com/jongregory/PersonalWebsite) so I have persistance and can edit on any machine.

A really neat feature of Hugo is the [hugo](https://gohugo.io/commands/hugo/) command that lets you run the site locally and view draft posts, this also updates the site on file save allowing changes to previewed immediately.

{{< highlight powershell >}}

hugo server -D

{{< / highlight >}}

### Hosting

The hosting now uses [Netlify](https://www.netlify.com/) which has been fantastic to setup, HUGO docs describe [deployment and hosting setup](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/). This only takes a few clicks and can be triggered from GitHub commits, so I simply push to master and the site is built and deployed.

Netlify also provide [custom domain support](https://www.netlify.com/docs/custom-domains/) and [HTTPS Support via Lets Encrypt](https://www.netlify.com/docs/ssl/). You can choose [managed DNS](https://www.netlify.com/docs/dns/) so you url routes directly to Netlify servers for faster performance.

### Summary

Both Hugo and Netlify were very easy to setup, my page is not controlled from the command line and GitHub which as a developer is my comfort zone. 

Netlify deployments were easy to setup and reliable. The whole set up is much lighter and easier to use, there is not maintance or upgrades to do and I can quickly change the styles.

I am really happy with the look of the site now and can focus on creating content in markdown and not the infrastructure. 
