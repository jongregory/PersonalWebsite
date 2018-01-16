---
title: "New Website Checklist - Part 7 Security"
date: 2017-11-19T12:03:31Z
draft: true
tags: ["checklist","productivity"]
---


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

[**Prev** - Part 6 Search](/posts/checklist-new-website-search/)