---
title: "Creating an alerting rule group"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rule-groups"
---

Vital Managed Service for Prometheus (VMP) provides you with preset alerting templates for cloud services such as Vital Kubernetes Engine (VKE). The templates apply to major application scenarios of service monitoring. This facilitates you in quickly configuring alerting rules for cloud services. This topic describes how to configure an alerting rule group by using an alerting template.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* VMP has been activated.

* An alert notification policy has been created. For more details, see [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).

* An alert aggregation policy is created. For more details, see [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the navigation pane, click **Alert Center \> Alert rule** to go to the alert rule management page.

3. Click **Create \> Create using template**. Select the desired template and configure policy details as needed, including basic information, alert resources, alert notifications, and more. After completing the configuration, click **Confirm**.

   * **Select ** **template**: Select the template that suits your application scenario. You can select a preset or custom template.

   * **Basic Information**: Configure the basic information about the alert rule.

      
      |Parameter |Descriptions |
      |---|---|
      |Name |Configure a custom name for the alert rule group. |
      |Project |The owning project of the alert rule group. Projects are a platform\-provided resource management mechanism that allows you to group resources for different business applications or projects. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, while streamlining expense allocation and auditing for diverse cloud resources.  |
      |Tags |Tags of the alert rule group. Tags are key\-value pairs used to identify alert rule groups. You can combine tags with selectors to quickly filter target alert rule groups. A tag is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use tags for resource authorization and bill splitting.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 labels.</div><br> |
      

   * **Alert resource**: Configure alert resource information.

      
      |Parameter |Descriptions |
      |---|---|
      |workspace |The workspaces where monitoring data is stored. |
      |Variable |Configure the variable information of the alerting rule group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Variables are used for finer\-grained filtering of monitored cloud service resources. For example, in a <strong>VKE node</strong> template, you can select a VKE cluster by using variables.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Preset variables may vary in different alerting templates. Configure variables based on your business requirements for alerting.</div><br> |
      

   * **Rule preview**: Preview the rules in the template, and configure trigger conditions and trigger policies for each rule.

      
      |Parameter |Descriptions |
      |---|---|
      |Rule toggle |Enable or disable rules. On the right side of the rule list, click the corresponding toggle to enable or disable the rule. |
      |Trigger condition |Select P0, P1, or P2 to set different alert levels. If you do not select an option, alerts at this level are not configured. |
      |Trigger policy |Configure an alert trigger policy. Specify the alert level, condition, threshold, and condition duration.<br><br><br>* Select P0, P1, or P2 to set different alert levels. If you do not select an option, alerts at this level are not configured.<br><br>* **Comparison condition**: Specify the comparison condition between the PromQL statement and the threshold. You can configure multiple comparison conditions. Valid values: **Greater than**, **Greater than or equal to**, **Less than**, **Less than or equal to**, **Equal to**, and **Not equal to**.<br><br>* **Threshold**: Set the threshold of the metric.<br><br>* **Condition duration**: Configures the duration for which the metric meets the condition. Valid values:<br><br>   * **Trigger immediately**: triggers an alert immediately if the alerting condition is met.<br><br>   * **Custom duration**: Select an alert trigger time. Available options include 1 minute, 2 minutes, 5 minutes, 10 minutes, 20 minutes, 30 minutes, 1 hour, 3 hours, 6 hours, and 12 hours. For example, 1 minute means that the alert will be triggered after the condition has been met for 1 minute. |
      

   * **Alert notification**: Select a suitable notification policy and aggregation policy from the Unified Alert Center or the Original VMP alert policy tab.

      
      |Parameter |Descriptions |
      |---|---|
      |Notification policy |Select an alerting notification policy from the Notify policy list. The system will send alerts to the specified contacts based on the alert levels and contact groups configured in the notification policy. For more details, see [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules). |
      |Aggregation policy |Select an alerting aggregation policy from the Aggregation policy list. For more details, see [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules). |
