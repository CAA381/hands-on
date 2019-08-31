# Lesson B – Observability and Control of your application
# Exercise B1 -  Configure Custom Alerts

## Objective
You already now how to use tha catalog of alerts of Alert Notification. This catalog is growing and in time you are going to have access to more and more alerts from different SAP Cloud Platform services.
However, thee are some alerts that cannot be into the catalogue, but are quite important. 

Let's put ourselves in the shoes of a developer. Our cloud application is a complex beast, besides all the dependencies and services that it uses it has also quite a decent amount of code. Into that code exceptional situations always occur. For example some of the dependencies we have starts returning unknown to us values and our code does not know what to do. In such kinds of situations, typically a developer would throw an exception. And most probably an operator would like to know that there was such an exceptional situation.

This is where the custom alerts come in play. Alert Notification exposes an REST API **everyone** can post an alert. This means whenever you have an exceptional situation in your application you can all this REST API and it will post an alert for you. See the picture below for reference.

![](../../images/b/b1_2_custom.png)

### What you will learn during the exercise
* You will learn about the import/export feture of SAP Cloud Platform Alert Notification.
* Depending on your choice you are going to code or explore how to post a custom alert.
* You will learn how to configure basic authentication user and password witth which you can use the Alert Notification.

### Estimated Time
30 minutes

## Exercise Steps

1. Import alert subscription into Alert Notification.
2. Configure basic authentication user and password.
3. Explore the application code and how a custom alert is being posted.
4. Post the custom alert.

## Preparation

**You should have your application deployed from the previous Lesson. If you do not have it in your Cloud Platform space, please notify one of the sessions lectors and they will provide it for you.**

## 1. Import Alerts

During exercise B1 we explored how we can create Subscriptions, Actions and Conditions via Cloud Cockpit. During this exercise we are going to use a different approach. We are going to **import** our configuraion. Export/Import feature of SAP Cloud Platform Alert Notification allows us to configure once and then import the configuration into different accounts. This certainly saves a lot of clicking.

**If in the previour exercise you have chose to use your email instead of slack channel please call the session facilitator in order to help you with handling your configuration.**

1. Let's start by opening the Export/Import screen of Alert Notifcation. To do so in Cloud Cokpit - Alert Notification UI click on **Export and Import**

![](../../images/b/b2_1_export_import.png)

2. Now it is time to import our configuraion. We have already defined action (send us the alert to a slack channel). What is left to do is to define a Subsctiption and a Condtion that matches our alert. For that purpose copy the json configuration below. 
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
      "name": "<Your custom alert name>",
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

3. Paste the json into the **Import** field of the Alert Notification UI and **change** the name of the subsription from **\<Your custom alert name>** to **MyCustomAlertLastThreeDigitsOfYourUserName**.

![](../../images/b/b1_2_change_name.png)

4. Click on the **Import** button.

![](../../images/b/b2_3_click_import.png)

5. This action will delete our previours configuration, so click on **OK**. 

![](../../images/b/b2_4_click_ok.png)

6. Alert import should be succesfull

![](../../images/b/b2_5_import_ok.png)

> Note that if you see the message **Failed to import subscription**, you most probably have missed to change the name of your subscription in point 3.

6. Navigate to the subscriptions screen and verify that this is what you see

![](../../images/b/b2_6_verify_import.png)

## 2. Configure Basic Authentication

Once we are done with our configuration. What is left to do is to generate an user and password with which the application will be able to post the custom alert. 

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

## 3. Explore the Application Code

Now we are good to go. We are ready to post our custom alert. From now on you have two possible options.

A) **To Code** - if you want to get your hands dirty and writ a lttile code this is your flow. **Note that this will put additional ~20 minutes on top of the exericse**. 

B) **Not to Code** - this is the main flow of the exercise continuing below


## 4. Post the Custom Alert

[![](../../images/nav-previous.png) Previous Exercise](../B1/README.md) ｜[![](../../images/nav-home.png) Overview page](../../README.md) ｜
