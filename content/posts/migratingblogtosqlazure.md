---
title: "Migrating Blog to SQL Azure Database"
date: 2016-03-28T16:03:54Z
draft: true
---

This is post is about my experiences migrating my blog to a SQL Azure Database.

When I started with BlogEngine.Net I used the put of the box persistence which is XML file based in the App_Data folder.  

I wanted to use a SQL Azure Database and migrate the data across, I found the blog post below with instructions.

[http://nyveldt.com/blog/page/BlogEngineNET-Provider-Migration](http://nyveldt.com/blog/page/BlogEngineNET-Provider-Migration)

I took the database script from the setup folder in the BlogEngine.NET file system and ran it against the New SQL Azure DB using SQL Server Managment Studio.

This gave me most of what was required but I had to change the **BlogMigration.aspx** page to remove the ''1'' from the master page name;

<%@ Page Language="C#" MasterPageFile="~/admin/admin1.master" AutoEventWireup="true" CodeFile="BlogMigration.aspx.cs" Inherits="admin\_Pages\_BlogMigration" Title="Blog Migration" %>

I still had some compile errors , the following blog post describes the changes required to the **BlogMigration.aspx.cs** code file, and how to set the blog guid id.

  

[http://www.rhizohm.net/irhetoric/post/2014/12/11/BlogEngineNET-Provider-Migration.aspx](http://www.rhizohm.net/irhetoric/post/2014/12/11/BlogEngineNET-Provider-Migration.aspx)

I had to check that the firewall setting were correct for my new SQL Azure DB and that it allowed connections from Azure Web Servers. This post describes how to do that

[https://azure.microsoft.com/en-gb/documentation/articles/sql-database-configure-firewall-settings/](https://azure.microsoft.com/en-gb/documentation/articles/sql-database-configure-firewall-settings/)

The users were missing from the database , so I took the encrypted passwords out of the \\App_Data\\Users.xml and put into the database. This link shows where to find the user information  in the XML and the database.

[http://dnbe.net/docs/post/frequently-asked-questions#HowdoIresetlostadminpassword](http://dnbe.net/docs/post/frequently-asked-questions#HowdoIresetlostadminpassword)

I also found I had to take the blog guid and change the user and role table to use the imported blog guid, they were all set up with the guid from the set up script.

A few niggle bit was very easy to do in the end thanks to the migration tool and above blog posts.