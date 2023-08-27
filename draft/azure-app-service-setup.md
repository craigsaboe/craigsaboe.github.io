---
layout: post
title: Starting Up a New Azure App Service Instance
author: @craigsaboe
published: 2022-07-07 15:11:00
---

* Create > Marketplace > "Web App for Containers"
* Publish: [x] Docker Container
* App Service Plan:
  * If you don't have one, can be helpful to define one for general use that maps to something like the B1:1 instance or whatever is the lowest-end dev box (for testing purposes) - you can bump it to a higher level for testing or prod later on.

Setting Up CD From Azure Container Repo
* Deployment > Deployment Center
* Settings:
  * Registry source: ACR
  * Authentication: Admin credentials
  * Registry: [your ACR's name]
  * Image: [image set in that registry]
  * Tag: [latest is probably best for CD, I think]
  * Continuous Deployment: [on]

