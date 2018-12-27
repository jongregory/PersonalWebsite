---
title: "SSL V 3.0 - Disable Poodle Threats on IIS"
date: 2016-08-12T15:08:13Z
draft: false
tags: ["tips","security","pentesting"]
---

On a recent PEN test the SSL V3 POODLE bug was picked up on the server [http://www.symantec.com/connect/blogs/ssl-30-vulnerability-poodle-bug-aka-poodlebleed](http://www.symantec.com/connect/blogs/ssl-30-vulnerability-poodle-bug-aka-poodlebleed)

To test a website this handy page reports on any url visible to the browser [https://cryptoreport.thawte.com/checker/views/certCheck.jsp](https://cryptoreport.thawte.com/checker/views/certCheck.jsp)

I assumed this would be a setting in IIS but the advice from Microsoft is a quick registry edit - detailed in the ''Disable SSL 3.0 Server Software'' section in this article [https://technet.microsoft.com/library/security/3009008.aspx](https://technet.microsoft.com/library/security/3009008.aspx)

### Disable SSL 3.0 in Windows****For Server Software

You can disable support for the SSL 3.0 protocol on Windows by following these steps:

1.  Click **Start**, click **Run**, type **regedt32** or type **regedit**, and then click **OK**.
2.  In Registry Editor, locate the following registry key:
    
    HKey\_Local\_Machine\\System\\CurrentControlSet\\Control\\SecurityProviders\\SCHANNEL\\Protocols\\SSL 3.0\\Server
    
    **Note** If the complete registry key path does not exist, you can create it by expanding the available keys and using the **New** -> **Key** option from the **Edit** menu.
    
3.  On the **Edit** menu, click **Add** **Value**.
4.  In the **Data** **Type** list, click **DWORD**.
5.  In the **Value** **Name** box, type **Enabled**, and then click **OK**. 
    
    **Note** If this value is present, double-click the value to edit its current value.
    
6.  In the **Edit DWORD (32-bit) Value** dialog box, type **0** .
7.  Click **OK**. Restart the computer.

**Note **This workaround will disable SSL 3.0 for all server software installed on a system, including IIS.