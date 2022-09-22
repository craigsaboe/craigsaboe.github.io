Title: Starting a Statiq site
---

[prereq: .NET Core SDK]
```
> dotnet new console --name StatiqSiteNameHere
> cd StatiqSiteNameHere
> dotnet add package Statiq.Web --version 1.0.0-beta.49
```
- Open Program.cs
- Add:
```
await Bootstrapper
  .Factory
  .CreateWeb(args)
  .RunAsync();

```
- Create a page under \input
```
Title: Something Clever
---
# Content Title
Clever musings to go here.
```
- Run: ``` > dotnet run```
- Preview ``` > dotnet run -- preview```