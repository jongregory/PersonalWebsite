---
title: "Blog Rebuild with HTTPS all the time"
date: 2016-09-29T18:25:46Z
draft: false
tags: ["security","blog"]
---

 Ok so it was time for the blog to receive some TLC, I am running [BlogEngine.Net](http://dotnetblogengine.net/ "BlogEngine.Net") version 2.9 as an azure web app with an azure SQL database. Version 3.3 of [BlogEngine.Net](http://dotnetblogengine.net/) was available. There has been a lot of improvements to the user interface and editor. I was also running a multi user and multi blog set up which made the database upgrades trickier. So I opted for a full clean install and then to migrate the data over. I am not a profilic author so there was not too much to migrate.

Also with the push towards HTTPS for all pages and chrome marking pages insecure in 2017, [https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html](https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html "https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html") I wanted to upgrade to HTTPS. The best way to do this was to use a [Lets Encrypt](https://letsencrypt.org/ "Lets Encrypt") certificate which is a free automated certificate authority.

**Clean Installation of BlogEngine.Net**

This was the easiest part simply download the zip file from [http://blogengine.codeplex.com/releases/view/621156](http://blogengine.codeplex.com/releases/view/621156 "http://blogengine.codeplex.com/releases/view/621156"), then extract the files. The web.config needed to be updated to use the DbBlogProvider and a connection string added. 

{{< highlight xml >}}
    <blogProvider defaultProvider="**DbBlogProvider**" fileStoreProvider="XmlBlogProvider">
      <providers>
        <add description="Xml Blog Provider" name="XmlBlogProvider" type="BlogEngine.Core.Providers.XmlBlogProvider, BlogEngine.Core" />
		<add connectionStringName="BlogEngine" description="Sql Database Provider" name="DbBlogProvider" type="BlogEngine.Core.Providers.DbBlogProvider, BlogEngine.Core" />
      </providers>
    </blogProvider>
{{< / highlight >}}

The Membership Provider and Role Provider also needed to be updated to use the database although this is less important as I am sticking to single user mode.

{{< highlight xml >}}

 <membership defaultProvider="DbMembershipProvider">
      <providers>
        <clear />
        <add name="XmlMembershipProvider" type="BlogEngine.Core.Providers.XmlMembershipProvider, BlogEngine.Core" description="XML membership provider" passwordFormat="Hashed" />
		<add name="DbMembershipProvider" type="BlogEngine.Core.Providers.DbMembershipProvider, BlogEngine.Core" passwordFormat="Hashed" connectionStringName="BlogEngine" />
      </providers>
    </membership>
    <roleManager defaultProvider="DbRoleProvider" enabled="true" cacheRolesInCookie="false">
      <providers>
        <clear />
        <add name="XmlRoleProvider" type="BlogEngine.Core.Providers.XmlRoleProvider, BlogEngine.Core" description="XML role provider" />
		<add name="SqlRoleProvider" type="System.Web.Security.SqlRoleProvider" connectionStringName="BlogEngine" applicationName="BlogEngine" />
        <add name="DbRoleProvider" type="BlogEngine.Core.Providers.DbRoleProvider, BlogEngine.Core" connectionStringName="BlogEngine" />
      </providers>
    </roleManager>
    
{{< / highlight >}}

Once the blog was started up the admin section had a link to update to 3.3.5, which was upgraded automatically from the admin section without me having to touch a file. Very slick.

**Adding LetsEncrypt**

I have been wanting to try LetsEncrypt out for a while and this was ideal for my blog, I wasn't sure how to get a certificate onto a Azure WebApp using a custom domain. After some googling this Azure extension stood out a mile [https://github.com/sjkp/letsencrypt-siteextension](https://github.com/sjkp/letsencrypt-siteextension "https://github.com/sjkp/letsencrypt-siteextension"). Not only does it provide a UI for adding the certificate it also sets up a web job to refresh them when they expire. The LetsEncrypt certificates expire after 90 days , this is for security and to encourage automation to renew the licences. [LetsEncrypt Expiration Notes](https://letsencrypt.org/2015/11/09/why-90-days.html "LetsEncrypt Expiration Notes")

I found this [great detailed blog post](https://gooroo.io/GoorooTHINK/Article/16420/Lets-Encrypt-Azure-Web-Apps-the-Free-and-Easy-Way/21872#.V_qFHeArK70)  which explained a lot of the reasons for the different steps, however the 'Register a Service Principal' in powershell looked a bit tricker than the time I had available so I jumped back over to the [WIKI Documenation](https://github.com/sjkp/letsencrypt-siteextension/wiki/How-to-install "WIKI Documenation") for the extension and that covered how to do it in the Azure Control Panel  

I found the extension failed on the last step the first time it ran, then I ran again and it worked. Wasn't able to find out why and may have just been a azure refresh speed on one of the set up steps

**Add a https redirect (Skipped down to the enforce HTTPS section)**

Again a nice easy one, just need to add the redirect rule into the web.config this [Blog Post on Azure](https://azure.microsoft.com/en-gb/documentation/articles/web-sites-configure-ssl-certificate/ "Blog Post on Azure ") covers how to add a certificate to a custom domain, as I had done this with the Azure Extension I just needed to skip to the 'Enforce HTTPS section'

Adding the following section in the <system.webserver> section of the web.config moves all sessions to HTTPS

{{< highlight xml>}}
 <rewrite>
      <rules>
        <!\-\- BEGIN rule TAG FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!\-\- END rule TAG FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
    
{{< / highlight >}}

**Migrate old data **

 The final step was to migrate the data over from the old blog, I had created a new SQL Azure Database so just needed to take from three tables. be\_Posts, be\_Categories and be_PostCategory. I wrote the slightly funky query to generate a formatted insert statement and ran in SSMS with a results to text. Then moved the query over to the new database. It worked for all but three posts where the post data exceeded the limit in the results to text of SSMS. As there were only three I moved those posts manually. Not the cleanest of solutions I admit but I wanted a fresh install of the blog software and to make future upgrades easier by using the default blog guid as the blog id.

{{< highlight sql >}}

SELECT
'INSERT INTO \[dbo\].\[be_Posts\]
 (\[BlogID\]
 ,\[PostID\]
 ,\[Title\]
 ,\[Description\]
 ,\[PostContent\]
 ,\[DateCreated\]
 ,\[DateModified\]
 ,\[Author\]
 ,\[IsPublished\]
 ,\[IsCommentEnabled\]
 ,\[Raters\]
 ,\[Rating\]
 ,\[Slug\]
 ,\[IsDeleted\])
 VALUES
 (',
      char(39) + '27604F05-86AD-47EF-9E05-950BB762570C' + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + convert(varchar(50),\[PostID\]) + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + \[Title\] + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + \[Description\] + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + '*' + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + convert(varchar(50),\[DateCreated\]) + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + convert(varchar(50),\[DateModified\]) + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + \[Author\] + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + convert(varchar(50),\[IsPublished\]) + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + convert(varchar(50),\[IsCommentEnabled\]) + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + convert(varchar(50),\[Raters\]) + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + convert(varchar(50),\[Rating\]) + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + \[Slug\] + char(39) + CHAR(13) + CHAR(10)
      ,',' + char(39) + convert(varchar(50),\[IsDeleted\]) + char(39) + CHAR(13) + CHAR(10)
	  ,')'
  FROM \[blogjongregorydb\].\[dbo\].\[be_Posts\]
GO
{{< / highlight >}}

** Conclusion**

Writing this first post has been so much easier, the editor in 3.3.5 is much better and the ability to add links is far quicker. The code window has more formatting and is easier to edit, and code snippets can be added in directly. Although I still prefer the formatting of [http://hilite.me/](http://hilite.me/ "http://hilite.me/") .

Adding the LetsEncrypt extension and certificate was really convenient and just need to check the renewal of the certificate in 90 days time. 

But the blog and my personal CV website is marked as secure and I feel confident using this approach on other websites.