---
title: "Azure Service Bus"
date: 2019-01-31T07:14:46Z
draft: false
---

[Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) is the Azure Cloud Messaging offering and is ideal for decoupling applications, having messaging resilience and building publish & subscribe communications.

## Getting Started ##

The [Documentation]() is extensive but I found it much easier to dive into the [samples](https://github.com/Azure/azure-service-bus), if you familiar with message buses it easy to pick up, and if your new to the subject the documentation can support the concepts. There are samples for .Net Core, .Net Standard and .Net Framework each of which use different NuGet libraries for the SDK Code, the Azure Portal setup is the same for each. 

## Key Concepts ##

[Queues](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-queues-topics-subscriptions#queues) are the base of the messaging application with messages being enqueued by one process and then dequeued by another, multiple listeners can share a queue but a message will only be processed by one listener so this would only provide processing scaling and the listeners should all process the message identically.  

[Topics](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-queues-topics-subscriptions#topics-and-subscriptions) are the azure implementation of publish subscribe and are a way of sending the same message to multiple applications. Topics are defined in the Azure portal and are queues behind the scenes, subscriptions are also defined in the portal and these are the subscribing processes who receive a copy of the message.

[Sessions](https://docs.microsoft.com/en-us/azure/service-bus-messaging/message-sessions) provide guaranteed FIFO by associating message into groups using a provided session id and the receiver accepts messages for that session only. Sessions don't expire but do take up storage so its best practice to open and close them once complete. A use case maybe a file transfer, or series of ordered update messages.

[Duplicate Detection](https://docs.microsoft.com/en-us/azure/service-bus-messaging/duplicate-detection) in the event of a failure during a enqueue of a message duplicate detection allows the message to be sent again on recovery to get the confirmation, if the initial message was committed to the queue it is identified as a duplicate and removed.

[Dead Letters](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-dead-letter-queues) are automatically created with the queue and are a place to park messages that can not be processed, they can then be examined and either corrected or deleted as required. Messages can be moved to the dead letter queue by the listeners processing code.

[Auto Forwarding](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-auto-forwarding) is a service which automatically takes messages from one queue or topic and forwards them to another queue or topic, this can provide further decoupling between sender and receiving and assist in scaling. There is a 2000 subscription limit on a topic.

[TimeToLive](https://docs.microsoft.com/en-us/azure/service-bus-messaging/message-expiration) - this provides and expiry time for a message so if its not processed by that time it becomes unavailable. There is an option to add it to the dead letter queue otherwise its deleted. This is useful to manage costs as abandoned messages don't take up storage in the azure subscription especially in pre prod environments where having a clean queue is beneficial to testing.

[Relays](https://docs.microsoft.com/en-us/azure/service-bus-relay/) - Service Bus Relay provides web services to be able to use a service bus from an on premise application. It removes the need to change the network infrastructure or open non standard ports. It carries an extra cost but help facilitate hybrid cloud and on premise applications.

## Use Cases ##

**Decoupling** applications is crucial especially when they cross business domains such as integrations, using relays can also provide decoupling between hybrid applications with differing levels of performance in the cloud and on premise. 

**Resilience & Retry** is possible when using a messaging system, if the receiving application is not available to process the message they can wait in the queue until it ready to receive them, this is also beneficial to help level out peaks in processing, one application may generate a spike of messages at certain times which queue up and can be processed asynchronously by the receiving application.

**Publish & Subscribe** for distributed applications is a way of sending notifications to multiple applications, a website purchase for example may need to be sent to order processing, stock level and finance applications. The website need only send a single message and any applications interested can subscribe to it.

**Audit & Logging** when using the topic or publish subscribe model and audit or logging subscriber can be set up to record all messages being sent to provide a audit trail, this removes the need to the main applications to do the logging processing and provide a central log when there are multiple publishers.

**Delayed Message Processing** is possible with [message deferral](https://docs.microsoft.com/en-us/azure/service-bus-messaging/message-deferral), this is useful when messsages have to be processed in order or and event has to occur first. A purchase could queue a feedback email to send 24 hours days later for example once the order has been show as shipped.

## Considerations ##

Azure Service Bus is driven cloud based so reliant on HTTP Requests, so the ordering of the messages reaching a queue when en-queueing in quick succession may not be the same as the order of calls in the code.

When de-queueing messages, if ordering is important then the need to consider the number of listeners. If there is more than one then the messages will be processed on a first come first served basis. 

Transactions - there is no distributed transaction between the service bus and a database so you either get at-least-once or at-most-once delivery depending on whether you close the DB transaction first or mark the message as processed first. This means you need to implement everything in an idempotent manner on the consumer side (if using at-least-once - with at-most-once you accept loss of data). [This Stack Overflow](https://stackoverflow.com/questions/15556084/azure-service-bus-and-transactions) question explains the concept in more detail. This should not be confused with the concept of transactions within azure service bus .

Service Bus Queues are different to storage queues, although similar in name  - there is a a summary article [here](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted)
