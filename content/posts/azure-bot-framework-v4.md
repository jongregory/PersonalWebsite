---
title: "Azure Bot Framework V4"
date: 2018-10-10T13:55:03Z
draft: false
tags: ["bot framework","azure"]
---

**Overview**

The azure bot service is a C# or JS framework for building bots to run in Azure. Its enables bots to be created and deployed quickly. The documentation has some 5 minute quick start guides to demonstrate the ease of use - [https://docs.microsoft.com/en-us/azure/bot-service/?view=azure-bot-service-4.0](https://docs.microsoft.com/en-us/azure/bot-service/?view=azure-bot-service-4.0)

As well as providing a framework and tools to build bots there is integration into Azure Cognitive Services so AI features can be integrated into the bot via API tools so powerful user interactions can be built quickly.

The documentation is very good and so are the samples, this article is intended as a quick guide to some areas of interest. As with most powerful frameworks its quick to set up a Happy Path but there is also a lot of other features to learn and read about.

**Key Concepts**

The bots communicate via HTTP requests allowing multiple channels to be used, this document describes the process and concepts - How Bots Work and the supported Channels are here Connect to Channels

**Channels**

The majority of the bots built so far have used the direct line api and then taken the webchat from [https://github.com/Microsoft/BotFramework-WebChat](https://github.com/Microsoft/BotFramework-WebChat), this can be customised to the webchat panel appears in a window styled. 

**Dialogs**

Dialogs are a way of managing the conversation with the user and the bot, and the waterfall dialog is structure to use for the conversation flow. The Dialogs Library documentation demonstrates how to set these up, and multiple dialogs can be used for complex conversations. Each step in the dialog type can be a set type to capture a specific format such as text or datetime. The available types are listed here - Dialog Types

**Turn**

A Turn consists of the user's incoming activity to the bot and any activity the bot sends back to the user as an immediate response. You can think of a turn as the processing associated with the arrival of a given activity.

The Turn Context provides information about the activity such as the sender and receiver, the channel, and other data needed to process the activity. One of the most important concepts in the framework

The adapter, an integrated component of the SDK, serves as the conductor of the framework. The service uses the activity information to create an activity object, and then calls the adapter's process activity method while passing in the activity object and authentication information

The bot's turn handler, which makes up most of the application logic, takes a turn context as its argument. The turn handler will typically process the inbound activity’s content and generate one or more activities in response, sending these out using the turn context's send activity method

Response handlers (also sometimes referred to as event handlers, or activity event handlers) can be added to the context object. These handlers are called when the associated response happens on the current context object, before executing the actual response

**Middleware**

The version 4.0 of the framework introduced middleware which is an important concept for the architecture of the bot, its important to consider state management in the middleware. 

Resource Management (.Bot file)
The .bot file is another new concept with version 4, and is used to manage configuration of services used by the bot - [https://docs.microsoft.com/en-us/azure/bot-service/bot-file-basics?view=azure-bot-service-4.0](https://docs.microsoft.com/en-us/azure/bot-service/bot-file-basics?view=azure-bot-service-4.0)

The credentials in the bot file are encrypted and use the bot secret which needs to added to the app settings. 

The .bot file can be managed from the command line with the MSBot CLI tool.

**Analytics**

Application insights has an extension to provide analytics for a bot and its channels - [https://docs.microsoft.com/en-us/azure/bot-service/bot-service-manage-analytics?view=azure-bot-service-4.0](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-manage-analytics?view=azure-bot-service-4.0)

**Open Source**

The entire bot framework, sdk, web channel and documentation are open sourced on GitHub, I had a documentation PR approved (smile)

There are 43 repos in total [https://github.com/Microsoft?utf8=%E2%9C%93&q=bot&type=&language=](https://github.com/Microsoft?utf8=%E2%9C%93&q=bot&type=&language=) a few useful ones are listed below

[https://github.com/Microsoft/BotBuilder](https://github.com/Microsoft/BotBuilder)

[https://github.com/microsoft/botbuilder-samples](https://github.com/microsoft/botbuilder-samples)

[https://github.com/Microsoft/botbuilder-dotnet](https://github.com/Microsoft/botbuilder-dotnet)

[https://github.com/Microsoft/BotFramework-WebChat](https://github.com/Microsoft/BotFramework-WebChat)

[https://github.com/Microsoft/BotFramework-Emulator](https://github.com/Microsoft/BotFramework-Emulator)

**Version History**

Version 4 of the Azure Bot Framework was released late 2018 and is a complete rewrite using .Net Core. This is the version which should be used moving forward, I wrote a few POC bots in Version 3 and have had to rewrite the ones I wanted to keep in Version 4.

**Hints & Tips**

*Secrets*

The .bot file is encrypted and uses secrets, in the turtorial I followed to get started in advised putting the secret in appsetting.json, but this ends up in source control which is not secure. So the bot secret should be managed outside of source control. This article [http://martink.me/articles/managing-secrets-with-bot-files-in-bot-framework-v4](http://martink.me/articles/managing-secrets-with-bot-files-in-bot-framework-v4) describes an approach for local and deployed management. Note I have not tried this out yet.

*Additional Resources*

[https://blogs.msdn.microsoft.com/jamiedalton/2018/11/01/bot-framework-v4-resources/](https://blogs.msdn.microsoft.com/jamiedalton/2018/11/01/bot-framework-v4-resources/)

*Authentication Issues*

Version 4 introduced the .Bot file which ships with dll into the cloud hosted App Service - [https://docs.microsoft.com/en-us/azure/bot-service/bot-file-basics?view=azure-bot-service-4.0](https://docs.microsoft.com/en-us/azure/bot-service/bot-file-basics?view=azure-bot-service-4.0 ) When generating a bot from a template in azure this contains information about configuration and services, this is usually fine when working locally but can then cause issues publishing the bot to azure. The MicrosoftAppId and MicrosoftAppPassword are used by the Bot Channel to authenticate to the Bot App Service and if these are not updated correctly you can get confusing error messages.

The entries in the .Bot file are encrypted and the MSBot command line tool can be used to manage them;

MSBot Documentation - [https://github.com/Microsoft/botbuilder-tools/blob/master/packages/MSBot/docs/bot-file-encryption.md](https://github.com/Microsoft/botbuilder-tools/blob/master/packages/MSBot/docs/bot-file-encryption.md) 

Add Service Endpoint (App Id/Password) - [https://github.com/Microsoft/botbuilder-tools/blob/master/packages/MSBot/docs/add-services.md](https://github.com/Microsoft/botbuilder-tools/blob/master/packages/MSBot/docs/add-services.md)

Trouble Shooting Authentication Issues - [https://docs.microsoft.com/en-us/azure/bot-service/bot-service-troubleshoot-authentication-problems?view=azure-bot-service-4.0#enable-security-localhost](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-troubleshoot-authentication-problems?view=azure-bot-service-4.0#enable-security-localhost)

Enable App Service Logging (Required to figure out what an earth is happening with Bots) - [https://docs.microsoft.com/en-us/azure/app-service/web-sites-enable-diagnostic-log](https://docs.microsoft.com/en-us/azure/app-service/web-sites-enable-diagnostic-log)



**Deployment**

If the Bot is built in the Azure portal it builds everything needed to run the bot, however as this is all templated it can cause some issues later when the source code is changed in Visual Studio, it is a cleaner to remove all the generated Azure Resources and deploy your bot into an App Service and create a Bot Channel. This can then be deployed directly from a Visual Studio or a deployment pipeline if required. This document talks through the setup and Visual Studio Deployment - [https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-deploy-azure?view=azure-bot-service-4.0](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-deploy-azure?view=azure-bot-service-4.0)

**Greeting Messages**

When working with the emulator the bot sends a greeting message on start up, but when using the direct line api this doesn't always work so the user has to type 'Hi' to initiate a chat, this blog post details how to structure the JS to resolve this;

[https://blog.botframework.com/2018/07/12/how-to-properly-send-a-greeting-message-and-common-issues-from-customers/](https://blog.botframework.com/2018/07/12/how-to-properly-send-a-greeting-message-and-common-issues-from-customers/)