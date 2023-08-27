---
layout: post
title: Getting SCP Access to a VM hosted by Google Cloud Platform
author: @craigsaboe
published: 2022-07-12 09:01:00
---

# Accessing files on a VM hosted in GCP 

## Generate an SSH key if needed
```
> mkdir C:\Users\WINDOWS_USER\.ssh\
> ssh-keygen -t rsa -f C:\Users\WINDOWS_USER\.ssh\KEY_FILENAME -C USERNAME -b 2048
```
Replace:
- WINDOWS_USER = your AD username
- KEY_FILENAME = whatever filename you want
- USERNAME = your username on the VM

This gives you:
- KEY_FILENAME (your private key)
- KEY_FILENAME.pub (your public key)

Ex. public key:
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDAu5kKQCPF... cloudysanfrancisco
```

src: https://cloud.google.com/compute/docs/connect/create-ssh-keys

## Add SSH key to project
- Google Cloud Console > Metadata
- Edit, then Add
- Paste in contents of public key file

src: https://cloud.google.com/compute/docs/connect/add-ssh-keys#add_ssh_keys_to_project_metadata

## Access VM from WinSCP
- Get external IP for VM from Google Cloud console > VM Instances
- Open WinSCP
  - File Protocol: SCP
  - Hostname: [external IP]
  - Username: [Google username for project]
  - Click Advanced
  - SSH > Authentication
    - Select private key in "Private key file:" file selection box
    - May get a WinSCP dialog to change the type of key to a .PPK file - if this occurs, do so
  - Click OK
- Login should now work successfully

## Access VM from Windows 10 SSH client
```
> ssh -i C:\Users\WINDOWS_USER\.ssh\KEY_FILENAME USERNAME@IP_ADDRESS
```
https://www.maketecheasier.com/use-windows10-openssh-client/

