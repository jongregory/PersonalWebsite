---
title: "C# Importance of Checking for NULLs"
date: 2016-08-21T14:08:11Z
draft: false
tags: ["tips","cs"]
---

This week I was reviewing some C# code where the developer had used 'ToString()' throughout on properties without checking for nulls. 

The result of this was a log file full of _**'System.NullReferenceException: Object reference not set to an instance of an object.'**_

And it was difficult to trace through where the error had occurred and the logic stopped executing.

So I put together a few simple samples of how to safely check for nulls and work with collections,  I can distribute them to the training developers and add hope to add more to this project over time. The code is  available here;

[https://github.com/jongregory/DotNetFoundation](https://github.com/jongregory/DotNetFoundation)

Some of the samples are below.

**Examples Ways to handle null values**

_AS Operator_

{{< highlight csharp >}}
//[https://msdn.microsoft.com/en-us/library/cscsdfbt.aspx](https://msdn.microsoft.com/en-us/library/cscsdfbt.aspx)

var asOperator = classWithNulls.IamNull as string;
Console.WriteLine("Null is returned by as with no exception : " + asOperator);

{{< / highlight >}}

_Convert Class_

{{< highlight csharp>}}
// [https://msdn.microsoft.com/en-us/library/system.convert](https://msdn.microsoft.com/en-us/library/system.convert)(v=vs.110).aspx

var convertToString = Convert.ToString(classWithNulls.IamNull);
Console.WriteLine("Convert Class returns empty string if null no exception : " + convertToString);

{{< / highlight >}}

_Coalesce Operator_

{{< highlight csharp >}}
//https://msdn.microsoft.com/en-GB/library/ms173224.aspx

var coalesce = classWithNulls.IamNull ?? "DefaultValueIfNull";
Console.WriteLine("DefaultValue is returned if null : " + coalesce);

{{< / highlight >}}

_Conditional Operator_

{{< highlight csharp >}}
//https://msdn.microsoft.com/en-gb/library/ty67wk28.aspx

var conditional = classWithNulls.IamNull != null
    ? classWithNulls.IamNull.ToString()
    : "DefaultValueIfNull";

Console.WriteLine("DefaultValue is returned if null : " + conditional);

// C# 6 and later null propagation operator where the null value is passed up the chain without an exception
//https://msdn.microsoft.com/en-GB/library/dn986595.aspx

var conditionalCSharp6 = classWithNulls.IamNull?.ToString();

Console.WriteLine("Null is propagated and returned without an Exception" + conditionalCSharp6);

// This can be combined with Coalesce to remove the null and provide a default value
var conditionalCSharp6DefaultValue = classWithNulls.IamNull?.ToString() ?? "DefaultValueIfNull";
Console.WriteLine("Default Value Returned without an Exception" + conditionalCSharp6DefaultValue);

{{< / highlight >}}

_Extension Method_

{{< highlight csharp >}}
public static class Extension
    {
        public static string ToStringOrEmpty(this Object value)
        {
            return value == null ? "" : value.ToString();
        }
    }

// A custom extension method attached to object to handle null values, see file ToStringOrEmpty.cs
// https://msdn.microsoft.com/en-gb/library/bb383977.aspx

var extensionMethod = classWithNulls.IamNull.ToStringOrEmpty();
Console.WriteLine("String Empty is returned by as with no exception : " + extensionMethod);

{{< / highlight >}}