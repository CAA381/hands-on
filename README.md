# Description
This guide has been created for the SAP TechEd 2019 session CA028. Taking your DevOps skills with SAP Cloud Platform to the next level.
In this session participants will learn best practices how to operate their Cloud Application deployed on SAP Cloud Platform.

# Used Landscape 
> **Note - DELETE THIS IN THE FINAL VERSION** The picture below is not final and **will** be changed

> **Note - DELETE THIS IN THE FINAL VERSION** Also note that the setup is **per participant** I do not want anything shared between participants since it can get messy. Maybe the only shared thing will be the GitHub repo. Of course they will share an CF org but eveyrone will have a separate space.

The different systems and their relation we use for our scenario are sketched out by the following landscape diagram.
![System Setup](images/system_setup_.png)

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
    * Cloud Controller - The Cloud Controller maintains a database with tables for orgs, spaces, services, user roles, and more. Via it we can understand what is the current state of our application (is it running, is it stopped, is it crashed, etc.)
    * Alert Notification - this service is used to defined events(alerts) that can occur with our application (or its dependencies). Once these events occur the Alert Notification will notify us via whatever channel. For the exercise case we are going to use it to define that we want to receive an alert when some of our application's components is unavailable.
    * Automation Pilot - this service is used to automate the reactions to a given alert. For example if you need to restart your applicaiton uppon an availability alert you can define this via Automation Pilot and not bother with manual work.
* Slack - open channel for receiving an alert. You will also have the opportunity to use your email.

Everything has been already configured for you so that you can focus on the DevOps topic. Nethertheless, here is a summary of the requirements that re needed if you want to set up the same landscape later on your own:

* **This GitHub Repo will be preserve for your convinience after the TechEd so you can consume the resource anytime**

> **TODO - DELETE THIS IN THE FINAL VERSION** Provide the list of requirements on a later point before I finalize the handouts.

# Preparation (Mandatory)
To finalize the setup we have to execute the following steps befor starting with the exercise:

> **Note - DELETE THIS IN THE FINAL VERSION** I currently don't have any prep steps but I leave this as a placeholder as they most probably will appear

Follow the instructions on the [preparation page](prep/README.md) to get all the details. 

# Exercises

## Short overview
Here's a sketch of what we are going to do in the next almost 2 hours:
1. We are going to import an existing application in our WebIDE 
2. Introduce a small change into it and test it locally in the browser
3. Convert our application to a Multi-Target Application and deploy it to the cloud
4. Setup a pipeline which supports blue-green deployment into productive environment
5. Deploy and test the application into the productive environment
6. Subscribe for Alert Notification
7. Define a subscription for and alert which notifies us eveyrtime some of the app's components is in state different than STARTED.
    > Note: we will refer to these as lifecycle management alerts

8. Intentiopnally break the application in order to receive an alert about its breakage
9. Explore sources of the applicaiton and see that there's a place where an exception is thrown in that very place also our application sends an alert to Alert Notification that something very specific for it has happened
    > Note: we will refer to these as custom alerts

10. Define a subscription for an alert which notifies us for this special situation
11. Intentionally trigger the special situation and get notified for it.
12. Automte the control over that application by using automated actions that react to a given alert

The actual exercises are grouped into three lessons

## Lesson A – Modeling and Test of your application
In this lesson we will get to know our appliaciton. We will understand how it can be configured. Also we will learn how to make a simple change and test it into our test environment. This lessons has the following exercises:

* Overview and Start - [Import the application from GitHub to SAP Web IDE](preparations/A/README.md)

## Lesson B – Setting up CI/CD pipeline
* Exercise B1 - [Setting up your Jenkins server](exercises/B1/README.md)
* Exercise B1 - [Creating your first pipeline](exercises/B2/README.md)
* Exercise B2 - [Configuring blue-green deployment of your application and deploying the application](exercises/B2/README.md)

## Lesson C - Observability and Control of your application
* Exercise C1 - [Setting up Alert Notification](exercises/C1/README.md)
* Exercise C2 - [Createing a subscription for lifecycle management alert and receiving the alert](exercises/C2/README.md)
* Exercise C3 - [Createing a subscription for custom alert and receiving the alert](exercises/C3/README.md)
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