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

## 2. Configure Basic Authentication

## 3. Explore the Application Code

## 4. Post the Custom Alert
