---
title: "Consistent Redirects and Session State"
date: 2016-11-29T18:49:33Z
draft: false
tags: ["tips","security"]
---

One thing I learnt from experience to check when getting unexpected behaviour with sessions in ASP.Net is the redirects. I have worked on sites where the HTTP and HTTPS redirects are inconsistent and this can cause issues.

One of the more serious cases experiences was were a 'www' redirect was missing and redirect was being used to transfer to a third party site. In this case the user started a session using the address at `[http://websitedomain..](http://websitedomain..).` and then transferred to the third party site.

When the user was redirected to the full web address `[http://www.websitedomain..](http://www.websitedomain..).` a new session was started by IIS and the user lost their session and all information associated with it. This severely affected the user experience on the site.

Many issues with lost sessions are difficult to diagnose due to the symptoms being misleading. Fortunately the fix is quick and easy , simply specifying the redirects in the web.config for the site ensured the consistency of URL for all sessions on the site.

These rules can be put into IIS but these can be lost in some cases when the web.config is overwritten on a deployment. In the rules are in the web.config then there is the benefit of versioning in source control and consistency across web-farms.

Here is an example web.config entry for http to https and non-www to www redirects;

{{< highlight xml>}}
   <rewrite>
      <rules>
        <rule name="Redirect landing request to trailing slash" stopProcessing="true">
          <match url="landing\\/(.*\[^\\/\])$" />
          <action type="Redirect" url="{R:0}/" redirectType="Permanent" />
          <conditions>
            <add input="{REQUEST_FILENAME}" matchType="IsDirectory" />
          </conditions>
        </rule>
        <rule name="Redirect to HTTPS" enabled="true" stopProcessing="true">
          <match url=".*" />
          <conditions logicalGrouping="MatchAll" trackAllCaptures="false">
            <add input="{HTTPS}" pattern="^OFF$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:0}" redirectType="Permanent" />
        </rule>
        <rule name="redirect non www to www" stopProcessing="true">
          <match url=".*" />
          <conditions  logicalGrouping="MatchAll" trackAllCaptures="false">
            <add input="{HTTP_HOST}" pattern="^domain.com$" />
          </conditions>
          <action type="Redirect" url="https://www.domain.com/{R:0}" />
        </rule>
      </rules>
    </rewrite>
    
{{< / highlight >}}