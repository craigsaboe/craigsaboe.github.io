---
layout: post
title: String Parsing in .NET
author: @craigsaboe
published: 2021-10-15 21:56:00
---

Title: String Parsing in .NET
Date: 2021-10-15 21:56:00
Modified: 2021-10-15 21:56:00
Category: 
Tags: 
Slug: 
Summary: 
Status: published

# C# String Parsing Bits

Some string parsing bits in C#:
```
    string lastPart = text.Substring(0, text.LastIndexOf('/')).Split('/').Last();

    Uri uri = new Uri("http://s.opencalais.com/1/pred/BusinessRelationType");
    string lastSegment = uri.Segments.Last();
```
So use a '\\' to get the end of a Windows file path! 
https://stackoverflow.com/questions/3387222/how-to-get-the-last-part-of-a-string