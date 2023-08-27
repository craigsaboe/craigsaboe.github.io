---
layout: post
title: Verify that an ID is both a valid integer and exists in a given table?
author: @craigsaboe
published: 2021-08-30 10:48:00
---

Title: Verify that an ID is both a valid integer and exists in a given table?
Date: 2021-08-30 10:48:00
Modified: 2021-08-30 10:48:00
Category: 
Tags: 
Slug: 
Summary: 
Status: published


This is a simple query to validate whether a given ID exists in a table.  It will return 1/0 for true/false, and won't blow up if someone keys in an ID that is something not CONVERT-able to an integer (I wasn't aware of the TRY_CONVERT function, very convenient - see https://docs.microsoft.com/en-us/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-ver15).

```
SELECT
    CASE WHEN EXISTS 
    (
        SELECT CompNo FROM dbo.Companies WHERE CompNo = TRY_CONVERT(smallint, @companyId)
    )
    THEN 1
    ELSE 0
END
```