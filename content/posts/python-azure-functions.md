---
title: "Python Azure Functions"
date: 2019-03-13T16:49:55Z
draft: true
tags: ["python","azure","faas"]
---

These instructions show how to create and run a azure python function locally (I installed python 3.6) - [https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python](create-first-function-python) 

These links have additional supporting information;

[https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-python](functions-reference-python)

[https://docs.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings](functions-triggers-bindings)

To get the modules loading locally from the requirements.txt you can run this - which pulls them all down.

<workingdir>\.env\scripts\python.exe -m pip install -r requirements.txt

When publishing the full script into azure I had to install docker for windows so the extra dependencies get built locally and pushed up, 


{{< highlight python >}}

func azure functionapp publish poc-python-fn --build-native-deps

{{< / highlight >}}