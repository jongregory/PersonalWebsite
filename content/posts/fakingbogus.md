---
title: "Faking and Seeding Data with Bogus"
date: 2017-12-29T10:10:43Z
draft: false
tags: ["testing","productivity"]
---

I was searching for a tool a few weeks back to help me seed some data and I found this fantastic NuGet package called [Bogus](https://www.nuget.org/packages/Bogus/). This tool lets you set up rules for a classes properties with various different data generation options.

For Example here is a some sample rules I created for a simple class where the id is generated as a unique index but the hashedcollection is passed in as a variable ;

{{< highlight csharp "linenos=table" >}}
            var comparerFake =
                new Faker<Comparer>().RuleFor(u => u.Id, f => f.UniqueIndex)
                    .RuleFor(u => u.ItemCreatedWhen, f => f.Date.Recent())
                    .RuleFor(u => u.HashedCollection, f => HashedCollection);
{{< / highlight >}}

Once the rules have been defined, I usually snaffle them away in a private method, then an instance or a collection of the class can be generated

//Generate a single instance
var classToPopulate = new ClassToPopulate();
comparerFake.Populate(classToPopulate);

//Generate a collection of ten instances
var fakeCollection = comparerFake.Generate(10);

The [API Support](https://github.com/bchavez/Bogus#bogus-api-support) for different datatypes and covers most of the ones likely to be need for most scenarios.

So far I have used this library for seeding a database with data, Testing complicated AutoMapper mappings and unit tests which operate on collections.