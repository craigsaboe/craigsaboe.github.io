---
layout: post
title: Starting and Using Azure App Service Logs
author: @craigsaboe
published: 2022-07-07 15:11:00
---

* Open the App Service instance's admin portal
* Go to Monitoring > App Service Logs
* Under Application logging, select "File System"
* Copy off the new "FTPS" path that's been created below
* Go to Deployment/Deployment credentials
* Create username + password for FTP user
* Under Monitoring/App Service logs, the new user should appear under "FTP/deployment username"

You should now be able to log in through an FTP client and pull down logs (among other things).