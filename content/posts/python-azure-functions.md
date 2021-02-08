---
title: "Python Azure Functions"
date: 2019-03-13T16:49:55Z
tags: ["python","azure","faas"]
---

An interesting challenge this month was to take some python code that had been produced by a data scientist working in another company in the group. The script was usually run manually on laptops using marketing datasets, the output was then used in reports and presentations. 

The python was being included in part of an application to take a daily dataset, produce insights data and then feed that into PowerBi as a data file. 

Azure functions now have python in preview, and as the application was not being considered for production use in the near future they were chosen to run the script. 

Azure functions can be triggered in many ways, using the HTTPTrigger allowed the script to run ad-hoc and pick up the input dataset from Azure Blob Storage if present and then output to another blob storage. To use within the wider application an Azure Logic App was intended to trigger the function. 

These are the high level steps used to set up the function; 

* These instructions show how to create and run a azure python function locally (I installed python 3.6) - [https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python](create-first-function-python) 

* These links have additional supporting information;

	[https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-python](functions-reference-python)

	[https://docs.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings](functions-triggers-bindings)

* To get the modules loading locally from the Python requirements.txt you can run this - which pulls them all down.

	{{< highlight bash>}}
	<workingdir>\.env\scripts\python.exe -m pip install -r requirements.txt
	{{< / highlight >}}

* When publishing the full script into azure I had to install docker for windows so the extra dependencies get built locally and pushed up, this was a simple one line command to publish;


	{{< highlight python >}}
	func azure functionapp publish poc-python-fn --build-native-deps
	{{< / highlight >}}