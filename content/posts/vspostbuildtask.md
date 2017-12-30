---
title: "Visual Studio Website Projects - Restore References without a build"
date: 2016-01-29T16:01:37Z
draft: false
tags: ["vs","tips"]
---

 I recently had to deal with a multiple missing references issue on the CI Build Server for Visual Studio website project. 

Building the website was not an option as it was a CMS project and the build took over ten minutes, and it was not possible to convert it to a web application either. 

Team City was being used to build the class library projects and the Nuget restore step was skipping the website project from the solution file as it was called local.<websitename> in the *.sln and on the CI server it was set up as dev.<websitename>

I needed a generic process where new nuget packages and class library projects could be added with having to make large changes the established CI process and project , and was restricted by the limitations of the legacy CMS.

The solution to the two reference scenarios was quite simple in the end;

**Scenario 1 – Adding a reference to a project in the visual studio solution**

1.  Add the reference to the website as usual in Visual Studio by right clicking on the project 
2.  In the Class Library project that is being referenced add a custom build step, this will push the dll to the website \\bin folder for each build on any machine.

*   Right Click on the Website Project 
*   Build Events
*   Add the following line to the ‘Post-build event command line’

               
{{< highlight csharp "linenos=table" >}}



xcopy /Y "$(ProjectDir)$(OutDir)$(TargetFileName)" "$(ProjectDir)..\\CMS\\Bin"

{{< / highlight >}}

Using this technique means the project becomes responsible for putting the output dll into the website so the website does need to be compiled , and nothing needs to be configured on the CI server. If the project is being built in Visual Studio the **/Y** option forces and overwrite so the build does not fail.

**Scenario 2 – Referencing NuGet Packages in a Visual Studio Website**

  
Add the following Powershell into a script in the website project root directory and committed to source control.

{{< highlight powershell "linenos=table" >}}



$scriptpath = $MyInvocation.MyCommand.Path
$dir = Split-Path $scriptpath
$files = Get-ChildItem $dir\\Bin\\*.refresh

ForEach ($file in $files) { 
$content = Get-Content $file
$filename = Split-Path $content -leaf
Write-Host "Restoring File : "  $dir\$content " To " $dir\\bin\$filename
Copy-Item $dir\$content $dir\\bin\$filename -force
}

{{< / highlight >}}

This script was then run in the CI process after the package restore , it finds the ***.dll.refresh** files and copies them out of the packages folder and into the **\\bin** of the website project.

When adding a nuget package to the website project the [Refresh File](http://stackoverflow.com/questions/4089165/what-is-a-dll-refresh-file-in-asp-net)  is added to source control, but not the dll file itself. The refresh file is a text file used by visual studio to manage the location of the files for refreshing on builds. 

This approach was generic and maintenance free and saved having to build the website project unnecessarily .