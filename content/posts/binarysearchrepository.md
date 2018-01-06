---
title: "Binary Search of a Repository"
date: 2017-04-21T13:29:24Z
draft: false
tags: ["tips","productivity"]
---

Sometimes an innocuous change can cause issues on a project at a later date, especially in scenarios when working with an application such as a CMS with lots of black box code.

A useful technique when an issue is occurring and there is no obvious cause is to employ a [Binary Search Algorithm](https://en.wikipedia.org/wiki/Binary_search_algorithm) on the repository.

This technique is also known as a half interval search, involves reverting the repository to the last known working point and verifying the issue is not present. 

Then move to the commit halfway between the last known working point and the last commit, if the issue is present then you know the cause is in the first half of the commits, if the issue is not present then the issue is in the second half of the commits.

The same process is then applied to the half way point of the commits which contain the issue, repeating until the number of commits has been reduced to a manageable level.

A tool like [Git Extensions](https://sourceforge.net/projects/gitextensions/) can be used to compare the few commits where the issue is known to start to see what has changed.

This approach works well when there are no clues to what is causing the issue, and can save lots of time with a trial and error approach.

It is recommended to use this technique on a completely fresh checkout to maintain the integrity of the local repository.

### Real World Scenario

On a recent project the webforms async setting had been set on the web forms master page in February. In May it was discovered that a Resource String helper provided by the CMS was not working. Using the binary search technique helped us to zero on this change and then understand why this had broken the resource code.