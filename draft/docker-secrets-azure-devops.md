---
layout: post
title: Using Docker Secrets in Azure DevOps Pipelines
author: @craigsaboe
published: 2022-05-03 14:50:00
---

- Under ADO Pipelines, select the pipeline, click Edit, then click 'Variables' at the top
    - Create needed variables and check the boxes to 'Keep this value secret'
- Modify 'azure-pipelines.yml':

Add flag for 'DOCKER_BUILDKIT':
```
variables:
  appName: 'some-app-name'
  ...(other vars)...
  DOCKER_BUILDKIT: 1
```

Add one or more steps to expose variables:
```
    - bash: |
        echo $(variable_name) > ${PIPELINE_WORKSPACE}/var_name.txt
      displayName: Store secret 1
      env:
        SECRET_KEY: $(variable_name)

```

Pass secret files in to the docker build task as "--secret" arguments
```
    - task: Docker@2
      displayName: Build an image
      inputs:
        command: build
        repository: $(imageRepository)
        dockerfile: $(dockerfilePath)
        containerRegistry: $(dockerRegistryServiceConnection)
        tags: $(tag)
        arguments: --secret id=somesecret,src=$(Pipeline.Workspace)/var_name.txt
```
- You can pass multiple secrets by repeating the same "--secret" argument


Modify dockerfile to use secret files:

- Use 'mount' at start of any RUN commands that need access to the secrets:

```
RUN --mount=type=secret,id=hf_user \
    dotnet nuget add source "https://nugetrepository/index.json" --name nugetrepo --username $(cat /run/secrets/somesecret) ...
```

- You need to use --mount for each command; it does not remain in scope.
- You can pass multiple "--mount" commands sequentially for multiple vars

## Future Edits
- Creating temp files seems a little weird, think you can probably do this a little more streamlined?
    - https://pythonspeed.com/articles/docker-build-secrets/
- Not sure how to handle local dev, it shouldn't be hard but haven't done it yet.
- Azure Key Vault could be tied into this somehow for added security - I think.

## Docs
- https://docs.docker.com/develop/develop-images/build_enhancements/#new-docker-build-secret-information
- https://stackoverflow.com/questions/70408381/docker-buildkit-returning-run-secrets-secret-id-no-such-file-or-directory
- https://stackoverflow.com/questions/66446874/right-way-to-use-secret-flag-in-docker-buildkit
- https://forums.docker.com/t/docker-using-docker-buildkit-to-pass-a-token-secret-during-build-time/104151