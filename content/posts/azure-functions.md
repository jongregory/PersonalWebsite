---
title: "Azure Functions"
date: 2018-02-28T10:02:43Z
draft: true
tags: ["cloud","azure","serverless"]
---

[Azure Functions](https://azure.microsoft.com/en-us/services/functions/ "Azure Functions") are Functions as a Service (FAAS) which are a type of [Serverless Architecture](https://www.martinfowler.com/articles/serverless.html). More specifically Serverless Compute and allow the developer to create and run small pieces of code without the need for an application. They are a level above Platform as a Service (PAAS) where the application framework is provisioned by the cloud provider.  

There are many FAAS providers, this post describes a recent experience using [Azure Functions](https://azure.microsoft.com/en-us/services/functions/ "Azure Functions") and [Azure Table Storage](https://azure.microsoft.com/en-gb/services/storage/tables/ "Azure Table Storage") to implement a Serverless API.

To trigger a function there are a number of options;

- Blob / Queue Storage Event
- Azure Cosmos DB
- SaaS Event Processing such as saving a file in one drive
- HTTP Webhook URLs
- Timer based processing
- Real-time Stream /  Real-time Bot Messaging


This solution for this requirement was originally pitched as an API, but on closer inspection the size of the logic meant it was ideal to the webhook approach of an azure function. This reduced the required infrastructure and running costs, the [Azure Functions Pricing](https://azure.microsoft.com/en-us/pricing/details/functions/ "Azure Function Pricing") is per call model and the first million per month are free.


Storage

Benefits

Drawback

Possible use cases

Useful Resources

[Azure Serverless Cookbook](https://azure.microsoft.com/en-us/resources/azure-serverless-computing-cookbook/en-us/?_lrsc=2dfc26f7-a655-430d-8bbf-b7cbb5b33983 "Azure Serverless Cook Book")
  



*Points to cover*

Can replace simple apis
Possible Use cases
Darwbacks - ip restriction / security
Azure Tables - Azure Storage Explorer
Amazon Equivalent
Cook book link - https://azure.microsoft.com/en-us/resources/azure-serverless-computing-cookbook/en-us/?_lrsc=2dfc26f7-a655-430d-8bbf-b7cbb5b33983
Are they charged per call without key for bots etc?

Documentation - https://docs.microsoft.com/en-us/azure/azure-functions/

