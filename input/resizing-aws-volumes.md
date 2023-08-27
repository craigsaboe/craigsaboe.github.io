---
layout: post
title: Resizing AWS Volumes Of A Linux VM
author: @craigsaboe
published: 2021-08-30 10:48:00
---

Title: Resizing AWS Volumes Of A Linux VM
Date: 2021-08-30 10:48:00
Modified: 2021-08-30 10:48:00
Category: 
Tags: AWS
Summary: 
Status: published


I needed to add drive space to a partition of a Kali Linux VM I was hosting in AWS. After adding space to the VM in the AWS console, the partition has to be expanded to actually make use of that space, requiring a bit of console work.

Starting Out:

<code>df -hT</code>

![Alt text](/images/resize-aws-volumes/1.png "Optional title")

<code>lsblk</code>

![Alt text](/images/resize-aws-volumes/2.png "Optional title")

* Vol was 12GB, now 25GB
* xvda shows 25GB after expanding disk in AWS console, but xvda1 still is 12GB

<code>sudo growpart /dev/xvda</code>

![Alt text](/images/resize-aws-volumes/3.png "Optional title")

<code>lsblk</code>

![Alt text](/images/resize-aws-volumes/4.png "Optional title")

* xvda1 now shows 24.9GB size
* df -h will still show partition size of 12GB

<code>sudo resize2fs /dev/xvda1</code>

![Alt text](/images/resize-aws-volumes/5.png "Optional title")

<code>df -h</code>

![Alt text](/images/resize-aws-volumes/6.png "Optional title")

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html?icmpid=docs_ec2_console