---
layout: post
title: Get List Of Sessions/Active Connections In PostgreSQL
author: @craigsaboe
published: 2021-08-30 10:48:00
---

Title: Get List Of Sessions/Active Connections In PostgreSQL
Date: 2021-08-30 10:48:00
Modified: 2021-08-30 10:48:00
Category: 
Tags: postgresql
Slug: 
Summary: 
Status: draft


## Query
select pid,
       usename, 
       datname, 
       client_addr, 
       application_name,
       backend_start,
       state,
       state_change
from pg_stat_activity;

Result:

## Column Definitions
- process_id - process ID of this backend
- username - name of the user logged into this backend
- database_name - name of the database this backend is connected to
- client_address - IP address of the client connected to this backend
- application_name - name of the application that is connected to this backend
- backend_start - time when this process was started. For client backends, this is the time the client connected to the server.
- state - current overall state of this backend. Possible values are:
    - active
    - idle
    - idle in transaction
    - idle in transaction (aborted)
    - fastpath function call
    - disabled
- state_change - time when the state was last changed