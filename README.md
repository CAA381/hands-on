# Description
This guide has been created for the SAP TechEd 2019 session CA028. Taking your DevOps skills with SAP Cloud Platform to the next level.
In this session participants will learn best practices how to operate their Cloud Application deployed on SAP Cloud Platform.

# Used Landscape 
> **Note - DELETE THIS IN THE FINAL VERSION** The picture below is not final and **will** be changed

> **Note - DELETE THIS IN THE FINAL VERSION** Also note that the setup is **per participant** I do not want anything shared between participants since it can get messy. Maybe the only shared thing will be the GitHub repo. Of course they will share an CF org but eveyrone will have a separate space.

The different systems and their relation we use for our scenario are sketched out by the following landscape diagram.
![System Setup](images/system_setup.png)

The used landscape consists of the following systems:
> **TODO - DELETE THIS IN THE FINAL VERSION** The application to be used is yet to be clarified however most probably we will use some from the spring sample apps like spring-music or CAP's bookshop java applicaition.

* Our sample application, deployed into two separate CF spaces (Test/Prod). The application consists of two microservices and a database.
* SAP WebIDE or Visual Studio Code - depending on the choice of the participant those are the development environments that will be used.
* GitHub - repository where we will keep our application's soruces, the version into that repo will be deployed on the landscape
> **TODO - DELETE THIS IN THE FINAL VERSION** What we will do with the code is to introduce a change, test it on the test environment and then deploy it productively. In order not to get into merge conflicts and making everyone submitting into github I will most probably create two separate repos - one for the code before the change used for the test environemtn. One repo that contians the code after the change used for productive deployment. However this is just an idea I will think for other options as well.

* Cx Server - Downloaded docker container which consists of
    * Jenkins with Blue Ocean - with the help of jenkins we will be able to build a pipeline. For the sake of the time we will keep our pipeline simple.
    * MTA Deploy Service - de-facto the tool that is used for deployment of MultiTarget applications. We will integrate this one with our pipeline in order to execute our productive deployment

> **Note - DELETE THIS IN THE FINAL VERSION** Some of the services below are not yet listed on the diagram. I want first to clear some technical questions before putting them there.

* On the SAP Cloud Platform side we have:
    * Availability service - this service monitors closely our application and it can understand if some of its components are unavailable. 
    * Alert Notification - this service is used to defined events(alerts) that can occur with our application (or its dependencies). Once these events occur the Alert Notification will notify us via whatever channel. For the exercise case we are going to use it to define that we want to receive an alert when some of our application's components is unavailable.
    * Automation Pilot - this service is used to automate the reactions to a given alert. For example if you need to restart your applicaiton uppon an availability alert you can define this via Automation Pilot and not bother with manual work.
* Slack - open channel for receiving an alert. You will also have the opportunity to use your email.

Everything has been already configured for you so that you can focus on the DevOps topic. Nethertheless, here is a summary of the requirements that re needed if you want to set up the same landscape later on your own:

* **This GitHub Repo will be preserve for your convinience after the TechEd so you can consume the resource anytime**

> **TODO - DELETE THIS IN THE FINAL VERSION** Provide the list of requirements on a later point before I finalize the handouts.

# Preparation (Mandatory)
To finalize the setup we have to execute the following steps befor starting with the exercise:

1. Download and configure the Cx Server Docker Container
2. Import the projects into your IDE of choice (**TODO** Think whether not to do that in the Lesson A)

Follow the instructions on the [preparation page](prep/README.md) to get all the details. 

# Exercises

## Short overview
Here's a sketch of what we are going to do in the next almost 2 hours
We have already our application deployed on Cloud Platform, so we are going to:
1. Introduce a small change into it
2. Test this change into the test environment
3. Setup a pipeline which supports blue-green deployment into productive environment
4. Deploy and test the application into the productive environment
5. Define an availability monitor and alert for the application
6. Intentiopnally break the application in order to receive an alert about its breakage
7. Automte the control over that application by using automated actions that react to a given alert

The actual exercises are grouped into three lessons

## Lesson A – Modeling and Test of your application
In this lesson we will get to know our appliaciton. We will understand how it can be configured. Also we will learn how to make a simple change and test it into our test environment. This lessons has the following exercises:

* Exercise A1 - [Getting started with your application. Explore its sources via an IDE of Choice](exercises/A1/README.md)
* Exercise A2 - [Make small change and test it into your test environment](exercises/A1/README.md)

## Lesson B – Setting up CI/CD pipeline
* Exercise B1 - [Setting up jenkins to work with GitHub](exercises/B1/README.md)
* Exercise B2 - [Creating your first pipeline](exercises/B2/README.md)
* Exercise B3 - [Configuring blue-green deployment of your application and deploying the application](exercises/B3/README.md)

## Lesson C - Observability and Control of your application
* Exercise C1 - [Setting up availability monitor](exercises/C1/README.md)
* Exercise C2 - [Createing a subscription for alert](exercises/C2/README.md)
* Exercise C3 - [Breaking the applicaiton receive an alert](exercises/C3/README.md)
* Exercise C4 - [Automating your reactions to an alert](exercises/C4/README.md)

# Final hints before you start

* As the 3 lessons don’t depend on each other, you can choose which lessons you want to learn. In 2 hours, you should be able to run 2 of them, 3 if you are really fast. So you can start with one or the other lesson. **Only the preparation steps need to be done at the beginning.**

> **TODO - DELETE THIS IN THE FINAL VERSION** The users and passwords are currently in clatification note I will fill this section later on.

* Multiple systems with different users: As you are working on different systems that use all different user / password combinations you need to be very careful where to use which user. Too many failed login attempts will lock the systems. 
* Use the provided Student Overview Paper to verify credentials during the hands-on session.
* Your Teched image will be automatically deleted 5 minutes after the end of the session.

# Handy links
> **TODO - FILL THIS ON LATER STAGE**

# Contact
This content is currently maintained by 
* [Kiril Gavrailov](mailto:k.gavrailov@sap.com)
* [Georgi Kirtchev](mailto:georgi.kirtchev@sap.com)
* [Vesselin Mitrov](mailto:vesselin.mitrov@sap.com)

# License
Copyright (c) 2018 SAP SE or an SAP affiliate company. All rights reserved.
This project is licensed under the Apache Software License, v. 2 except as noted otherwise in the [LICENSE file](LICENSE.txt).