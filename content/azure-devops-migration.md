---
layout: post
title: Azure DevOps - Quick Git Migration
author: @craigsaboe
published: 2022-09-22 14:50:00
---


## Quick Migration from another Git host to Azure DevOps project
- [your-org] == Your organization name in Azure DevOps
- [project-name] == Project name
- [repo-name] == Default is just [project-name] but you can specify something different if hosting multiple in the same project

``` 
> git remote add azure https://[your-org]@dev.azure.com/[your-org]/[project-name]/_git/[repo-name]
> git push -u azure --all
> git remote remove origin
> git remote rename azure origin
```

Verify that your remotes are correct:
```
> git remote -v
```

You can use ADO's "Import Repository" functionality if it's a publicly-available source or just uses basic auth, I believe, but this won't work for GitHub or other providers.