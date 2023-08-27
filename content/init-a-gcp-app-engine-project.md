---
layout: post
title: Set up a GCP App Engine Project with Azure Pipeline Deployment
author: @craigsaboe
published: 2022-05-18
---

# Create A GCP Project
- Create new cloud project
- Create new App Engine app: "App Engine" > "Create Application"
- On the "Get started" pane, select "I'LL DO THIS LATER" - will get set up w/ the Azure Pipeline

# Ensure Correct APIs Enabled With Credentials And Permissions
![API & Services](../images/gcp-azure-setup/api_and_services.png)
- "Cloud Console" > "API & Services"
  - Select "ENABLE APIS AND SERVICES" at top of page
  - Need App Engine Admin API, Google App Engine Flexible Environment and Service Management API
  - Select "Credentials" from left nav pane
  - Create an account
  - Create a JSON key for that account
    - Automatically will download a file like 'azure-gcp-test-[Some ID].json':
```
{
  "type": "service_account",
  "project_id": "azuregcp-test",
  "private_key_id": "SOME ID STRING",
  "private_key": "-----BEGIN PRIVATE KEY-----\SOME LONG PRIVATE KEY=\n-----END PRIVATE KEY-----\n",
  "client_email": "azuregcp-test@appspot.gserviceaccount.com",
  "client_id": "NUMERIC CLIENT ID",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/azuregcp-test%40appspot.gserviceaccount.com"
}
```
  - Add permissions:
    - App Engine Deployer - To deploy new code to App Engine.
    - Cloud Build Editor - Needed to be able to use gcloud tool to deploy.
    - Storage Admin - Needed to be able to use gcloud tool to deploy.
    - Service Account User - To run operations as the service account.
    - App Engine Service Admin - To upgrade our new version to the default version.

# Add Azure Service Connection
- "Project Settings" > "Pipelines" > Service Connections > New service connection
- Create "Docker Registry"
  - "Docker Registry": https://gcr.io/(PROJECT_ID)
  - "Docker ID": _json_key
  - "Docker Password": (paste the **entire contents** of the json file)

# Create A Test App
- Create a new project folder and "dotnet new webapp"
- Modify Program.cs to look like this (.NET 6 style):
```
var builder = WebApplication.CreateBuilder(args);

// https://cloud.google.com/appengine/docs/flexible/custom-runtimes/build#listening_to_port_8080
// code from: https://github.com/GoogleCloudPlatform/getting-started-dotnet/blob/master/HelloWorld/Program.cs

// Google App Engine sets the PORT environment variable - this ensures we are listening to the correct PORT.
if (!string.IsNullOrEmpty(Environment.GetEnvironmentVariable("PORT")))
{
    builder.WebHost.UseUrls($"http://0.0.0.0:{Environment.GetEnvironmentVariable("PORT")}");
}

// Add services to the container.
builder.Services.AddRazorPages();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error");
    // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapRazorPages();

app.Run();
```
- Create a Dockerfile as well (make sure you replace the DLL with your app's name.)
```
# https://docs.docker.com/engine/examples/dotnetcore/

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "AzureGCP-test.dll"] 
```
- Create a app.yaml file as well.
```
runtime: custom
env: flex

# The settings below are to reduce costs during testing and are not appropriate for production use. For more information, see:
#   https://cloud.google.com/appengine/docs/flexible/dotnet/configuring-your-app-with-app-yaml
# Reference: https://github.com/GoogleCloudPlatform/dotnet-docs-samples/blob/master/appengine/flexible/HelloWorld/app.yaml
manual_scaling:
  instances: 1
resources:
  cpu: 1
  memory_gb: 0.5
  disk_size_gb: 10
```

# Create the ADO Pipeline
- Create a new pipeline with a type of "Azure Repos Git", pick the right repository and configure for a Docker image
- Change the definition to look like this (so it can use the GCP service connection):
```
# Docker
# Build a Docker image
# https://docs.microsoft.com/azure/devops/pipelines/languages/docker

trigger:
- master

resources:
- repo: self

variables:
  tag: '$(Build.BuildId)'

stages:
- stage: Build
  displayName: Build image
  jobs:
  - job: Build
    displayName: Build
    pool:
      vmImage: ubuntu-latest
    steps:
    - task: Docker@2
      inputs:
        containerRegistry: 'GoogleContainerRegistry'
        repository: 'AzureGCP-Test/AzureGCP-Test'
        command: 'buildAndPush'
        Dockerfile: '**/Dockerfile'
```

# GCP Container Registry
- Search for 'container registry' to bring up that module
- You should see the docker image listed there that you just pushed from ADO

# Add Service Credential As Secure File
- "Pipelines" > "Library" > "Secure Files"
- Upload secure credentials JSON file


# References
- https://purple.telstra.com/blog/azure-pipeline-gcp-app-engine