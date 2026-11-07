---
title: "Glossary"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Terms"
---

Before you use the Cloud Monitor service, you need to first understand the basic concepts. This helps you effectively use this service.

<span id=".5Zyw5Z-f77yIUmVnaW9u77yJ"></span>
## Region

Regions refer to geographical locations where physical data centers are deployed, which are isolated from each other based on the internal network. You can filter and view the monitoring information of cloud products in different regions.

<span id=".5LqR5Lqn5ZOB55uR5o6n"></span>
## Cloud product monitoring

A capability of Cloud Monitor that allows you to view the monitoring information of resources for each cloud product within the current account. For the list of supported cloud products, see [Cloud product metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).

<span id=".55uR5o6n5oyH5qCH"></span>
## Metric

The type of monitoring data of cloud products, such as CPU utilization and memory utilization of ECS. A series of monitoring data is collected for each metric over time. You can learn about the usage of cloud resources based on the changes in the monitoring data.

<span id=".6ZiI5YC85ZGK6K2m"></span>
## Threshold alert

If you have specific expectations for the performance consumption of your cloud resources, you can set thresholds for their various metrics. The system will then automatically send alert notifications if monitoring data reaches these thresholds. This enables you to promptly identify resource exceptions.

<span id=".5ZGK6K2m562W55Wl"></span>
## Alert policy

An alert policy is a specific description of a threshold alert, which consists of an alert name, alert resource type, alert trigger condition, alert contact, and alert channel. The system will monitor the metrics based on the policy you set and send alert notifications.

<span id=".5ZGK6K2m6LWE5rqQ57G75Z6L"></span>
### Alert resource type

It is used to identify which type of cloud product the alert policy applies to. When you select **ECS**, the alert policy will be set for the metrics of ECS resources.

<span id=".5ZGK6K2m6Kem5Y-R5p2h5Lu2"></span>
### Alert trigger condition

The alert trigger condition for a metric, which is a semantic condition consisting of the metric type, threshold, statistical period, and duration.

<span id=".5ZGK6K2m6IGU57O75Lq6"></span>
### Alert contact

The detailed method of receiving alert notifications.

<span id=".5ZGK6K2m6IGU57O757uE"></span>
### Alert contact group

An alert contact group can consist of one or more alert contacts. When you create an alert policy, you need to select a contact group. After an alert is triggered, alert notifications are sent to all contacts in the contact group.

<span id=".5ZGK6K2m5rig6YGT"></span>
### Alert channel

The method of sending alert notifications. Currently, emails, phone calls, SMS messages, and alert callbacks are supported. Alert callbacks push detailed alert information to servers by using POST requests. This helps you build intelligent programs to handle alerts.
