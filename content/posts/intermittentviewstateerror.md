---
title: "ASP.NET Web Forms - Intermittent View State Error"
date: 2016-08-02T12:08:21Z
draft: true
---

On a web forms application on load balanced environment I recently had to investigate some errors for invalid viewstate. It was an intermittent error which only occurred when someone important used the site.

This became high profile quickly and very annoying, it has been a long time since I had to deal with view state thanks to MVC and it was difficult to reproduce. Eventually we found that clearing all caches and browser history allowed the error to be recreated.

The error message was a value cannot be null error;

`System.Web.HttpException: Value cannot be null.
Parameter name: inputString \[ArgumentNullException: Value cannot be null.Parameter name: inputString\]
at System.Web.UI.ObjectStateFormatter.Deserialize(String inputString, Purpose purpose)
at System.Web.UI.Util.DeserializeWithAssert(IStateFormatter2 formatter, String serializedState, Purpose purpose)
at System.Web.UI.HiddenFieldPageStatePersister.Load()
\[ViewStateException: Invalid viewstate. Client IP: 86.131.46.52 Port: 49531 Referer: https://*********.com/checkout/payment Path: *******.aspx User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; rv:11.0) like Gecko ViewState: \] \[HttpException: The state information is invalid for this page and might be corrupted.\]`

The machinekey was in the web.config for both servers and the load balancing set up correctly. Looking at New Relic there was more viewstate errors which didn''t hit the application so were not logged.

The most likely solution found when googling was to move the machine key to the machine.config file at the server level _C:\\Windows\\Microsoft.NET\\Framework64\\v4.0.30319\\Config_

The site web.config had the machine key removed and there is a web.config in the same directory as the machine.config , in one server this had the machine key and on another it didn''t. So it was removed from all.

This url has some useful information about the scope of the configuration files

[https://msdn.microsoft.com/en-us/library/ms178685.aspx](https://msdn.microsoft.com/en-us/library/ms178685.aspx)

ASP.NET 4.5 introduced cryptographic improvements, when the configuration was set wrong these were picked up and the following error was received.

`System.Configuration.ConfigurationErrorsException: When using <machineKey compatibilityMode="Framework45" /> or the MachineKey.Protect and MachineKey.Unprotect APIs, the ''validation'' attribute must be one of these values: SHA1, HMACSHA256, HMACSHA384, HMACSHA512, or alg:\[KeyedHashAlgorithm\]. (C:\\Windows\\Microsoft.NET\\Framework64\\v4.0.30319\\Config\\web.config line 31)`

Explicitly setting the validation key'' validation="SHA1" '' to ensure the correct encryption  setting  was picked up solved this.

There is more information about the improvements here;

[https://blogs.msdn.microsoft.com/webdev/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2/](https://blogs.msdn.microsoft.com/webdev/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2/)

But after all that reconfiguration  the error popped up once more in New Relic!

After some more investigation we found that the viewstate had been moved to the bottom of the page for SEO, on the page receiving the error it was possible to submit the page before it had completed loading and then error then occured. Moving the viewstate back to the top seems to have cured it but we are keeping a close eye on New Relic