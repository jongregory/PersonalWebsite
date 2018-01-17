---
title: "New Website Checklist - Part 2 Content"
date: 2017-08-24T12:03:31Z
draft: false
tags: ["checklist","productivity"]
---


### Content

All website have content and the creation and maintenance of  this content is important to understand early on?

1. *Where is the content coming from?* Are the any external systems such as a PIM, or multiple sources that need to be merged. 
3. *Content Production* - Is it being imported and then enhanced on one environment and then being migrated to another? In some cases content or product information is imported in a raw format and then is enhanced into web suitable format by content creators. 
4. *How often does it need to be refreshed?* - Who should trigger the refresh of content and will this affect the site performance? Are there any issues around delayed updates such as price or availability? Is a rollback strategy required?
5. *Data ownership across multiple applications*, what happens when data is changed and how is it propagated across the system. Is the flow of content bi-directional? Whats the frequency of the flow?
6. *[Command Query Separation](https://www.martinfowler.com/bliki/CommandQuerySeparation.html) principle* - Content or products may be drawn from one environment, but commands (Orders etc) may need to be sent to another - Draw content or products from a production source for enhancement in a staging website but need to send Orders back into a QA/Test infrastructure to prevent false order. Separation of bi-directional services are ideal for this scenario.
7. *Deletion Strategy* - When content or products are deleted from the website do they need to be soft or hard deleted? How should the URL and redirect be handled for the SEO best practice? If content or products are being imported would this override the deletion?

[**Prev** - Part 1 Images](/posts/checklist-new-website-images/)

[**Next** - Part 3 Payment](/posts/checklist-new-website-payment/)