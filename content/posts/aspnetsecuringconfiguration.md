---
title: "ASP.Net Securing Configuration"
date: 2016-08-15T15:08:45Z
draft: false
tags: ["tips","security","pentesting"]
---

The management of configuration is not the most exciting aspects of development and often one where mistakes are made. The aim with these techniques is to try and strike a balance between security without affect development velocity. 

Ideally configuration management should be considered at the start of the projects and the following aims met;

1.  Encrypt all sensitive configuration
2.  Keep passwords and keys out of source control
3.  Maintain portability between environments with minimum configuration
4.  Encrypt using machine specific keys
5.  Co-Locate configuration for ease of maintance
6.  Remove application configuration from Web.config

The following are some ways to achieve the above.

**Machine Keys Location **

In a load balanced environment a machine key is required in each instance of the application for session and encrypt. These are often put into the web.config but there is then a risk that these get put into source control.

A solution is to move the machine keys out of the web config and into the machine.config on each of the servers.

Means the machine key does not have to be in source control and can be left on each of the servers, this also has the added advantage that the machine key is available to all threads running on the server not just the web site.

<Location - mention 32 and 64 bit - add it to the system.web>

<Sample config>

[https://msdn.microsoft.com/en-us/library/ms178685.aspx](https://msdn.microsoft.com/en-us/library/ms178685.aspx)

Should keep the key in a secure location.

**Two Methods of separating out web and application config**

File - [https://msdn.microsoft.com/en-US/library/ms228154(v=vs.100).aspx](https://msdn.microsoft.com/en-US/library/ms228154(v=vs.100).aspx)

configSource - [https://msdn.microsoft.com/en-us/library/system.configuration.sectioninformation.configsource(v=vs.110).aspx](https://msdn.microsoft.com/en-us/library/system.configuration.sectioninformation.configsource(v=vs.110).aspx)

**Encrypting a external config file directly (app.config or equivalent)**

1.  .Open Command Prompt as Administrator
2.  Rename the the file Web.Config
3.  Wrap the xml <configuration> </configuration>
4.  Run the encryption command "C:\\Windows\\Microsoft.NET\\Framework\\v4.0.30319\\aspnet_regiis.exe" -pef "connectionStrings" "D:\\EncryptedConfig"
5.  Remove the <configuration> </configuration>
6.  Restore the file name

**Encrypting a external config file via the web.config**

1.  Run the encryption command "C:\\Windows\\Microsoft.NET\\Framework\\v4.0.30319\\aspnet_regiis.exe" -pef "connectionStrings" "<Location of web.config>"

**Creating a custom config setting and encrypting**

<Two options here - a custom configuration section which can represent complex structures and be typed, or NameValueCollection for Key / Value Pairs ( the same approch as app settings)

Only some sections of application configuration may need encrypting, by creating a custom section this can be redirected from the main web.config using configsource and encrypted. Unsecure configuration can then be placed in app settings as usual without the maintenance overhead of encryption. 

[https://msdn.microsoft.com/en-us/library/2tw134k3.aspx](https://msdn.microsoft.com/en-us/library/2tw134k3.aspx)

 \- Sample Encryption

 \- Sample Config File

 \- Web.config redirect

 \- Encryption Command

 \- C# value access 

**Web.Config Transformations**

Web.Config transformations allow for section of the configuration file to be replaced with different types of builds Debug, Release etc. These can work on in conjunction with the techniques above , the transforms do need to be available during the build so more than likely put into source control. 

So in the situation where configuration does not need to be in source control a redirect can be used, for environment specific configuration which can go into source control a transform is ideal

[https://msdn.microsoft.com/en-us/library/dd465326(v=vs.110).aspx](https://msdn.microsoft.com/en-us/library/dd465326(v=vs.110).aspx)