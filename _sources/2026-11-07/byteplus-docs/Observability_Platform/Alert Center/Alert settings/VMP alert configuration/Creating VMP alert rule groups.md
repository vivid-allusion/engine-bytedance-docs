---
title: "Creating VMP alert rule groups"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_rule_groups"
---

An alert rule group is a collection of alert rules. You can configure an alert rule group by applying a custom or preset alert template in VMP, which helps you quickly complete alert rule configuration for cloud products. This topic describes how to create an alert rule group by using an alert template.

<span id="Gx3TwIY3"></span>
## Prerequisites


* You have created an alert notification policy that specifies the contacts who receive notification messages, the notification template, and other information. For detailed instructions, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

* You have created an alert aggregation policy to aggregate alert notifications and prevent alert storms. For more details, see [Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies).

* (Optional) If you want to create an alert rule group by using a custom alert template, create the alert template in advance. For more details, see [Creating VMP alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_VMP_alert_templates).


<span id="1Im5CPi9"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click ** Alert Center \> Alert Configuration** to go to the Alert Configuration management page.

3. In the Alert Configuration section on the left, select **VMP** and click the **Alert rule group** tab.

4. Click **Create alert rule group**. On the configuration page, select the target template. You can select a custom or preset alert template. After selection, click **Next**.

5. Configure the information for the alert rule group, and then click **Confirm**.

   
   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Name |Configure a custom name for the alert rule group. |
   ||Project |The owning project of the alert rule group. Projects are a platform\-provided resource management mechanism that allows you to group resources for different business applications or projects.<br><br>Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">VMP alert rule groups are added to the default project by default, which cannot be modified.</div><br> |
   ||Tags |The tags attached to the alert rule group. Tags are key\-value pairs used to identify alert rule groups. You can combine tags with selectors to quickly filter target alert rule groups.<br><br>A tag is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use tags for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 tags to an alert rule group.</div><br> |
   |Alert resource |workspace |The workspace to monitor and trigger alerts for.<br><br>The workspace of Vital Managed Service for Prometheus (VMP) is an abstract integration of data and collection rules, which provides users with standard cloud Prometheus capabilities. For more details, see[ Workspace overview](https://docs.byteplus.com/en/docs/vmp/Workspace-overview). |
   |Alert notification |Notification policy |Select an alert notification policy. The system sends alerts to the specified contacts based on the alert levels and contact groups configured in the notification policy. For notification policy details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies). |
   ||Aggregation policies |Select an alert aggregation policy. An aggregation policy is primarily used to configure the aggregation cycle for alerts. It groups a batch of alerts for notification, preventing a large number of alert messages from being generated in a short period when alerts are triggered frequently. For detailed instructions, see[ Creating aggregation policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies). |
   |Variable |Variable |Configure the variable information of the alerting rule group.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Variables are used for finer\-grained filtering of monitored cloud service resources. For example, in a VKE node template, you can select a VKE cluster by using variables.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Preset variables may vary in different alert templates. Configure variables based on your business requirements for alerting.</div><br> |
   |Rule preview |Rule configuration |You can preview the alert rules configured in the template. You can adjust the trigger condition, trigger policy, label, annotation, and enabled status for each rule. |
   ||Metric preview |In the "Actions" column to the right of the target rule, click "**Metric preview**" to compare the original input with the final query statement after variable substitution. You can also preview the metric chart with the data from the last hour. |
   


<span id="3aFmCNhp"></span>
## Validate results


* After the alert rule group is created, return to the alert rule group management tab to view the created alert rule group and its details, such as the associated template, version, workspace, notification policy, and aggregation policy.

* Switch to the "Alert Rule" tab to view the alert rules associated with the current alert rule group and rule details.
