---
title: "New Website Checklist - Part 3 Payment"
date: 2017-09-22T12:03:31Z
draft: true
tags: ["checklist","productivity"]
---

Some of the Big Hitters to check when starting a new website project

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

[**Prev** - Part 2 Content](/posts/checklist-new-website-content/)

[**Next** - Part 4 Migration](/posts/checklist-new-website-migration/)