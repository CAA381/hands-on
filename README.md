# Description
Welcome to our hands-on session -CAA381 Taking Your DevOps Skills on SAP CloudPlatform to the Next Level. We are part of the Learning Journey - Apply DevOps in an SAP solution landscape. And today we are going to get more insights on how to operate with ease your SAP Cloud Platform application. 

# Used Landscape 

The different systems and the relation we use for our scenario are sketched out by the following landscape diagram.
![System Setup](images/system_setup_.png)

The used landscape consists of the following systems:

* Every participant will have a dedicated Cloud Foundry space, accessible with the provided username and password from the handouts on your desks.
* Our sample [Timesheet Application](https://github.wdf.sap.corp/MA/teched2019-caa381), which we will deploy into the dedicated space.
* SAP WebIDE or Visual Studio Code - depending on the choice of the participant those are the development environments that you will use.
* GitHub - repository where we will keep our application's sources, you will deploy this application's version of the landscape
* Cx Server - Downloaded docker container which consists of
    * Jenkins with Blue Ocean - with the help of Jenkins we will be able to build a pipeline. For the sake of the time, we will keep our pipeline simple.
    * MTA Deploy Service - this is the deployer application that our pipeline will use to deploy the application into our Cloud Foundry space.

* On the SAP Cloud Platform side we have:
    * Cloud Controller - The Cloud Controller maintains a database with tables for organizations, spaces, services, user roles, and more. Via it, we can understand what the current state of our application is (is it running, is it stopped, is it crashed, etc.)
    * Alert Notification - this service is used to define events(alerts) that can occur with our application (or its dependencies). Once these events occur, the Alert Notification will notify us via whatever channel. For the exercise case, we are going to use it to define what we want to receive an alert when some of our application's components are unavailable.
   
* Slack - open channel for receiving an alert. You will also have the opportunity to use your email.

Everything has been already configured for you so that you can focus on the DevOps topic. Nevertheless, here is a summary of the requirements that are needed if you want to set up the same landscape later on your own:

* **This GitHub Repo will be preserved for your convenience after the TechEd so you can consume the resource anytime**
* You can download Cx Server from [here](https://github.com/SAP/cloud-s4-sdk-pipeline-docker/tree/master/s4sdk-jenkins-master/cx-server)
* You will need to have an [SAP Cloud Platform](https://cloudplatform.sap.com/index.html) account (CF or Neo environment)
* An active subscription to [Alert Notification](https://cloudplatform.sap.com/capabilities/product-info.SAP-Cloud-Platform-Alert-Notification.df14655e-ee31-45ab-b755-71f869e359c8.html).
* SAP CAP based application. Learn how to build one [here](https://developers.sap.com/group.cp-apm-full-stack-app.html)

# Preparation (Mandatory)
To finalize the setup we have to execute the following steps befor starting with the exercise:

> **Note - DELETE THIS IN THE FINAL VERSION** I currently don't have any prep steps but I leave this as a placeholder as they most probably will appear

Follow the instructions on the [preparation page](prep/README.md) to get all the details. 

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

## Lesson A – Setting up CI/CD pipeline
>***TODO - DELETE THIS IN THE FINAL VERSION** - Benjamin should refine that and also the overview
During this lesson, you will understand how a CI/CD pipelines work and what SAP can offer you to make your day-to-day DevOps processes easier.

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
