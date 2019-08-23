# Description
Welcome to our hands-on session *CAA381 Taking Your DevOps Skills on SAP CloudPlatform to the Next Level* which belongs to the learning journey *Apply DevOps in an SAP solution landscape*. In the next two hours, you will learn and practice how SAP tools help you to build, deliver, and operate high-quality cloud applications that will delight your customers ...and your development team.

# Used Landscape 

During this session, we will interact with various tools and systems. The following sketch shows an overview of the flow of our session.
![System Setup](images/system_setup_.png)

The used landscape consists of the following systems:

* **[Timesheet Application](http://cloudl000024.wdf.sap.corp:8080/teched/caa381.git)**\
Each participant will deploy an own instance of this app to SAP Cloud Platform. The application implements a typical SAP Cloud Platform scenario: It realizes a business process for creating and approving timesheet entries. The project is based on the SAP Cloud Application Programming Model. Furthermore, it uses the convinient APIs of the SAP Cloud SDK to retrieve employee data from SAP SuccessFactors and to read/write approved timesheet entries to S/4HANA. 
* **IntelliJ IDEA**\
We will work with IntelliJ as IDE to edit and push the code of the Timesheet Application.
* **GitLab SCM**\
For central source code management, we will use GitLab. We use a shared source code repository as starting point. In this repository, each participant will create his own branch to isolate source code changes from other participants.
* **Project Piper Cx Server**\
Project Piper provides tools for the efficient implementation of Continuous Delivery in the SAP ecosystem. We will use the Piper Cx Server to create an own local Continuous Delivery server instance out of the box. In this pre-configured environemnt, we will then execute the SAP Cloud SDK pipeline to run the build, tests, quality checks, and deployment of our Timesheet Application.
* **SAP Cloud Platform Cloud Foundry Space**\
Every participant will have a dedicated Cloud Foundry space, accessible with the provided username and password from the handouts on your desks. Furthermore, we will use the following services to observe and operate our application:
   * The Cloud Controller maintaining a database with tables for organizations, spaces, services, user roles, and more. Via it, we can understand what the current state of our application is (is it running, is it stopped, is it crashed, etc.)
   * The Alert Notification Service which is used to define events (alerts) that can occur with our application (or its dependencies). Once these events occur, the Alert Notification will notify us via whatever channel. For the exercise case, we are going to use it to define what we want to receive an alert when some of our application's components are unavailable.
   
* **Slack**\
Finally, we will use Slack for receiving alerts. You will also have the opportunity to use your email address.

Everything has been already configured for you so that you can focus on the DevOps topic. Nevertheless, here is a summary of the requirements that are needed if you want to set up the same landscape later on your own:

* **This GitHub Repo will be preserved for your convenience after the TechEd so you can consume the resource anytime**
* To get started with Piper and the SAP Cloud SDK Continuous Delivery Toolkit, check out [this tutorial](https://blogs.sap.com/2017/09/20/continuous-integration-and-delivery/).
* You will need to have an [SAP Cloud Platform](https://cloudplatform.sap.com/index.html) account (CF or Neo environment)
* An active subscription to [Alert Notification](https://cloudplatform.sap.com/capabilities/product-info.SAP-Cloud-Platform-Alert-Notification.df14655e-ee31-45ab-b755-71f869e359c8.html).
* SAP CAP based application. Learn how to build one [here](https://developers.sap.com/group.cp-apm-full-stack-app.html)

# Preparation (Mandatory)

## Start IntelliJ IDE
Before starting any concrete activities, please make sure that you checked out the latest version of our sources. Please navigate to `D:\Files\Session\CAA381` and click on the IntelliJ shortcut.

![](images/a/start-intellij.png)

## Pull Latest Sources
We have a copy of the Timesheet Application checkout out on our machine. However, our colleagues continued working on it during the last days. Therefore, we need to check out the lastest sources after IntelliJ started. On the top right, we can click on the blue "Update Project" arrow to start the update.

![](images/a/git-pull.png)

After the latest sources have been successfully pulled, we will see a success indicator on the bottom right.

![](images/a/pull-success.png)

## Create Personal Branch

Now, let's create our personal branch for our source code changes. On the bottom right, click on `master` and then select `New branch` from the popup menu.

![](images/a/new-branch.png)

In the next dialog, enter your personal participant id which has been handed out to you and click on `OK`.

![](images/a/branch-name.png)

    > TODO Check if MTA.YAML needs to be customized. If not, remove "participantId" from mta.yaml.

Finally, we can push our personal branch to the central source code repository. In the top menu, click on `VCS > Git > Push`.

![](images/a/push-branch.png)

In the appearing dialog, click `Push`.

![](images/a/push-dialog.png)

Success! You are now ready to continue with lesson A.

![](images/a/push-success.png)

# Exercises

## Short overview

1. Set up a deployment pipeline which deploys the sample app into our Cloud Foundry space
2. Intentionally introduce an error into our deployment process. Explore how easy it is to understand this error. Respectively how easy it is to fix it.
3. Fix the error situation
4. Deploy and test the application into your environment
5. Define a subscription for and alert, which notifies us every time some of the app's components is in a state different than STARTED.
    > Note: we will refer to these as lifecycle management alerts

6. Intentionally break the application to receive an alert about its breakage
7. Explore sources of the app. Notice that there is a place where something unusual happens. In that very place also our app sends an alert to Alert Notification that something concrete for it has happened
    > Note: we will refer to these as custom alerts

8. Define a subscription for an alert which notifies us for this particular situation
9. Intentionally trigger the unusual case and get notified for it.

The actual exercises are grouped into three lessons

## Lesson A – Seting up Continuous Delivery for the Timesheet Application
In lesson A, you will bring your application source code to life by deploying it to SAP Cloud Platform. You might be familar with complex and slow release cycles in traditional software development. In this lesson, you will learn how you can deliver application changes to production within just a few minutes and without risking major regressions for your customers. In particular, we will run through the following streamlined steps:

* Setting up a local pre-configured Continuous Delivery server
* Creating a build job for delivering our project with the SAP Cloud SDK Continuous Delivery pipeline
* Configuring the pipeline behavior for our project
* Analyzing, and fixing a quality issue that the pipeline discovered in our code
* Running the pipeline again, resulting in a successful deployment of our application to SAP Cloud Platform

![](images/nav-next.png) [Overview and Start](overviews/A/README.md)

## Lesson B - Observability and Control of your application
In this lesson, you will learn how to observe and control your application after deployment. During this phase, different problems happen (availability issues, performance issues, unexpected load and many more). You will explore SAP Cloud Platform's offerings towards all these potential issues that might appear.


![](images/nav-next.png) [Overview and Start](overviews/B/README.md)


# Final hints before you start

* As the two lessons don't depend on each other, you can start from wherever you like. In 2 hours, you should be able to run both of them. We recommend executing the lessons consecutively. **Only the preparation steps need to be done at the beginning.**
* **Use the provided Student Overview Paper to verify credentials during the hands-on session.**
* Your Teched image will be automatically deleted 5 minutes after the end of the course.

# Handy links
* [Blog posts with regards to SAP Cloud SDK and Cx Server](https://blogs.sap.com/2017/05/10/first-steps-with-sap-s4hana-cloud-sdk/)
* [Blog posts with regards to SAP Cloud Platform Alert Notification](https://blogs.sap.com/tag/sap-cloud-platform-alert-notification/)
* [SAP Cloud Application Programming Model](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/00823f91779d4d42aa29a498e0535cdf.html)

# Contact
This content is currently maintained by 
* [Benjamin Heilbrunn](mailto:benjamin.heilbrunn@sap.com)
* [Vesselin Mitrov](mailto:vesselin.mitrov@sap.com)
* [Kiril Gavrailov](mailto:k.gavrailov@sap.com)

# License
Copyright (c) 2019 SAP SE or an SAP affiliate company. All rights reserved.
This project is licensed under the Apache Software License, v. 2 except as noted otherwise in the [LICENSE file](LICENSE.txt).
