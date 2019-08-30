# Lesson A - Setting up Continuous Delivery for the Timesheet Application

# Brief Overview
Imagine that you freshly joined a new development team. The team is new to cloud development and started recently to work on a new project, the Timesheet Application.

![Screenshot of Timesheet Application](../../images/a/timesheet-app.png)

The Timesheet application helps companies to implment an approval workflow for the tracking of employee working hours. To benefit from the unique opportunities of building applications in the cloud, the team decided to build the Timesheet application on SAP Cloud Platform. Thanks to the SAP Cloud SDK, the team was quickly able to build the necessary integrations to SAP SuccessFactors for retrieving employee data and SAP S/4HANA for storing timesheet entries. The webservices and the persistence for timesheet entry drafts are implemented based on the SAP Cloud Application programming model.

Thanks to your productive colleagues, the application is already in a good initial state. Now your Product Owner wants to start to roll out the application to first customers to gather their feedback. It is expected, that those customers will have a lot of feedback and your team wants to be able to quickly react to it. Furthermore, as with every new application, customers might run into glitches that you didn't discover during development. Therefore, your team wants to be able to confidently deliver new versions of the Timesheet Application on a sub-daily basis - in short your team wants to start practicing *Continuous Delivery*. This requires a high level of automation of your whole build, test, quality assurance, and delivery activities, typically achieved by the implementation of a Continuous Delivery pipeline. 

Implementing and maintaining Continuous Delivery environments and pipelines is a challenging task that requires special expertise and an increasing amount of effort as your application and pipeline matures. In many development teams, this becomes the full-time job of a team member. Imagine how much additional customer value you could create if this person would be relieved from his burden and could start working on value-adding features that delight customers.

Luckily, if you are building your application with the SAP Cloud Application Programming model and / or the SAP Cloud SDK, we can help you! SAP's open source Project Piper provides efficient ready-made tools to kickstart your Continuous Delviery endevours. For our use case it offers a containerized Continuous Delivery infrastructure which can be used to easily instantiate Continuous Delivery servers on any host with Docker installed or on Kubernetes clusters. In this environemt, we can then execute the ready-made SAP Cloud SDK Continous Delivery pipeline which does the actual work of building a change, executing relevant tests and quality checks, and finally deploying it to production if everything went well.

## Estimated Time: 60 minutes

## What you will learn
 - How to setup Continous Delivery within minutes with the help of Project Piper Cx Server.
 - How to execute blue-green deployments of you application out-of-the-box.
 - Best practices for continous delivery.

## Exercise Description 
 - We are going to setup a Jenkins server from scratch. Don't get scared, with the help of Cx Server this is more than easy.
 - After that we are going to setup our user credentials and make the initial configuration
 - Lastly, we are going to build a Pipeline which will execute blue-grenn deployment of our application.


* Exercise A1 - [Starting Your Local Continuous Delivery Server](../../exercises/A1/README.md)
* Exercise A2 - [Creating your first pipeline](../../exercises/A2/README.md)


[[![](../../images/nav-home.png) Overview page](../../README.md) ｜ [![](../../images/nav-next.png) Start Exercise](../../exercises/A1/README.md)]
