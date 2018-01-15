---
title: "New Website Checklist"
date: 2017-09-12T12:03:31Z
draft: true
tags: ["checklist","productivity"]
---

Some of the Big Hitters to check when starting a new website project

### Images

Images are crucial for any modern website, but I have sometimes found the process for managing the images and matching to content on the website can be overlooked. Some questions I always try and ask in the early stages of a new website project are;

Where are images sourced from, is there an image management tool or are they manually uploaded? How will the images be refreshed? If they are being sourced from a external source what is the latency and can then by loaded into a CDN?

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

Is there an existing site

Are user being imported - passwords etc

Is user / order history being imported

### Housekeeping & Maintenance

When can data be archive?

Logging Levels & retention

Inactive users and associated data

Focus on getting a site out their - can lead to early failures.


### Search

How complicated?

Result Count

Performance

What Data