# Lesson A - Setting up Continuous Delivery for the Timesheet Application

# Brief Overview
Imagine that you freshly joined a new development team. The team is new to cloud development and started recently to work on a new project, the Timesheet Application.

![Screenshot of Timesheet Application](../../images/a/timesheet-app.png)

The Timesheet application helps companies to implement an approval workflow for the tracking of employee working hours. To benefit from the unique opportunities of building applications in the cloud, the team decided to build the Timesheet application on SAP Cloud Platform. Thanks to the SAP Cloud SDK, the team was quickly able to make the necessary integrations to SAP SuccessFactors and SAP S/4HANA. The web services and the persistence for timesheet entry drafts are implemented based on the SAP Cloud Application programming model.

Thanks to your productive colleagues, the application is already in a good initial state. Now your Product Owner wants to start to roll out the application to first customers to gather their feedback. It is expected that those customers will have a lot of feedback, and your team wants to be able to react quickly. Furthermore, as with every new application, customers might run into glitches that you didn't discover during development. Therefore, your team wants to be able to confidently deliver new versions of the Timesheet Application on a sub-daily basis.  In short, your team wants to start practising *Continuous Delivery*. This requires a high level of automation of your whole build, test, quality assurance, and delivery activities, typically achieved by the implementation of a Continuous Delivery pipeline. 

Implementing and maintaining Continuous Delivery environments and pipelines is a challenging task that requires particular expertise and an increasing amount of effort as your application and pipeline matures. In many development teams, this becomes the full-time job of a team member. Imagine the additional customer value you could create if this teammate would be relieved from his burden and could start working on value-adding features that delight customers.

Luckily, if you are building your application with the SAP Cloud Application Programming model and / or the SAP Cloud SDK, we can help you! SAP's open-source Project Piper provides efficient ready-made tools to kickstart your Continuous Delivery endeavours. For our use case, it offers a containerized Continuous Delivery infrastructure twhich hat can be used to easily instantiate Continuous Delivery servers on any host with Docker installed or on Kubernetes clusters. Once we have the necessary infrastructure, we can then execute the ready-made SAP Cloud SDK Continous Delivery pipeline. The pipeline does the actual work of building a change, executing relevant tests and quality checks, and finally deploying it to production if everything went well.

## Estimated Time: 60 minutes

## What you will learn
 - How to setup a Continous Delivery infrastructure within just minutes with the help of Project Piper Cx Server.
 - How to leverage the SAP Cloud SDK ready-made pipeline for automating the delivery process without writing a single line of code.
 - Good practices for Continuous Delivery.

* Exercise A1 - [Starting Your Local Continuous Delivery Server](../../exercises/A1/README.md)
* Exercise A2 - [Setting Up Your Pipeline](../../exercises/A2/README.md)



[![](../../images/nav-previous.png) Preparation](../../prep/README.md) ｜[![](../../images/nav-home.png) Overview page](../../README.md) ｜ [Start Exercise ![](../../images/nav-next.png)](../../exercises/A1/README.md)
