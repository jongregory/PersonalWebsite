---
title: "Testing Web Config IP Restrictions Locally"
date: 2017-01-27T10:07:26Z
draft: true
---

I was up against a hard deadline recently and needed to test some IP restrictions locally before deploying to a dev server. I have never had to do this locally before and had to jump through a few hoops to get it working. 

We wanted to put the restrictions in the config so they are applied to any environment the site is hosted on, this is easily achieved using the **<ipSecurity>** attribute in the **<security>** group. 

The sample xml below shows a configuration where all IP's are blocked except the ones listed, it is possible to invert this with the **allowUnlisted** attribute being set to true. When this is the case the IP's in the list are not allowed to access the site.

    <security>
      <ipSecurity allowUnlisted="false" denyAction="Forbidden">
        <!\-\- this line blocks everybody, except those listed below -->
        <!\-\- removes all upstream restrictions -->
        <clear/>
        <!\-\- allow requests from the local machine -->
        <add ipAddress="127.0.0.1" allowed="true"/>
        <!\-\- Allowed IP's-->
        <add allowed="true" ipAddress="0.0.0.0" subnetMask="255.255.0.0" />
      </ipSecurity>
    </security>

This iis.net article details the options for IP configuration restriction as well as other options [https://www.iis.net/configreference/system.webserver/security/ipsecurity?showTreeNavigation=true#005](https://www.iis.net/configreference/system.webserver/security/ipsecurity?showTreeNavigation=true#005)

To get this working on my local machine I had to do three other steps , although one may not have been required!

1 - Turn on the IIS Role service for IP security via the Turn Windows Features On and Off - the steps are detailed here [https://www.iis.net/configreference/system.webserver/security/ipsecurity?showTreeNavigation=true#003](https://www.iis.net/configreference/system.webserver/security/ipsecurity?showTreeNavigation=true#003)

2 - Allow the Security section to be overridden at the application level, within IIS the Security section is locked for override and needs to be set to Read/Write in the Feature Delegation settings. This is available at the server level in IIS and is covered in this blog post [https://www.iis.net/learn/manage/managing-your-configuration-settings/an-overview-of-feature-delegation-in-iis#02](https://www.iis.net/learn/manage/managing-your-configuration-settings/an-overview-of-feature-delegation-in-iis#02)

3 - Allow Override in the **ApplicationHost.config** files, there are two of these one for the machine located at _%windir%\\system32\\inetsrv\\config\\applicationHost.config _and another in the project folder at _.vs\\config. _I set both to be safe but it maybe that only the project level one is required.

This is an example of the required setting 

<section name="ipSecurity" overrideModeDefault="Allow" />

This is the stack overflow post that pointed me in the right direction for the ApplicationHost.config [http://stackoverflow.com/questions/16220819/internal-server-error-with-web-config-ipsecurity](http://stackoverflow.com/questions/16220819/internal-server-error-with-web-config-ipsecurity)