---
layout: post
title: "Bulk inserting data into SQL Server using C#"
date: 2016-02-15
comments: true
categories: csharp sql
---

In the last few days I had a question: what is the most fastest method to bulk insert data into a SQL Server database using C#? I decided to gather up all methods that I could find and do a very simple performance test to decide which one is the fastest.

Here are my results for inserting 10000 rows over 500 iterations:

 Method                  | Time
 ----------------------- | -------------
 `SqlBulkCopy` class     | 137.022 ms
 `bcp` utility           | 146.876 ms
 Table-Valued Parameter  | 150.900 ms
 Simple.Data             | 208.320 ms
 XQuery                  | 235.490 ms

My configuration:

- i5 M460 @ 2.53GHz
- 6GB of RAM
- 500GB 7200 RPM 16MB Cache HDD

SQL Server version:

```
Microsoft SQL Server 2014 - 12.0.2000.8 (X64)   Feb 20 2014 20:04:26   Copyright (c) Microsoft Corporation  Express Edition (64-bit) on Windows NT 6.3 <X64> (Build 9600: )
```

The first thing you may notice was the `bcp` there. Yes, `bcp` wasn't run from C# but I wanted to add to the list for comparison purposes.

Well, basically all methods listed had very similar results but if you are searching for the fastest one you choose `SqlBulkCopy`.
Moreover, the remaining methods got more than one disadvantage besides performance: the `bcp` needs to receive a `.csv` file, Table-Valued Parameter needs to have a procedure and obviously a 'Table-Valued Parameter' in the target database, `Simple.Data` needs a third party library installed, `Simple.Data` and XQuery needs a `.xml` file and also a procedure created in the database.

If you are interested in take a look at the code that generated the results [I added the test code in GitHub](https://github.com/fagnercarvalho/bulk-insert-sqlserver-csharp/blob/master/BulkInsertSqlServer/Program.cs). In the code you will see that I tested Dapper but the performance was bad and I decided to remove from the test results. I also used the `Parallel.For` method but the performance was even worse.
