---
title: "Microsoft AI Event"
date: 2018-04-01T09:27:27Z
draft: true
---

Microsoft Hands On AI Event - Thursday 1st March Birmingham

I recently attended a great event in Birmingham hosted by <> where Microsoft demonstrated the Azure Cognitive Services.

Email - jongregoryaiday@hotmail.com - windowcleaner10

Quick Notes

* Day of hands on guided labs - available on GitHub
* MS do one to one hacks with companies for 3-5 days to generate POC real world POC samples
* Humans  + machines = ultimate intelligence
* Data and Machine Learning
* Cognitive Computing (api into machine learning)
* Conversation as a service
* ML - analyses data and finds patterns
* ML - Good use case slide on notes
* Rolls Royce using ML for predictive engine servicing
* Cognitive Services - can use ML without having to know ML uses API's
* 30+ Apis (Vision / Language (NLP) / ...
* Language is the new UI - Bots are the new apps

VISION Section

* Vision - dog vs blueberry muffin - can categorise images and do OCR
* https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/
* https://github.com/martinkearn/ai-services-workshop
* Face detection, recognition and emotion and age guess, gender
* Cherry Bot - fun engagement app for football - does content moderation so people cannot upload rude selfies
* Video Indexer - content tagging, sentiment analysis and face detection
* Custom Vision - https://customvision.ai/ - domain specific - can build you own model - sample use makaton app to request the sign for a word
* POC - Don't publicise - http://makaton.azurewebsites.net/
* Facial recognition returns JSON of attributes and values it has recognised
* Could do a brown bag on the makaton recognition samples of rabbit / sleep

KNOWLEDGE Services

* @martinkearn 
* cortana solutions template - can deploy a recommendation framework on azure subscription (item to item & personalised recommendations) - ideal for ecommerce sites
* Natural Langauge FAQ - really great exmaple for pluging in a website FAQ service
* Experience Learning - realtime, dynamic decision making, learns based on user actions - adapts content based on learning
* https://qnamaker.ai/ - create bot from an existing website FAQ
* http://aka.ms/recotemplate - recommendation engine template - this was more involved - wasn't able to get this working due to wifi speed but demos a  recommendaton machine learning for books - used files from the sample repo
* http://martink.me/


SPEECH Services

* @daltskin
* demo live subtitles from speech into french
* higher accuracy than humans apparently - switchboard test proves this
* aka.ms/speechswitchboardtest
* Translator speech - speaker recognition - bing speech
* bing speech - sdk and api available for audio to text - built on contana tech so can make your owb digital assitant
* Lewis? intent detection
* Black Radley - bing speech POC - facial recognition to play for kids or OAP in museums to play different audio for exhibits
* https://www.microsoft.com/en-us/research/blog/
* speaker recognition - voice is your passport - https://www.microsoft.com/en-us/translator/default.aspx
* Custom Speech - language model and acoustic model - so can support custom language models - can help with technical or domain specific words - also help to filter out background noise in industrial environments - video showed the star commander game which uses lots of complex domain specific words
* Claims MS is the best speech recognition available at the moment


LANGUAGE Services

* Text Analytics - sentiment analysis, key phrase extraction, language detection (120 different languages) - https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/ - can do advanced spell check driven from bing search words
* LUIS Language Understanding Intelligent Service - https://azure.microsoft.com/en-us/services/cognitive-services/language-understanding-intelligent-service/
* https://www.luis.ai/ - couldn't get this to work with in private browsing window / wifi issues
* Will need to work through luis demo on my own - was training the tool with phrases to find patients /  spare beds
* Intent / Entities

BOTS and Conversational Apps

* 85% of time in just 5 apps
* Bots are rest apis
* Cortana Intelligence Suite - Data coming in - enhancing it - accssing it
* Also know as Azure Bot Service - name used interchangeably, azure bot has mainly the same components - plus more
* Key point is you can build the bot once then target multiple platforms - not platform specific 
* supports Skype, slack, skype for business, email, sms
* PAAS offering and a functions based offering
* BOT Scenarios - Infortion REtrievel (FAQ), Commercial Transactions (buy tickets), Digital Agents and IoT ( House Control )
* Bots can send out notifications and get much higher user engagement than email
* Two flavours of bot sdk - .net and JS
* Bot Builder SDK - recommend using application insights to get telementory
* Got lots of samples on GitHub - there is a bridge for alexa
* An emulator for debugging
* used the markdown instructions in the github bot folder - will need to run this through again as got errors due to wifi and time
* This one descended into madness a little bit

MACHINE Learning

* Mason Cusack
* Talk focused applying machine learning not defining what machine learning is
* ML development tool allows developers consume ML without an in depth knowledge of the low level mathematics
* https://studio.azureml.net/
* Supervised & unsupervised learning - Reinforcement
* Stressed to don't believe the hype - ML is accessible and has been around in research for a long time - classical ML can solve many problems so need to dive into implementing deep learning
* tried to follow this one along but my join of datasets didn't produce any results so missed a step - he ran out of time so switched to a one made earlier model - again need to revisit this one

