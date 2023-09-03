Title: Setting Up Azure Pipelines
Date: 2023-09-01 10:48:00
Modified: 2023-09-01 10:48:00
Category: 
Tags: 
Slug: 
Summary: 
Status: draft

This set of tutorials covers how to set up integration between Azure DevOps and Microsoft Azure for the purposes of continuous integration and delivery.

Specifically, we are looking at a scenario where we have a project that will be:

Using ADO for source control

Utilizing Azure Pipelines 

Containerized

Hosted in Azure

Upon completion, the following should happen:

A dev commits code changes to a "primary" branch

"Primary" just being shorthand for branches like 'QA' or 'prod' - not feature or transient branches

The branch's pipeline is triggered

The pipeline builds the application into a Dockerfile and pushes it to an Azure Container Registry

An Azure App Service for Containers instance has a webhook that is tripped whenever that specific Dockerfile is updated

That App Service instance automatically pulls down the new Dockerfile and rebuilds to put an updated Docker image into service

As you can see, this scenario automates the whole process to get every code update from the time it is pushed to source control, to the point it is actually generally available.  This has the following benefits:

The dev no longer needs to spend time and effort updating those shared instances

There's much less risk of mistakes when running through the process

Devs don't need much or any access to Azure environments - the pipeline only needs the ability to reach the container registry.  

IT can handle management of any Azure services needed because they should just need to create App Service instances and point it at a Dockerfile

They should not need to do anything with the app itself that would need code changes or developer assistance

Overview

Before any pipelines can be configured in Azure DevOps, permission must be granted to whoever is administering the ADO project, to make connections from an Azure pipeline to an Azure Container Registry.  The ACR is a secure, private service and for obvious reasons we don't allow non-authorized personnel to push Dockerfiles there.

The connection itself will be created by (most likely) a Team Lead when the project is ready to set up a pipeline.  However, in order to do this, a Team Lead (or whoever is assigned to create the connection) requires certain subscription-level AAD permissions to do so.  If they don't have them, they will receive an error like so when they try and create it:

This "User Access Administrator" permission is also required for other dev user admin actions, and is currently given to both Team Leads for the purposes of administering ADO and some aspects of Azure infrastructure.  Based on future discussions, this permission could be removed and IT could handle actions requiring it, but that would add more internal support burden - again, for future discussion.

Step 1

The only step currently needed is for an AAD admin to go in and give that "User Access Administrator" permission to the user in question on a subscription-wide basis.  Once that is done, the Team Lead should have no problem creating the service connection.

Overview

This is a walkthrough of how to tell an App Service instance to watch a particular repo in the Azure Container Registry to automatically refresh itself anytime that a particular Dockerfile there changes.

Prerequisites

An Azure Container Registry already exists

A version of the Dockerfile has already been deployed there

A blank instance of an App Services for Containers has been created

Step 1

We first need to give permissions for accessing the Azure Container Registry repo to the service account for the App Service.  To do this, you will need to have a level of admin access.

Open up the control panel for the Container Registry, and select "Access control (IAM)"

![Image2]('images/setup-azure-pipeline/2.png')

In the section called "Grant access to this resource", click "Add role assignment".  If you don't see this, you don't have permissions.

![Image3]('images/setup-azure-pipeline/3.png')

From the list of roles to be added, select "AcrPull".

![Image4]('images/setup-azure-pipeline/4.png')

Under "members", select the dropdown for "Managed Identity".

![Image5]('images/setup-azure-pipeline/5.png')

Click "+ Select members".  In the dialog, select "App Service", which should show you options for all App Service identities in that resource group.  Select the one for the App Service you created.

![Image6]('images/setup-azure-pipeline/6.png')

Click "Ok" and finish the wizard.  The App Service should now have permissions to access the Container registry to pull images.

Step 2

Go to the Azure App Service instance in the Azure control panel.  Go to "Deployment Center" under the "Deployment" section.

![Image7]('images/setup-azure-pipeline/7.png')

Step 3

Change "Registry Source" to be "Azure Container Registry".  Then, select the appropriate registry, image and tag as provided to you by the dev team.

![Image8]('images/setup-azure-pipeline/8.png')

Also, make sure to turn "Continuous Integration" to "On".  Without this, the webhook won't fire and the container won't refresh.

![Image9]('images/setup-azure-pipeline/9.png')

Finishing Up

At this point, everything should be ready.  You can now ask the developers to kick off a pipeline run and make sure that the webhook picks up the change by looking in the "Logs" section of the App Service's control panel, and watching for a Docker notification that a new image has been detected and it is loading and running it.