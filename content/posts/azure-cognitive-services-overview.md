---
title: "Azure Cognitive Services Overview"
date: 2018-04-09T20:26:07+01:00
draft: false
tags: ["cloud","azure","ai","cognitive services"]
---

## Introduction ##

On March 1st I risked the snow disruption to attend a great event in Birmingham hosted by [Fusion Meetup](https://twitter.com/fusionmeetup?lang=en) where Microsoft demonstrated their Azure Cognitive Services.

This was a hands on event with a chance to have a go with each of the available Cognitive Services.

This post is a summary of the services presented with some thoughts on how powerful they are and the benefits they could bring to a website.

## What are Azure Cognitive Services?


[Azure Cognitive Services](https://azure.microsoft.com/en-us/services/cognitive-services/) are a set of consumable tools which make Cognitive AI functions available to a wider audience. This means websites and applications can be augmented with cognitive AI tooling for more advanced communication with users. 

Cognitive Services are one third of the [Microsoft AI Platform](https://azure.microsoft.com/en-us/overview/ai-platform/) suite of AI services, the others being Machine Learning Services and BOT Framework.

By providing a set of API's and Dashboard Portals Microsoft have abstracted the  complexity of AI functionality and brought it within the scope of small to medium projects.

There are four main Cognitive Services covered in this post;

1. [Vision](https://azure.microsoft.com/en-us/services/cognitive-services/directory/vision/) - a set of services to process and extract data from images, including Face and Emotion recognition, Content Moderation and Image/Video Indexing
2. [Knowledge](https://azure.microsoft.com/en-us/services/cognitive-services/directory/know/) - tooling for experience learning, recommendation engines and enhanced BOTS.
3. [Language](https://azure.microsoft.com/en-us/services/cognitive-services/directory/lang/) - Natural Language Processing with LUIS, Text Analytics and Translation Services
4. [Speech](https://azure.microsoft.com/en-us/services/cognitive-services/directory/speech/) - Tooling for Speech Recognition and Instant Translations.

Equally as exciting and with some overlap is the [Machine Learning Services](https://azure.microsoft.com/en-us/services/machine-learning-services/) provided by Microsoft, these can be used in conjunction with the [Cognitive Services](https://azure.microsoft.com/en-us/services/cognitive-services/) to provide powerful solutions. So they will be mentioned in this post but I plan to produce a dedicated post covering Machine Learning Services in more detail.

## How do I use Cognitive Services?

The major benefit of the Azure Cognitive services is the ease of use and integration into applications. They can be used with a mix of the Azure Portal for setup and configuration with REST API and JSON payload or SDK to interact with the service. 

Depending upon the service, LUIS the Language Understanding and Intelligence Service for instance, requires setup of example data and training to learn the data.

Each service has a getting started guide in the docs and there is a [AI Services Workshop](https://github.com/martinkearn/AI-Services-Workshop) GitHub library with samples and instructions.


## What can I do with Cognitive Services?

This is the really exciting part of Azure Cognitive Services, they open up the possibilities for applications to interact with users beyond the traditional keyboard approach.

<expand this which each of the services and what could be done>

### Vision ###

[Azure Computer Vision](https://azure.microsoft.com/en-gb/services/cognitive-services/computer-vision/) is an API which analyses images. It can be used Categorise Images, detect human faces , OCR and even flag adult content.

In addition to the Computer Vision service there is Custom Vision Service available at [https://customvision.ai/](https://customvision.ai/) which is a portal to build domain specific models. Once trained this can be used for you own Content Moderation. Image Classification and Categorisation would be possible using these Image services for applications where the users are providing images or content.

### Knowledge ###

[Azure Knowledge](https://azure.microsoft.com/en-gb/services/cognitive-services/directory/know/) services offer a cortana template for building recommendation engines for ecommerce sites. The [QNA Maker API](https://azure.microsoft.com/en-gb/services/cognitive-services/qna-maker/) is a impressive tool which will scan a existing websites FAQ section and generate knowledge bases in the cloud and a Bot to answer the questions. It uses natural language processing too assist in matching the questions to the answers.

[Azure Search](https://azure.microsoft.com/en-gb/services/search/) has been enhanced with AI tooling to produce Azure Cognitive Search. This uses the cognitive services too analyses content and data to produce search indexes. [Custom Skills](https://docs.microsoft.com/en-us/azure/search/cognitive-search-create-custom-skill-example) can be plugged into the search analysis to add further insight and structure to the data.

### Language ###

[Azure Text Analytics](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) analyses sections of text for sentiment analysis, key phrase extraction and language detection with currently 120 different languages supported.

[LUIS](https://www.luis.ai/) - Language Understanding Intelligent Service uses machine learning to recognise entities in a sentence and identify the intent of the statement or question. LUIS is trained and the more information put in the model the more accurate the results. It also records the utterances it receives so the model can be improved with actual user input.

Creating BOTS backed by Natural Language processing LUIS can enable more fluid communication and understanding of complexities of questions users sometimes ask. As the models are developed and trained the services can route to the required content or products more accurately.

### Speech ###

[Speech Services](https://azure.microsoft.com/en-gb/services/cognitive-services/directory/speech/) offer Speech to Text, Text to Speech , Speech Translation and Speaker Recognition features. 

Speech interaction opens up new opportunities with accessibility or localisation, allowing users to talk to you website or application in the language of their choice is very powerful. Partially sighted of blind users could use speech and text reader to access the services they require.

Imagine a Business MI application enhanced by using speech or bots to access KPI or summary performance data. Used in conjunction with an MI tool important information could be accessed and analysed far quicker.


### Combining Services ###

The real power comes form combining these services to work together to provide powerful interactions and learning. Many of the services are using Machine Learning behind the scenes , but can also be combined with additional machine learning services to drive improved interactions.

Using LUIS to understand intent can enhance a chatbot written in the Bot Framework, coupled with image processing the bot can recognise, moderate and categorise  uploaded images. The Azure cognitive search can use custom skill to access cognitive services to extract domain specific data from content and files, this can then be combined with LUIS and the bot framework to allow a user to navigate and search data via a bot dialogue.


## Conclusion

The AI Platform and Azure Cognitive services offer web and application developers affordable access to complex and advanced AI services. Adding Cognitive Services to an application or website opens up multiple channels of communication with users which improves as the services learn.

Applications of any kind can benefit from improved communication with the users, reduced administration of content, more intelligent targeting of information and up-selling and 'learning' users behaviour.

The use cases opened up by Cognitive Services as vast and application development in the coming years will be transformed as they enter more mainstream usage. The key benefit is accessibility and affordability of complex AI services which previously not been possible.

## Resource and Links 

[Cognitive Service Docs](https://azure.microsoft.com/en-us/services/cognitive-services/)

[Overview of Microsoft AI Services](https://azure.microsoft.com/en-us/overview/ai-platform/)

[AI Services Workshop](https://github.com/martinkearn/AI-Services-Workshop)



