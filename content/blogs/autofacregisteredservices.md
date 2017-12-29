---
title: "Autofac Registered Services"
date: 2017-06-21T21:13:03Z
draft: true
---

I was trying to debug and issue with Autofac this week I wanted to be able to display the services that had been registered, more for peace of mind that this wasn't the issue really.

I found this handy code snippet to display the registered services;

`using(var scope = _container.BeginLifetimeScope()) {
 var services = _container.ComponentRegistry.Registrations;
 var log = scope.Resolve();
 foreach(var service in services) {
  foreach(var innerservice in service.Services) {
   log.Info(string.Format("service name {0}", innerservice.Description));
  }
 }
}`

  
This was really handy for validating everything had registered across all the autofac modules as expected.