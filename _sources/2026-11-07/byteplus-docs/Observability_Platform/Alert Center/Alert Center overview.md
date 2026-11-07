---
title: "Alert Center overview"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Alert_Center_overview"
---

The Alert Center is a unified alert management module provided by Observability Platform for all observability products. It not only normalizes alert and notification configuration data, but also provides a centralized entry point for managing alert rules. This breaks down alert configuration silos across observability products and lays the foundation for improving the standardization and maintainability of the overall observability system.


* The Alert Center of Observability Platform provides unified management of configuration data for policies such as notification policies, aggregation policies, and suppression policies, as well as notification objects such as contacts, contact groups, callback addresses, and on\-call schedules. Observability products such as Cloud Monitor, Server\-side Monitoring, and VMP share a single data source. This reduces rule maintenance costs and improves the consistency and reusability of alert rules.

* The Alert Center of Observability Platform consolidates the configuration entry points for alert rules (including Cloud Monitor alert rules and cloud service event rules) into the "Alert settings" module for centralized management. This facilitates continuous platform\-level development of alert governance, rule auditing, policy optimization, and alert operations capabilities, enhancing the maintainability and scalability of the overall observability system.


<span id="rPdohwEs"></span>
## Alert principles

During the operation of cloud services, when a metric triggers the alert condition in an alert rule, the generated alert message is processed through the aggregation policy and suppression policy for alert aggregation and suppression. A notification is then sent based on the channels, notification methods, and contacts configured in the notification policy, ensuring that the alert reaches contacts in a timely manner and is promptly handled.


* **Alert policy**: Specifies the objects and rules that trigger alerts. To monitor the data status of a cloud service resource, you can create an alert policy. When the data of the monitored resource reaches the alert trigger condition, the system will send an alert notification using the specified method, allowing recipients to identify resources with anomalies in a timely manner.

* **Aggregation policy**: Primarily used to configure the aggregation cycle for alerts. It groups a batch of alerts together for notification, preventing alert storms caused by a large number of alert messages generated in a short period when alerts are triggered frequently.

* **Suppression policy**: Primarily used to suppress frequent but unimportant alerts, preventing them from overwhelming more important alert notifications and allowing recipients to focus on issues that truly matter.

* **Notification policy**: Defines the recipients, delivery channels, and content display format for alert notifications when alerts of different levels are triggered or recovered.


<span id="YhYh9wJK"></span>
## Notification methods

Supported notification methods vary by cloud service.


|Notification methods |Cloud Monitor |Cloud product event |Vital Managed Service for Prometheus |Server\-side Monitoring |
|---|---|---|---|---|
|Phone call |✅ |✅ |✅ |✅ |
|Text message |✅ |✅ |✅ |✅ |
|Email |✅ |✅ |✅ |✅ |
|Feishu group bot |✅ |✅ |✅ |✅ |
|Feishu application bot |✅ |✅ |✅ |✅ |
|DingTalk |✅ |✅ |✅ |✅ |
|WeCom |✅ |✅ |✅ |✅ |
|Slack |✅ |✅ |✅ |✅ |
|General callback address |✅ |✅ |✅ |✅ |
|Orchestration |✅ |✅ |❌ |❌ |
|Message queue |❌ |✅ |❌ |❌ |
|Torch Log Service (TLS) |❌ |✅ |❌ |❌ |


<span id="0RBoBRkb"></span>
## Procedure


1. **Configure notification methods**: Select and configure the methods for receiving notification messages based on your actual scenario. For example, configure a Feishu bot or a Feishu application bot.

   * For the notification methods supported by different products, see the **Notification methods** section in this topic.

   * For configuration instructions for common notification methods, see [Configuring notification methods](https://docs.byteplus.com/en/docs/Observability_Platform/Notification_method).

2. **Create notification objects**: Configure the channels and objects for receiving notification messages based on your actual needs to ensure timely receipt of notifications.

   * You can directly specify contacts, contact groups, or callback addresses as the objects to receive notification messages. For more information, see [Notification objects](https://docs.byteplus.com/en/docs/Observability_Platform/Notification_objects).

   * You can assign on\-call personnel for specific time periods as the objects to receive notification messages. For more information, see [Creating on-call schedules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_on-call_schedules).

3. [Create a notification template](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_templates): Specify the type, channel, style, and other information for message notifications to improve the standardization and readability of notification messages.

4. [Create a notification policy](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies): Specify the methods, objects, template, and other information for receiving notifications when alerts of different levels are triggered or recovered.

5. [Create an aggregation policy](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies): (Optional) Configure the aggregation cycle for alerts to group a batch of alerts together for notification, preventing alert storms caused by a large number of alert messages generated in a short period when alerts are triggered frequently.

6. [Create a suppression policy](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_silence_policies): (Optional) Suppress frequent but unimportant alerts to prevent them from overwhelming more important alert notifications, allowing recipients to focus on issues that truly matter.

7. **Configure alert rules**: Configure alert trigger rules and notification policies for resources in each product as needed. When an alert is triggered, notification messages will be sent to the specified contacts. For configuration examples, see [Creating Cloud Monitor alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Cloud_Monitor_alert_rules), [Creating cloud service event rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_cloud_service_event_rules), [Creating VMP alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rules), and [Creating Server-side Monitoring alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Server-side_Monitoring_alert_rules).

8. [View alert history](https://docs.byteplus.com/en/docs/Observability_Platform/Alert_history): When a monitored resource reaches the threshold configured in the alert rule, an alert is triggered, and a notification message is received. The system also records alert events and notification history to facilitate traceability and troubleshooting.
