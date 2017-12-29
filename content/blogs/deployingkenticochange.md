---
title: "Deploying Changes with Kentico"
date: 2017-03-16T20:48:19Z
draft: true
---

Modern development techniques involve moving change between environments, a typical life cycle is Local -> Development -> QA/Staging -> Production. Being able to package up a set of changes, apply a version number, and then migrate move that along the environment path is crucial to a resilient and reliable development process.

There is a wide range of tooling available for migrating change between environments for the .Net code used within the Kentico project. These tools can be used to move the changes to the website file system along with any bespoke code added to the Visual Studio solution.

Crucially Kentico also stores structural information in the database which the file system changes are dependent upon and this needs to be migrated between environments in parallel to the file system changes. 

The challenge to building an effective Continuous Integration process for Kentico has been synchronising file system and database system change between developers local environments onto an integrated development environment, then onto QA and Production.

Kentico has been providing more and more tooling over recent versions as a way to migrate change between environments, the following are some of the possible approaches.

### Manual

The simplest way to manage change is to record the changes made to a Kentico Environment in spreadsheet or equivalent and then manually reapply these to the other environments when required. This technique is not recommended as is time consuming and error prone, the environments are likely to become inconsistent very quickly.

There are situations when this maybe the only option available for example access to environments or applying a very small change to a legacy site, it is not a practical solution for a team of developers producing multiple changes.

**Imports/Exports**

The first of the automated tools is the Kentico Import/Export process which has been in Kentico since the early versions. This can be accessed from the Kentico Admin section and allows everything from a single object too full site to be extracted into a collection of data files. These files can then be imported into the required environments.

This is an established approach to migration and is currently the best way to extract and migrate an entire site.

It is manual process though which can be slow for smaller changes, it is difficult to isolate a single developers change in the extract so the file contains more objects than required. This can lead to conflicts when importing and the files are very large to store in a version control system with no ordering process available for applying the import files. 

For more information on the Import and Export process the documentation is here [Kentico Import and Export Documentation](https://docs.kentico.com/display/K9/Exporting+and+importing+sites).

### Content Staging

 Version 8 of Kentico introduced [Content Staging](https://docs.kentico.com/k10/deploying-websites/content-staging) , this process tracks change to content and Kentico objects and then allows that change to be selectively migrate to other environments. This process is bi-directional so content created on a QA environment can be synchronised down to the development environment.

The process is based on web services so each of the environments need to be able to communicate with the next one in the chain via HTTP. This is usually fine for local and development environments, but can prove more challenging for QA and Production environments where access maybe restricted.

When using Content Staging it is important to turn it on as soon as possible so it can track change, it is possible to do this without having the target a server available. The URL can be added at a later date and the change synchronised.

[Content Staging](https://docs.kentico.com/k10/deploying-websites/content-staging) tracks a mix of developer and content creator change so filtering is available to allow each of the target change sets to be separated out and migrated. Version 9 introduced the concept of grouping change and then migrating that group to another environment [https://docs.kentico.com/k9/deploying-websites/content-staging/synchronizing-the-content](https://docs.kentico.com/k9/deploying-websites/content-staging/synchronizing-the-content)

By default Content Staging captures a wide range of change, and the tracked list can grow significantly over time. It is advisable to housekeep this list to only include required change. The tracked change is order dependant so a Create task must come before an Edit task for example. It is possible to programmatically filter out unrequired change so that managing the migrations becomes more efficient this document [https://docs.kentico.com/k9/custom-development/handling-global-events/excluding-content-from-staging-and-integration](https://docs.kentico.com/k9/custom-development/handling-global-events/excluding-content-from-staging-and-integration) describes the process in more detail.

**Continuous Integration**

 Continuous Integration was introduced in version 9 and improved in version 10, this works on a similar principal to content staging in that changes are automatically tracked but differs in that this changes is serialized into xml files on the file system. These files can then be checked into the source control system and shipped with the rest of the file system changes. In the bin folder of the Kentico website is a command line tool that can be used to apply these change files to the database.

This is a developer focused tool which has enabled developers to use a local copy of the Kentico database and synchronise changes between themselves, and then on up to development. It also supports working on multiple branches on the same local environment with the Kentico database change being reapplied or removed when switching between environments. It has a negative impact on performance so should not be used on production environments.

The golden rule of working with continuous integration is to run the command line tool when ever a branch is changed, committed or pulled.

On my projects we use Continuous Integration to manage the change between local copies of Kentico and then as part of the build and deployment process up to the development environment. This is achieved by running the command line tool on the web server after the deployment, but does restrict us to just one webserver for the development environment. This is because the CI process is server specific so in a web farm scenario there is two servers pointing to one database which the CI process does not currently support. Theoretically it is possible to use the CI restore process on a development web farm if the CI process is disabled on the development database, although this is untested by the author.

For the environments after development we use Content Staging and have to perform this synchronisation as a manual step following the build and deployment process. It is a quick process and does not cause a lengthy delay but means the build process cannot be fully automated.

Continuous Integration is a great tool but does need to be set up correctly and used with care, the Kentico instructions should be followed carefully [https://docs.kentico.com/k10/developing-websites/preparing-your-environment-for-team-development/setting-up-continuous-integration](https://docs.kentico.com/k10/developing-websites/preparing-your-environment-for-team-development/setting-up-continuous-integration). 

### Compare

 Compare for Kentico is a partner developed tool which allows the visual comparison of two instances of Kentico, and facilitate the synchronisation of the environments.

This tool is extremely useful when inheriting a Kentico previously unknown application or applying the previously discussed change control techniques to a legacy system. In these scenarios it is important to understand the differences between the environments and ensure they are synchronised before implementing a change control pipeline.

It is also very useful when for debugging environment that are behaving differently. Compare requires agents to be installed on each of the environments to work.

The Search for Compare tool is free to use but the Compare for Kentico is a paid for tool.

### Kentico Draft

 Kentico draft is an offering from the Kentico Cloud suite , and is not strictly a tool for managing change, but does allow content to be created outside of the Kentico application and then migrated over.

It is a productivity tool that allows development teams and content creators to define structures and create content in a cloud based tool while the main application is being developed. When the main application is ready the content can be migrated over.

One of the major benefits of the using the Kentico Cloud tooling is that content can be managed in one place and accessed via an API. This means the content can be used across system not just kentico. [Kentico Cloud Management](https://kenticocloud.com/content-management) acts as a content hub so in the context of this article could be used to move content between different environments of the same application, or to import or migrate content form other systems.

The [Kentico Delivery API](https://developer.kenticocloud.com/v1.0/docs/using-delivery-api) allows the content to be accessed via a RESTful API enabling it to be easily moved between environments. The other exciting feature is the ability to act as a Headless CMS allowing content to be accessed from any language or platform.

When using Kentico Draft it is possible to move the file system changes via a CI pipeline and then move content via the Kentico Delivery API.

**Future**

Content Staging and continuous Integration when used together have vastly improved the process of managing change between environments. This has facilitated the creation of continuous Integration and Delivery Pipelines for Kentico Projects.

There are still some challenges that cannot be met, versioning a change set is difficult. Tools such as Octopus Deploy and Microsoft Release Manager can be used to create packages that have version numbers assigned which can then be migrated up through environments. For Kentico there still needs to a manual selection of the change and this is not able to be included into the packages.

Fully automated one click deployments are also not possible currently when using Content Staging as this step has to be done manually.

The ideal scenario is a change set of both file system and Kentico change can be grouped together, apply a version number, and then deploy to each environment. This would provide confidence in exactly what each release will change and the resilience in that the change will have been tested on previous environments.

Fully automated pipelines like this allow the release control to be taken away from the development team and empower the test and product teams to approve releases. One click tools mean that a user authorises a release with one click and it is applied to the environment.

With the recent developments in Kentico Change control hopefully this functionality will be in the near future and true Continuous Deployment can be achieved.