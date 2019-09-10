# Lesson B – Observability and Control of your application
# Exercise B2 -  Configure Custom Alerts

## Objective
You already know how to use the catalogue of alerts of Alert Notification. This catalogue is growing, and in time, you are going to have access to more and more alerts from different SAP Cloud Platform services.
However, there are some alerts that cannot be into the catalogue but are quite important. 

Let's put ourselves in the shoes of a developer. Our cloud application is a complex beast; besides all the dependencies and services that it uses it has also quite a decent amount of code. Into that code, exceptional situations always occur. For example, some of the dependencies we have started returning unknown to us values, and our code does not know what to do. In such kinds of situations, typically a developer would throw an exception. And most probably an operator would like to know that there was such an exceptional situation.

This is where the custom alerts come in play. Alert Notification exposes a REST API and **everyone** can post an alert. This means whenever you have an exceptional situation in your application, you can call this REST API and it will post an alert for you. See the picture below for reference.

![](../../images/b/b1_2_custom.png)

### What you will learn during the exercise
* You will learn about the import/export feature of SAP Cloud Platform Alert Notification.
* Depending on your choice you are going to code or explore how to post a custom alert.
* You will learn how to configure basic authentication user and password with which you can use the Alert Notification.

### Estimated Time
30 minutes

## Exercise Steps

1. Import alert subscription into Alert Notification.
2. Configure basic authentication user and password.
3. Explore the application code and how a custom alert is being posted.
4. Post the custom alert.

## Preparation

**You should have your application deployed from the previous Lesson. If you do not have it in your Cloud Platform space, please notify one of the sessions lectors, and they will provide it for you.**

## 1. Import Alerts

During exercise B1, we explored how we can create Subscriptions, Actions and Conditions via Cloud Cockpit. During this exercise, we are going to use a different approach. We are going to **import** our configuration. Export/Import feature of SAP Cloud Platform Alert Notification allows us to configure once and then import the configuration into different accounts. This certainly saves a lot of clicking.

**If in the previour exercise you have chosen to use your email instead of Slack channel, please call the session facilitator to help you with handling your configuration.**

1. Let's start by opening the Export/Import screen of Alert Notification. To do so in Cloud Cockpit - Alert Notification UI click on **Export and Import**

![](../../images/b/b2_1_export_import.png)

2. Now it is time to import our configuration. We have already defined the action (send us the alert to a Slack channel). What is left to do is to define a Subscription and a Condition that matches our alert. For that purpose copy the json configuration below. **Paste this json into the Import section**
```javascript
{
  "conditions": [
    {
      "name": "AlertIsException",
      "propertyKey": "eventType",
      "predicate": "ANY",
      "propertyValue": "",
      "labels": [],
      "description": ""
    }
  ],
  "actions": [
    {
      "name": "SendMeSlackMessage",
      "state": "ENABLED",
      "labels": [],
      "description": "",
      "destination": "https://hooks.slack.com/services/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",
      "type": "SLACK"
    }
  ],
  "subscriptions": [
    {
      "name": "MyCustomAlert",
      "conditions": [
        "AlertIsException"
      ],
      "actions": [
        "SendMeSlackMessage"
      ],
      "labels": [],
      "state": "ENABLED",
      "description": ""
    }
  ]
}
```


3. Click on the **Import** button.

![](../../images/b/b2_3_click_import.png)

4. This action will delete our previous configuration, so click on **OK**. 

![](../../images/b/b2_4_click_ok.png)

5. Alert import should be successfull

![](../../images/b/b2_5_import_ok.png)

> Note that if you see the message **Failed to import subscription**, you most probably have missed changing the name of your subscription in point 3.

6. Navigate to the subscriptions screen and verify that this is what you see

![](../../images/b/b2_6_verify_import.png)

## 2. Configure Basic Authentication

We are done with our configuration; what is left to do is to generate a user and password. With them, the application will be able to post the custom alert. 

1. This happens via the **Service Keys** UI of the Alert Notification, so navigate to it and click on the **Create Service Key** button.

![](../../images/b/b2_7_service_keys.png)

2. Copy the configuration below and paste it into **Configuration Parameters (JSON)** this will tell the Alert Notification that we want credential for BASIC authentication and not for OAuth.

```javascript
{"type":"BASIC"}
```

![](../../images/b/b2_8_basic_conf.png)


2. Give your configuration a name something like **basic_auth_service_keys** and click **Save**

![](../../images/b/b2_9_save_conf.png)

3. You should see something like in the picture below.

![](../../images/b/b2_10_verify_conf.png)

4. **This is step is important, do not miss** Open notepad, or other text editor and copy the client_id and client_secret values to it. 

## 3. Explore the Application Code

Now we are good to go. We are ready to post our custom alert. From now on, you have two possible options.

We have created a special Java Servlet in our sample application, that triggers a custom alert. 

1. To locate the servlet open JIdea. Navigate to **TriggerProblem.java** class in the **srv/src/main/java/my/timesheethandson** folder of the sample application.

![](../../images/b/b2_11_navigate.png)

2. Let's explore its code for a while

```java
public class TriggerProblem extends HttpServlet {
	private static final long serialVersionUID = 1L;

	private static final Logger logger = LoggerFactory.getLogger(TriggerProblem.class);

	public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String clientId = request.getParameter("clientId") != null ? request.getParameter("clientId") : "clientId";
		String clientSecret = request.getParameter("clientSecret") != null ? request.getParameter("clientSecret")
				: "clientSecret";

		try (CloseableHttpClient closableClient = HttpClients.createMinimal()) {
			IAlertNotificationClient client = new AlertNotificationClientBuilder(closableClient)
					.withAuthentication(clientId, clientSecret).withServiceRegion(ServiceRegion.EU10).build();
			client.sendEvent(prepareCustomEvent("Custome Alert From the Application",
					"This is a custom alert posted via ANS REST API"));
			response.getWriter().println("Alert posted!");
		} catch (IOException ex) {
			logger.error("Could not initialize closable http client", ex);
			response.getWriter().println("Alert failed to post " + ex.getMessage());
		}
	}

	private CustomerResourceEvent prepareCustomEvent(String subject, String body) {
		return new CustomerResourceEventBuilder().withBody(body).withCategory(EventCategory.EXCEPTION)
				.withSeverity(EventSeverity.ERROR).withSubject(subject).withType("Problem")
				.withAffectedResource(buildResource()).build();
	}

	private AffectedCustomerResource buildResource() {
		return new AffectedCustomerResourceBuilder().withName("Timesheet App").withType("Application").build();

	}
}

```

Alert Notification provides you with a Java-based client which enables custom alerts with a couple of lines of code. The important parts of the code above are:

2.1. This is how you create the client, which will make the REST API calls. We point to the EU10 datacenter, which is where the spaces for this hands-on are created. We also pass the client_id and the client_secret which we have created in the previous section of this exercise.

```java 

  IAlertNotificationClient client = new AlertNotificationClientBuilder(closableClient)
					.withAuthentication(clientId, clientSecret).withServiceRegion(ServiceRegion.EU10).build();
 ``` 

2.2. This is how we send the actual alert. We also set its body and subject.

```java
client.sendEvent(prepareCustomEvent("Custome Alert From the Application",
					"This is a custom alert posted via ANS REST API"));
```
  

## 4. Post the Custom Alert

We are good to go to post our custom Alert. 

1. To do so - in Cloud Cockpit, open your application.

![](../../images/b/b2_12_open_app.png)

2. Click on the app URL

![](../../images/b/b2_13_app_url.png)

3. Now it is time to trigger our alert. To do so, we should tell the TriggerProblem class our **client_id** and **client_secret** that we have generated in the previous steps. To do so in the application URL that you have opened add - /alert.html - the URL should look like this

```
https://<time sheet applciation url>/alert.html
```

4. Once you hit enter a form is going to open, fill the client id and client secret and click on **Submit**.
![](../../images/b/b2_15_post_form.png)

5. You should see a success message.

6. Now in your Slack channel, you should see the alert.

![](../../images/b/b2_14_slack.png)

[![](../../images/nav-previous.png) Previous Exercise](../B1/README.md) ｜[![](../../images/nav-home.png) Overview page](../../README.md) 
