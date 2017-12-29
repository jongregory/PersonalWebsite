---
title: "Kentico CMS.Tests Library - Unit Testing for Kentico Objects"
date: 2016-10-12T19:17:48Z
draft: true
---

_As i was writing this post it was added to my works blog too - with much better formatting! [http://www.mmtdigital.co.uk/blog/october-2016/unit-testing-for-kentico-objects?platform=hootsuite](http://www.mmtdigital.co.uk/blog/october-2016/unit-testing-for-kentico-objects?platform=hootsuite "MMT Digital Blog")_

One of the big difficulties I have found when working on bespoke code for a Kentico based website was writing unit tests where the code under test used Kentico objects. For example the Kentico [AddressInfo](https://devnet.kentico.com/docs/8_0/api/html/T_CMS_Ecommerce_AddressInfo.htm "AddressInfo Object Link") object being used in a custom code method. 

When writing the test an AddressInfo object would need to be created and passed in as a parameter by the test. However the creation of the object would fail without a connection string even though the database is not required. 

I have seen a few approaches where people have written wrappers around the providers classes but if you want to work with the Kentico Objects they still had the inability to create a new object.

Starting in Kentico 8 the is a hidden gem library is included called CMS.Tests which provides the solution to the problem, there is not much documentation on it but this [Kentico Article](http://devnet.kentico.com/articles/test-automation-possibilities-in-kentico-8 "Kentico Article on CMS Tests") covers everything. There is also a class reference [Class Reference](https://devnet.kentico.com/docs/8_1/api/html/N_CMS_Tests.htm "CMS Test Reference page")  document which shows all the methods and properties.

There are three test types available;

1.  Unit Tests
2.  Integration Tests
3.  Isolated Integration Tests

**Unit Tests**

As you would expect these isolate the code from the database and allow for the tests to run quickly with provided fake data.

They key thing to do is make sure the tests inherit from the UnitTests base class in CMS.Tests otherwise the Fake<> methods cannot be used.

\[TestClass\]
public class IamAUnitTest : UnitTests
{
.....

 Once that is set up it is a simple case of creating Fake<> for each Kentico Object and its provider that the test requires; 

`Fake<AddressInfo, AddressInfoProvider>()
                .WithData(new AddressInfo()
                {
                    AddressGUID = _billingAddressGuid,
                    AddressLine1 = "AddressLine1",
                    AddressLine2 = "AddressLine2",
                    AddressCity = "AddressCity",
                    AddressZip = "Postcode"
                },
                    new AddressInfo()
                    {
                        AddressGUID = _deliveryAddressGuid,
                        AddressLine1 = "AddressLine1",
                        AddressLine2 = "AddressLine2",
                        AddressCity = "AddressCity",
                        AddressZip = "Postcode"
                    });`

You can provide as many objects as you want on the .WithData() method, and then the fake provider will let you look up on ids providing realistic scenarios

var billingAddress = AddressInfoProvider.GetAddressInfo(_billingAddressGuid);

This has been really useful when testing the logic in custom methods without having to spin up the website and initiate through the UI. It is also great for edge case and exception testing to see how logic performs when you get something unexpected back from Kentico.

There is a full list of the fakeable Kentico Objects [here](http://devnet.kentico.com/getattachment/Articles/2014-04/Test-Automation-Possibilities-in-Kentico-8/Kentico8-FullyFakeableProviders.pdf "Fakeable Kentico Objects").

**Integration Tests**

These allow the code to be run against database, but doesn't require a Kentico website. As long as all the required Kentico Binaries are referenced and an App.Config file with the database connection string.

These will be slower than a Unit test but allow for more realistic scenarios. Care should be taken if the tests write data to the database as this will be harder to reset at the end of the test, and could effect database integrity.

As above the test have to inherit from the IntegrationTests base class, but there is no need to call the Fake<> method as these tests will be accessing the database.

`[TestClass]
public class IamAIntegrationTest : IntegrationTests
{
.....`

**Isolated Integration Tests**

These tests are similar to the above integration tests, except it creates a copy of the database using [SQL Server 2012 Express LocalDB](https://msdn.microsoft.com/en-us/library/hh510202(v=sql.110).aspx "SQL Server 2012 Express LocalDB") to protect from any database writes affecting the integrity of the data. The local database get refreshed with each test so these will be slow to run, they are ideal for longer integration test perhaps on a nightly build.

The logic can be tested against a clean seeded database for each test which will be repeatable on each run.

**CMS Asserts**

 There is also a [CMS Assert Methods](https://devnet.kentico.com/docs/9_0/api/html/Methods_T_CMS_Tests_CMSAssert.htm "CMS Assert Methods") set of classes that allow Kentico Specific assertions, these can be used alongside the Test framework assertion provider. An example assertion taken from the Kentico articlet is the QueryEquals method, which  checks two  SQL statements are equal.

`CMSAssert.QueryEquals(q.ToString(), "SELECT UserID FROM CMS_User");`