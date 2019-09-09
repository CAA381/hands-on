# Lesson B – Observability and Control of your application
# Exercise B1 - Configure Alerts for App State Changes

## Objective
As you can notice from the diagrams, our solution consists of multiple components. It has a front end module, a backend module and a database. One of the most common situations that might happen to us is the crash (or stop) of some of those components. Usually, as  DevOps engineers, we would like to understand about such situations, since this stoppage might be unplanned and we need to react with actions like - restarting the application.

Cloud Controller interacts with applications and allows operators to do actions such as staging applications, starting or stopping applications, collecting health information.

Alert Notification integrates well with Cloud Controller, and it understands for every given event that happens with your application.


### What you will learn during the exercise
* You will explore the Cloud Cockpit.
* You will learn how to configure alerts for app state changes.
* You will explore the different states of a cloud application.
* You will learn how to receive the defined alerts via Slack and/or email.

### Estimated Time
25 minutes

## Exercise Steps

This exercise consists of a couple of steps.
![](../../images/b/b1_1_overview.png)

1. Subscribe for the alerts coming from Cloud Controller
2. Configure our output channels - like Slack and email.
3. Stop our application and receive the alert.

## Preparation

**You should have your application deployed from the previous Lesson. If you do not have it in your Cloud Platform space, please notify one of the sessions lectors, and they will provide it for you.**

## 1. Configure Alert Notification

1. Logon to [Cloud Cockpit](https://account.hana.ondemand.com/cockpit). Use the user and password provided in the hand-out papers on your desk. In the Global Accounts section select **TechEd2019**
![](../../images/b/b1_1_ga_home.png)

2. In the Subacount section select this session's subaccount **CAA381cf**
![](../../images/b/b1_2_subbaccount.png)


3. Navigate to the Spaces section and click on your space. **The space name is the same as your username.**
![](../../images/b/b1_4_click_on_space.png)

4. Drop down the **Services** section and click on Service Instances. Click on the **alert-notifiction-instance<x>**
![](../../images/b/b1_7_open_ans.png)

5. Open the Subscriptions section and click the **Create** button
![](../../images/b/b1_9_create.png)

6. In the pop-up screen fill the condition name to be **ApplicationStateChanged< The last three digits of your username >**. For example, AppHasStopped000. **You can set any other name, that you like**. Then click on the **Create** button.
![](../../images/b/b1_12_create_sub.png)

7. Click on **Create Condition**
 
![](../../images/b/b1_12_create_cond.png)

8. Now it is time to create our condition, against which the alert is going to match.

   1. Give the condition some meaningful name. For example **ApplicationStateHasBeenUpdated**
   2. Under Labels fill **AppStates** and hit enter or tab 
   > If you have a lot of subscriptions and conditions, the labels help you filter later on. 
   3. Under Condition select **eventType** 
   > Every alert coming from Alert Notification has the same model. It has eventType, subject, body and more fields. Alert Notification exposes a catalogue for alerts provided from the platform. In that catalogue you can see what the different values for certain field of an alert are. In our case [this is the catalogue entry](https://help.sap.com/viewer/5967a369d4b74f7a9c2b91f5df8e6ab6/Cloud/en-US/4255e6064ea44f20a540c5ae0804500d.html) that we are interested in.
   4. From the dropdown select **Is Equal To**
   5. Then in the text field fill **audit.app.update**
   6. Click on **Create** button
   > This condition tells Alert Notification **Please send me an alert every time the state of my application changes, no matter if it is a stop/start/crash or something else**
![](../../images/b/b1_12_condition_stop.png)

9. On the next screen click on **Assign**

10. Now it is time to tell Alert Notification where we want to receive those alerts. In the next screen click on the **+ Create Action link**
![](../../images/b/b1_16_create_action.png)

11. In the next screen select **Slack**. Slack is a cloud-based set of proprietary team collaboration software tools and online services. With Slack, you can manage different channels of communication, including automatic messaging.
   1. Click on the Slack radio button
   2. click Next
   ![](../../images/b/b1_17_select_slack.png)

12.Copy this link ```https://hooks.slack.com/services/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```.
      1. In **URL Address** paste the copied URL
      2. In the name field type **PostToMySlackChannel**
      3. In Labels type **AppStates** and click tab or enter
      4. Make sure that State is **ON**
      5. Click on **Create** button
      
![](../../images/b/b1_18_configure_web_hook.png)


> **Note:** Slack uses channels, where you can receive
your alerts. To integrate Alert Notification with Slack, one would need a [webhook](https://en.wikipedia.org/wiki/Webhook). In order not to bother you with Slack configurations we have pre-configured those webhooks for you. However, if you want to learn more about how to configure Slack, click [here](https://help.sap.com/viewer/5967a369d4b74f7a9c2b91f5df8e6ab6/Cloud/en-US/88a4774f9d3f43259b4dc9e7e7729829.html?q=slack)

13. On the next screen review and click **Assign**. Note that this is a **demo account**, however, in a productive environment you will have to make opt-in from Slack and confirm from within Slack
![](../../images/b/b1_19_assign_action.png)

14. Review the final summary and click **Close**
![](../../images/b/b1_20_summary.png)

## 2. Stop your application and Receive alerts

Now, once we are ready with our configuration, all that is left to see how it works. For that purpose, execute the following steps:
1. Open Slack by clicking here. Authenticate with the provided email and password on your hands-on sheets.
2. In the Cloud Cockpit click on your space name and then select the Applications section
![](../../images/b/b1_28_open_apps.png)
3. Select your running application
![](../../images/b/b1_29_select_app.png)
4. Click the Stop button of your application
![](../../images/b/b1_30_stop_app.png)
5. Open your [Slack Channel](https://caa381.slack.com). Authenticate with the provided email and password on the paper on your desk.
![](../../images/b/b1_31_open_slack.png)
5. On the left-hand side, you will see the Slack Channels. Click on # caa381-2019
6. If you are not the first who has posted an alert, you will see multiple alerts here. This is so because everybody from this exercise posts alerts onto that channel. To find yours you should search the alert by your space name. To do so go back to **Cloud Cockpit** and in the browser URL locate the **space** guid. Select the guid and copy it.
![](../../images/b/b1_32_space_guid.png)

7. Back in slack in the upper right corner, you are going to find the **Search** field. Click on it and **paste** the space guid. Then hit enter.
![](../../images/b/b1_33_search_field.png.png)

8. You should see the following result. And that is your alert. You can click on **view in channel** to see the alert into the slack channel itself.
![](../../images/b/b1_34_search_result.png)


[![](../../images/nav-previous.png) Lesson Overview](../../overviews/B/README.md) ｜ [![](../../images/nav-home.png) Overview page](../../README.md) ｜ [Next Exercise ![](../../images/nav-next.png)](../B2/README.md)
