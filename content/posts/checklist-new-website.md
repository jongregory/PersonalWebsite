---
title: "New Website Checklist"
date: 2017-09-12T12:03:31Z
draft: true
tags: ["checklist","productivity"]
---

Some of the Big Hitters to check when starting a new website project

### Images

Images are crucial for any modern website, but I have sometimes found the process for managing the images and matching to content on the website can be overlooked. Some questions I always try and ask in the early stages of a new website project are;

Where are images sourced from, is there an image management tool or are they manually uploaded? How will the images be refreshed? If they are being sourced from an external source what is the latency and can then by loaded into a CDN?

Matching up to the content - How will the images be matched to the location in the content, multiple product images for example. Can a naming convention be used and how should a missing image be handled gracefully?

Size and Optimisation - What format will the images be supplied in, do they need to be resized or optimised automatically automatically? Can a convention be put in place to size multiple images.

### Content

All website have content and the creation and maintenance of  this content is important to understand early on?

Where is the content coming from? Are the any external systems such as a PIM, or multiple sources that need to be merged. 

Is it being enhanced on one environment and then being migrated to another? In some cases content or product information is imported in a raw format and then is enhanced into web suitable format by content creators. 

How often does it need to be refreshed? - Who should trigger the refresh of content and will this affect the site performance? Are there any issues around delayed updates such as price or availability? Is a rollback strategy required?

Data ownership across multiple applications, what happens when data is changed and how is it propagated across the system. Is the flow of content bi-directional? Whats the frequency of the flow?

[Command Query Separation](https://www.martinfowler.com/bliki/CommandQuerySeparation.html) principle - Content or products may be drawn from one environment, but commands (Orders etc) may need to be sent to another - Draw content or products from a production source for enhancement in a staging website but need to send Orders back into a QA/Test infrastructure to prevent false order. Separation of bi-directional services are ideal for this scenario.

Deletion Strategy - When content or products are deleted from the website do they need to be soft or hard deleted? How should the URL and redirect be handled for the SEO best practice? If content or products are being imported would this override the deletion?


### Payment Gateway

When considering a payment integration there are two areas I consider, the implementation and the change management.

For the implementation the aim is to segregate and simplify the payment as much as possible to reduce the risk of malicious code.

1. Segregate the code base for audit
2. Hardening - back buttons, refreshes drop outs etc
3. Responsiveness across devices, this can vary between payment providers
4. What other code is running on the payment form? JavaScript or node modules

The payment form will be under some form of PCI DSS regulation, the idea of separating this form out into its own deployment process is to isolate the PCI regulation to only the affected code, leaving the main application free from additional regulation.

1. Change management process for the payment form, is it practical to seperate
2. Can the payment form be simplified enough to have a one off manual deployment
3. Access to production server, ideally this should only be the automated deployment tools
4. Audit tracking of changes to the payment form
5. Automated Pen Testing of the payment form and malicious code checker

### Migration

When a new site is being built it is more than often replacing an existing site. This site could possibly have user information, content, order history etc that users will expect to be in place when the use the new site.

Some questions to ask during planning;

* Is there an existing site? what is the state of the data? Its there in interface or api to get the data in an out?
* Is the user being imported? Do passwords meet the new security standards? Will the hashing or encryption support migration? 
* Will user have to re-register on first login or reset password?
* Is user / order history being imported? How much historical data should be brought across? Can a archived data service be used to display historical information to the user?
* Go-live approach will it be big bang or parallel running? does data have to be synchronised between the incumbent and replacement systems and for how long?

### Housekeeping & Maintenance

Making sure a website self manages is very important to maintain performance and up time. Automatically clearing out working data and archiving ensures a clean and performant database. An extra consideration is there is a storage cost when using cloud hosting, so managing the data in expensive storage and putting other data in cheaper storage can help with the cost of runnig a cloud app.

Some questions worth asking;

1. Which data can be archived and when? Will users require access of can it be offloaded to cheaper storage.
2. What Logging Levels are required for who long and retention? Can logs be aggregated and put into cheaper storage
3. What happens to Inactive users and associated data? Can accounts be automatically expired and removed? 


### Search

Search is a crucial element of any website, but depending on the tool being used can be a difficult fit with Agile development process. If the search tool has a limited feature set then this can be a blocker mid way through development forcing the adoption of a new tool.

Some useful questions to ask;

1. How complex are the features required, over the development of the site? Will the chosen tool provide all these features? 
2. Any special features required such as Result Count?
3. What are the performance requirements for search?
4. What Data is required? Where is it coming from? How often does it change? Can the search index be added to or does a rebuild involve search downtime.

### Security

Security is a huge and ever changing topic that should be considered throughout the life of the application, there are a few questions worth asking in the early stages of the project;

1. How will the Data at Rest be secured?
2. Does all or part of the Data in Transit need to encrypted
3. What will the Password Policy be
4. Data backups and retention, will these be secured and how will GDPR be accommodated with the right to be forgotten? Is it possible to restore a encrypted database from a back up? This should be tried early on
5. What ports need to open, development and other pre prod environments should have the same port lock down as prod to prevent unexpected failures.
6. API Security and authentication, how is the application going to authenticate talk to between the various components.
7. IP restriction - which parts of the application need to be public facing and which can be ip restricted
8. DB Usernames - can multiple database users for different parts of the application to provide Least User Privileges. the public site just have read and limited writes for example.

