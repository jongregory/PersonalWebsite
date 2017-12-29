---
title: "Sql Server Management Studio Results to Excel"
date: 2016-07-27T21:07:19Z
draft: true
---

I need to do some quick analysis on a error log table, so was running a grouping query on the log table.

To get the results into excel I wanted to cut and paste the results from SSMS query window into excel.

Annoyingly the .Net Exceptions where going into Excel on new rows which made it unreadable. 

This post had the answer, [https://www.mssqltips.com/sqlservertip/3416/line-split-issues-when-copying-data-from-sql-server-to-excel/](https://www.mssqltips.com/sqlservertip/3416/line-split-issues-when-copying-data-from-sql-server-to-excel/)

With SQL 2012 the line feeds and carriage returns are preseved  and needed to be filtered out in the query

`SELECT COUNT(*) as count, replace(replace(Message, char(10), ''''), char(13), '''') as ''Message'' FROM Log`