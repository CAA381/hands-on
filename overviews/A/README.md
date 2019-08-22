# Lesson A - Seting up Continuous Delivery for the Timesheet Application

Imagine that you freshly joined a new development team. The team is new to cloud development and started recently to work on a new project, the Timesheet Application.

TODO Add picture

The Timesheet application helps companies to implment an approval workflow for the tracking of employee working hours. To benefit from the unique opportunities of building applications in the cloud, the team decided to build the Timesheet application on SAP Cloud Platform. Thanks to the SAP Cloud SDK, the team was quickly able to build the necessary integrations to SAP SuccessFactors for retrieving employee data and SAP S/4HANA for storing timesheet entries. The webservices and the persistence for timesheet entry drafts are implemented based on the SAP Cloud Application programming model.

Thanks to your productive colleagues, the application is already in a good initial state. Now your Product Owner wants to start to roll out the application to first customers to gather their feedback. It is expected, that those customers will have a lot of feedback and your team wants to be able to quickly react to it. Furthermore, as with every new application, customers might run into glitches that you didn't discover during development. Therefore, your team wants to be able to confidently deliver new versions of the Timesheet Application on a sub-daily basis - in short your team wants to start practicing *Continuous Delivery*. This requires a high level of automation of your whole build, test, quality assurance, and delivery activities, typically achieved by the implementation of a Continuous Delivery pipeline. 

Implementing and maintaining Continuous Delivery environments and pipelines is a challenging task that requires special expertise and an increasing amount of effort as your application and pipeline matures. In many development teams, this becomes the full-time job of a team member. Imagine how much additional customer value you could create if this person would be relieved from his burden and could start working on value-adding features that delight customers.

Luckily, if you are building your application with the SAP Cloud Application Programming model and / or the SAP Cloud SDK, we can help you!



* Exercise A1 - [Make small change and test it into your local test environment](../../exercises/A1/README.md)
* Exercise A2 - [Converting your solution to a Multi-Target Application and test it on SAP Cloud Platform](../../exercises/A2/README.md)


[[![](../../images/nav-home.png) Overview page](../../README.md) ｜ [![](../../images/nav-next.png) Start Exercise](../../exercises/A1/README.md)]
