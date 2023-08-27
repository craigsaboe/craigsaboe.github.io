---
layout: post
title: 'Hello World' Starter Bitbucket Pipelines
author: @craigsaboe
published: 2022-05-16
---

# Basic YAML for a pipeline
- This might be mostly what BitBucket will create for you in 'Create your first pipeline' but I can't use that wizard in the current repo I'm using.

```
# This is an example Starter pipeline configuration
# Use a skeleton to build, test and deploy using manual and parallel steps
# -----
# You can specify a custom docker image from Docker Hub as your build environment.
# Temp ADO Repo Creds (REGEN AFTER TESTING THIS): csaboe / xckthsxxbx63v63n6gorrz3wuyogec6xj4pqpnqhclbrndn3esea
image: atlassian/default-image:2

pipelines:
  default:    
    - step:
        name: 'Add ADO Git Remote'
        script:
        - git remote add origin git@ssh.dev.azure.com:v3/KDG1/DCi/DCi
    - step:
        name: 'Test'
        script:
        - echo "Your testing goes here..."
    - step:
        name: 'Something Else'
        script:
        - echo "Your other action goes here..."

    # The following deployment steps will be executed for each pipeline run. To configure your steps and conditionally deploy see https://support.atlassian.com/bitbucket-cloud/docs/configure-bitbucket-pipelinesyml/
    # - step:
    #     name: 'Deployment to Staging'
    #     deployment: staging
    #     script:
    #       - echo "Your deployment to staging script goes here..."
    # - step:
    #     name: 'Deployment to Production'
    #     deployment: production
    #     trigger: 'manual'
    #     script:
    #       - echo "Your deployment to production script goes here..."
```