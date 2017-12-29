---
title: "Hyper-V Virtual Machine Copy"
date: 2016-06-16T20:06:41Z
draft: true
---

I needed to evaluate a several database tools against an application I was writing,  so it made sense to create VM with the application and then copy it. Looking into Hyper-V  there was no option to clone a Virtual Machine without puchasing a tool. 

Looking at google there were two options;

1.  Copy the virtual hard disk in file explorer and then create a new VM using the Hyper-V wizard and point to the copied VHD when setting up the disk
2.  Export the VM and then import as a new VM using the import export tool.

The following steps are how to do option 2 , note that this operation can only be performed once for each export. The export files can only be imported once, if you need to do multiple copies you will need to do another export for each import.

**In the Hyper-V Manager**

1 - Chose Export for the right hand side menu

![](http://blogjongregory.blob.core.windows.net/blogimages/HyperVCopy/HyperVExport.PNG)

2 - Select a location for the export files to go, this is a temporary location as once imported the directory will remain but cannot be used again.

![](http://blogjongregory.blob.core.windows.net/blogimages/HyperVCopy/HyperVExportFileDialog.PNG)

3 - The export can take a while .....

![](http://blogjongregory.blob.core.windows.net/blogimages/HyperVCopy/HyperVExportingStatus.PNG)

**Importing the exported Virtual Machine**

1 - In the Hyper-V Manager select ''Import a Virtual Machine''

![](http://blogjongregory.blob.core.windows.net/blogimages/HyperVCopy/HyperVImport.PNG)

2 - Select the folder where the exported Virtual Machine files were placed, selecting the top level folder is ok

![](http://blogjongregory.blob.core.windows.net/blogimages/HyperVCopy/HyperVImportFolder.PNG)

3 - Select the location for the new Virtual Machine to be created, note you will need to change these values as they will be the same as the original machine and it will attempt to overwrite.

![](http://blogjongregory.blob.core.windows.net/blogimages/HyperVCopy/HyperVImportLocations.PNG)

4 - It is important to select ''Copy the virtual machine'' otherwise it will overwrite the original machine, the import can take a while.

![](http://blogjongregory.blob.core.windows.net/blogimages/HyperVCopy/HyperVImportType.PNG)

5 - The imported VM will appear to have a duplicate name, this can be changed by right clicking on the name and changing to the required name

Once complete the VM can be started and used and is an exact copy of the original, this was ideal for the scenario as the evaluation was using trail period software and the VM''s were only required for a few days.