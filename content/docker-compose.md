---
layout: post
title: Docker Compose
author: @craigsaboe
published: 2022-05-24 10:50:00
---

# Running multi-container Docker apps
- Define docker-compose.yml file
```
version: "3.9"  # optional since v1.27.0
services:
  web:
    build: .
    ports:
      - "8000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```
- Run "docker-compose up"