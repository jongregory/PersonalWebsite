---
title: "Simple Power Shell Deployment"
date: 2017-06-08T20:24:36Z
draft: true
---

Sometime on projects there  it isn't possible to put in a decent CI process, this maybe due to time, budget or security policy on the servers.

For these situations I use this powershell script as a fallback to provide a robust method for deploying a website.

Its reads a config file of locations and IIS settings per environment using a naming convention, and delploys a version named folder from a staging location to the web site.

The application pool is stopped and started and the files are deployed to version folder with the IIS website pointed to the new version folder. This provides a backup and easy rollback to the previous release.

It also manages any junction links for media folders etc that are not part of the deployment.

I don't have to use this very often thankfully but this is a handy script to keep available to use a base when required.

The Repo is available here : [https://github.com/jongregory/SimpleDeploymentScript](https://github.com/jongregory/SimpleDeploymentScript "Simple Deployment Script Repo")

