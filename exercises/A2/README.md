# Lesson A – Seting up Continuous Delivery for the Timesheet Application

# Exercise A2 - Setting Up Your Pipeline

## Overview
After we started our Continous Delivery infrastructure, we are now ready to setup a Continuous Delivery Pipline for automating the process of building and delivering our Timesheet project.

We will learn how easy it is to create and configure a Continuous Delivery Pipeline for our project. Furthermore, we will earn a feeling for what the pipeline does and how it helps us to realize quick lead times and high quality.


## Exercise Steps
* For deploying the Timesheet Application, we will add our SCP target space to the pipeline configuration which is part of our application sources
* For running the Continuous Delivery pipeline of our application, we will create a build job on our Continuous Delivery Server
* We will observe the execution of our freshly created Pipeline and analyze the error messages after it failed
* We will fix the dicovered issue with the help of the SAP Cloud SDK
* Finally, we will run the pipeline again, resulting in a deployment to SAP Cloud Platform.

## Customize Your Pipeline Configuration

Thanks to the high degree of standardization in SAP Cloud Application Programming Model projects, we can adopt the SAP Cloud SDK pipeline without writing a single line of code. For modifying pipeline behavior, we can leverage the declarative `pipeline_config.yml` file which is located in the root of our project. Here we can perform well-defined customizations. In this session, we will use it to define the shared HANA database which will be used during automated tests and to define the SAP Cloud Platform deploymemt targets.

> Note: All Piper-based pipelines support the concept of aspect-oriented breakouts. In case your application requires more customizations than foreseen by our declarative configuration system, you can selective plug-in custom code to extend the pipeline behavior. 

In this session, the instructors created a SAP Cloud Platform user account and corresponding target space for each participant. So, let's switch back to IntelliJ and add the deployment target of our app to `pipeline_config.yml`.

Locate `pipeline_config.yml` in your project view and open it with a double click. As you can see, the configuration file already contains placeholder configuration entries for the HANA database and for the deployment. In order to make it work, we need to fill the placeholder `participantId` with the id that was assigned to us.

For this, click on `Edit > Find > Replace` like shown below.

![](../../images/a/replace-pipeline-config.png)

Now enter `participantId` as term to be replaced and your personal participant id as replacement. Then click on `Replace all`. Then save the file.

![](../../images/a/customize-pipeline-config.png)

> Feel free to have a closer look at the pipeline configuration. If you want to learn more about available configuration parameters, feel free to have a look into our reference: https://github.com/SAP/cloud-s4-sdk-pipeline/blob/master/configuration.md

Finally, we just need to commit and push our new configuration to the central source code repository. On the lower left, click on `Version Control` to open the version control pane.

![](../../images/a/version-control.png)

 Now click on `Local Changes` and then on the green "Commit" checkmark.

![](../../images/a/commit-pipeline-config.png)

In the appearing dialog, perform the following steps:
* Double check that your participant id is correctly filled into the placeholders in `pipeline_config.yml`
* Enter a commit message (e.g., "adapt pipeline config")
* Click on the down-facing arrow in the `Commit` button
* Select `Commit and Push`

![](../../images/a/push-pipeline-config.png)

After pushing your changes succesfully, you will see the following pop-up on the bottom right.

![](../../images/a/push-success.png)

The project is now fully configured for Continuous Delivery. Wasn't that easy!?
Next, let's configure our Continuous Delivery server.


## Configure Your Continuous Delivery Server

After your project is configured, let's set up the Jenkins build job for running the pipeline. We will first create the necessary deploymnent credentials and then a build job for our project.

Re-open your browser, navigate to the Jenkins user interface (http://localhost:8080).

### Create Deployment Credentials

The Continuous Delivery pipeline of your project will finally deploy to the SAP Cloud Platform space that we created for the purpose of this session. Before we can run it, we need to save the deployment credentials in Jenkins. This procedure is a bit cumbersome - so strictly follow the steps described.

* On the Jenkins landing page, look out for the menu on the left and click on `Credentials`.<br>
![](../../images/a/credentials1.png)

* Click on the `System` sub-item that appeared below `Credentials`.<br>
![](../../images/a/credentials2.png)

* Look out for the `System` section and click on `Global credentials (unrestricted)`.<br>
![](../../images/a/credentials3.png)

* In the menu section, you should now see the item `Add Credentials` - click on it.
<br>![](../../images/a/credentials4.png)

* Now you should see the form to enter a new credentials entry. Based on `pipeline_config.yml`, which we edited earlier, the pipeline will retrieve the deployment credentials from the entry with ID `CF-DEPLOY`. To create it, enter the following data. Make sure that you use the username and password that was handed out to you.<br>![](../../images/a/credentials5.png)

* Finally, click on `OK` and navigate back to the Jenkins landing page (http://localhost:8080).

Well done! As a result, you should now see your freshly created credentials entry.

![](../../images/a/credentials6.png)

Next, we will create the build job for our project.

### Create Build Job

We will now create a build job for our project which will run the pipeline for our branch.

* On the Jenkins landing page, click on `create new jobs`. 
<br>![](../../images/a/create-new-job.png)

* Enter `timesheet` as item name. 
* SAP Cloud SDK Continuous Delivery pipelines are designed for multi-branch git repositories. Therefore, select `Multibranch Pipeline` as job type.
<br>![](../../images/a/multibranch.png)
* Finally, click on `OK`.

Next, we will connect the source code repository to the new job.

* In the section `Branch Sources`, click on the button `Add source` and then on `Git`.
<br>![](../../images/a/branch-source.png)

* In the new pane, enter the git url `http://cloudl000024.wdf.sap.corp:8080/teched/caa381` as project repository.

By default, the multibranch pipelines will execute the pipeline for all branches of our repository. This is usually the desired behavior. However, since we are using a joint git repository in this hands-on session, we need to make sure that our build server does not start executing the pipelines of our co-participants. We can do this by limiting the build job to our branch only:

* Find the `Behaviors` section
* Click on the button `Add`
* In the menu, click on `Filter by name (with regular expression)`
<br>![](../../images/a/branch-behavior.png)

* Then navigate to the new `Filter by name (with regular expression)` section and enter the name of your branch (participant id) in the text field as shown below.
<br>![](../../images/a/branch-name.png)

* Finally, click on `Save`.

* Now, Jenkins will automatically scan the repository, discover your branch, and then execute the pipeline for it.
Make sure that Jenkins properly detects your branch (and only your branch). The corresponding output should look like the log below.
<br>![](../../images/a/branch-scanning.png)

## Monitor Pipeline Execution

After Jenkins discovered your branch, it automatically started executing the SAP Cloud SDK pipeline.

Let's inspect the progress of our pipeline execution:
* Go back to the Jenkins landing page on http://localhost:8080.
* You should see the `timesheet` job that we just created.
* The `Build Executor Status` section should show several executors that started running pipeline steps and stages.
* To inspect the execution of our pipeline, let's click on `Open Blue Ocean` in the Jenkins menu. This will bring us to the modernized (but minimal) Jenkins Blue Ocean user interface.<br>
![](../../images/a/job-created.png)
* Click on the `timesheet` job<br>
![](../../images/a/timesheet-job.png)
* Now you see all currently running pipelines of your timesheet job. To inspect the status of your first pipeline run, click on build run `1`<br>
![](../../images/a/timesheet-branch.png)

Welcome! This is the SAP Cloud SDK pipeline in action. On top you see the graph visualization of the pipeline gaining shape as the execution progresses. Each bubble in the pipeline graph represents a pipeline stage and all stages that are shown on a vertical line are executed in parallel. If you want to understand what's happening in a specific stage, just click on the bubble and inspect the logs shown below the pipeline graph. 

> Note: In our experience, the Jenkins Blue Ocean pipeline view has the tendency to get stuck, often after the end of a stage. Refreshing the browser (press `F5`) helps in such cases to show the latest state of pipeline execution.

![](../../images/a/pipeline-initial.png)

> Note: Your first build run will usually take quite some time because the pipeline needs to fetch many project dependencies from the internet. Fortunately, thanks to the smart and transparent download cache, follow-up builds will run significantly faster because dependencies will then be resolved locally.

While the pipeline executes, let's get a better understanding of what's going on. The automated pipeline is our primary tool facilitate a quick flow of work from commit to production - because only productively deployed code is good code. Sounds risky? That's why it also acts as a quick feedback giver - because we only want well-working code to be deployed to production.

## Structure of the SAP Cloud SDK Continuous Delivery Pipeline
So, what does the SAP Cloud SDK pipeline particularly do?

* **Bootstrapping:** The SAP Cloud SDK pipeline is fully codified (Pipeline-as-Code). That means that we already did all the hard work for you and you can start using it without writing a single line of code. If you look cloesely, you will find a file called `Jenkinsfile` in the root of your project. This file loads the SAP Cloud SDK pipeline definition from the open source repository on https://github.com/SAP/cloud-s4-sdk-pipeline and starts executing it.

> Note: By setting the property `pipelineVersion` to a specific release of the pipeline, you can fix the pipeline to a specific version. This is recommended for productive projects. Conducting a pipeline update to the most recent release is then just a matter of changing the value of `pipelineVersion`, ideally verified via a pull request.

* **Init:** Once the pipeline defintion is loaded, it runs its `Init` stage. Here, the pipeline loads your project-specific configuration from `pipeline_config.yml` and checks out the source code of your project.

* **Build:** This stage builds the deployable artifact of the application. Since the timesheet application is a SAP Cloud Programming Model based application, this will in our case be an *.mtar* file.

> Note: The SAP Cloud SDK pipeline implements the *build-once principle*, i.e., the artifact is only built once during the whole delivery process. The same deployable artifact is used in all follow-up stages without rebuilding (parts of) it. This saves precious time and increases the reliability of the pipeline.  

* **Local Tests:** The local test group executes a family of checks that can be run locally without deploying the application to SAP Cloud Platform. The individual stages are executed in parallel.
    * **Backend Unit- and Integration Tests:** These two stages run backend tests and collect code coverage information.
    * **Frontend Unit- and Integration Tests:** If your project has a frontend, these two stages execute the corresponding unit and integration tests. As you see, no one yet wrote frontend tests for the timesheet application - we should definitely address this in the near future to make sure that we get quickly receive feedback on the functional correctness of frontend components.
    * **Lint:** If the pipeline detects a SAPUI5 frontend in your application, it will automatically execute the SAPUI5 best practice linter. You can use the results to improve your code. If you want, you can also let the pipeline fail based on custom thresholds to enforce quality.
    * **NPM Dependency Audit:** If your project contains JavaScript modules, the pipeline will automatically execute `npm audit` to check whether your project uses vulnerable dependencies. If this is the case, it will let the pipeline fail. You can audit findings and whitelist dependencies via `pipeline_config.yml` if they turn out to be uncritical for you. In fact, we whitelisted some findings in the current state of the Timesheet Application.
    * **Static Code Checks:** The pipeline automatically executes a set of best-practice static code checks. This comprises general coding practices and checks that are specific to the proper use of the SAP Cloud SDK.
* **Remote Tests**: The remote test groups executes checks that require the deployment of the application. The individual stages are executed in parallel. The timesheet app does not have any remote tests yet, therefore this group is skipped by the pipeline.
    * **End-to-end Tests:** Using a simulated browser environment, end-to-end tests ensure that user stories of the application behave as expected when the application is deployed to SAP Cloud Platform.
    * **Performance Tests:** The SAP Cloud SDK SDK supports performance tests with Gatling and JMeter. If your project contains corresponding tests, they will be automatically executed.
* **Quality Checks:** This stage collects telemetry data of unit and integration tests and assures that your application does not violate relevant cloud qualities. It assures that you integrate other services in a resilient manner and that only whitelisted services are consumed from SAP S/4HANA ERP systems. In order to ensure that enough telemetry data was collected, it also enforces a minimum code coverage threshold.
* **Third-party Checks:** If your company holds a license of *Checkmarx*, *Fortify*, *SourceClear*, *WhiteSource*, you can easily integrate those commercial code scanners into the SAP Cloud SDK pipeline. They will be executed in parallel as part of the Third-party Checks stage. Since such scans tend to run longer, this group is only executed for the productive branch (usually `master`).
* **Artifact Deployment:** If the pipeline runs on the productive branch and all checks succeeded, the artifact can at this point in time be deployed to an artifact repository. This helps you to keep an auditable trail of deployed versions. We don't have a repository configured, therefore, this stage will be skipped.
* **Production Deployment:** If everything went well and the pipeline runs on the productive branch, the application will finally be deployed to the SAP Cloud Platform spaces defined in `pipeline_config.yml`.

## Inspecting The Build Result

After our quick excursion on the pipeline structure, let's check the result of pipeline run:
![](../../images/a/pipeline-failure.png)

Oh no! Something went wrong. Obviously the quality checks stage discovered a problem. Let's have a closer look into the logs by scrolling down until we see the error messages. 

![](../../images/a/pipeline-failure-msg.png)

The output tells us that our Timesheet application accessed the SAP S/4HANA `EmployeeTime` service in a non-resilient manner. This means that issues during the invocation, e.g., a high network latency or unexpected issues on SAP S/4HANA-side, could cascade to the timesheet application and, therefore, negatively affect the user experience of multiple end users or even tenants. By properly designing distributed applications, this fallacy can be easily avoided.

Let's have a look into the code to fix the issue. Open IntelliJ and locate the implementation of the Team Calendar Service (`srv/src/main/java/my/timeheethandson/TeamCalendarService`).

![](../../images/a/teamcalendar-file.png)

Feel free to have a look at the code and understand what's going on. Do you get a first feeling of what might be wrong?

Let's look closer at the code that reads existing entries from SAP S/4HANA and SAP SuccessFactors (starting in line 52).

```java
// Read SAP S/4HANA appointments
List<EntityData> s4Appointments;
try {
    s4Appointments = ResilienceDecorator.executeCallable(
        () -> readS4Appointments(persons, year),
        ResilienceConfiguration.of(WorkforceTimesheetService.class)
    );
} catch (Exception ex) {
    [...]
}

// Read SFSF appointments
List<EntityData> sfsfAppointments;
try {
    sfsfAppointments = readSfsfAppointments(persons, year);
} catch (Exception ex) {
    [...]
}
```

As you can see, the code that accesses SAP S/4HANA is wrapped by the `ResilienceDecorator` of the SAP Cloud SDK. However, this does not apply to the code that accesses SAP SuccessFactors - that's a violation of cloud qualities in the Timesheet application.

Let's fix the design flaw, by applying the same pattern as for the SAP S/4HANA integration code:

```java
// Read SFSF appointments
List<EntityData> sfsfAppointments;
try {
    sfsfAppointments = ResilienceDecorator.executeCallable(
        () -> readSfsfAppointments(persons, year),
        ResilienceConfiguration.of(EmployeeTimeService.class)
    );
} catch (Exception ex) {
    [...]
}
```
After adapting the code in IntelliJ, save the file, commit, and finally push it with the known procedure.
* Navigate to `Version Control > Local Changes` and then click on the green checkmark button to commit your changes.<br>
![](../../images/a/commit-resilience.png)
* In the new `Commit Changes` screen, review your changes, click on the the dropdown arrow of the `Commit` button, and finally click `Commit and Push`.<br>
![](../../images/a/push-resilience.png)

## Trigger a New Pipeline Run

Now its time to check whether our changes successfully fixed the issue:
* Re-open the Chrome browser
* Navigate to Blue Ocean
* Open the timesheet job and navigate to the branches (shortcut: http://localhost:8080/blue/organizations/jenkins/timesheet/branches/).
* Click on the `Run` button to trigger a new build of your branch.<br>
![](../../images/a/rerun-pipeline.png)

> Note: In productive setups, we would usually setup a webhook from our source code management system to Jenkins to trigger builds automatically whenever changes are pushed to git. For the sake of simplicity, we skipped this automation in our hands-on session.

* Click on the freshly started pipeline run to get to the pipeline progress screen we saw earlier.<br>
![](../../images/a/open-build.png)

This time, all checks should succceed and pipeline should finally perform a production deployment into your personal Cloud Foundry space.

![](../../images/a/deployment-successful.png)

## Open the Freshly Deployed Application

To view your space on SAP Cloud Platform, you can use the following deep link:
https://account.hana.ondemand.com/cockpit/#/globalaccount/b579d51f-44f7-4a0a-915d-83abd236f86d/subaccount/e44933a6-9b18-4072-8d54-bde63886af30/spaces

Alternatively, follow the following steps:
* Open https://account.hana.ondemand.com
* Click on the `Teched2019` global account tile
* Click on the `CAA381cf` subaccount tile
* In the menu on the left, click on the `Spaces` item

When you arrived at the spaces overview, click on the `CAA381-participantId` space tile.

You should now see the list of running applications which should look similar to the following screenshot. Click on the started application instance to get to the details.
![](../../images/a/applications.png)

Now, click on the link in the routes tile. This will open your freshly deployed application.
![](../../images/a/routes.png)

Congratulations, the timesheet app is now resilient and succesfully shows data from SAP SuccessFactors and SAP S/4HANA.

![](../../images/a/timesheet-app.png)


## Summary

At the end of this lesson, let's quickly recap what we learned so far:
* We learned how easy it is to setup a Continuous Delivery infrastructure with the help of Piper's `cx-server` script
* We understood the concept and value of ready-made pipelines
* We created our own declarative pipeline configuration for our Timesheet application and created a build job that executes the pipeline for our Timesheet project
* We learned which qualitites the SAP Cloud SDK pipeline assures for us and discovered that our application is not implemented in a resilient manner.
* After fixing the issue, we ran the pipeline again and successfully deployed our Timesheet application to production.

So far so good - SAP tools help to build and deliver high-quality applications efficiently. But what happens afterwards? How can we efficiently automate the operation of our app? That's what you will learn in Lesson B of this hands-on session. Have fun!

[![](../../images/nav-previous.png) Previous Exercise](../A1/README.md) ｜ [![](../../images/nav-home.png) Overview page](../../README.md) ｜ [Next Exercise ![](../../images/nav-next.png)](../../overviews/B/README.md)
