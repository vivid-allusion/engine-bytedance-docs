---
title: "Alerting templates"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Alert_templates"
---

In an alert template, alert rules and application scopes are independent of each other. You can configure different alert rules and application scopes separately to quickly generate alert tasks. The alert template provides the ability to inject alert rules, solving the problem of batch configuration.

<span id=".6YCa6L-H5oql6K2m5qih5p2_55Sf5oiQ5oql6K2m5Lu75Yqh"></span>
## Generate alert tasks through the alert template

After configuring alert rules and application scopes, they are combined to automatically generate alert tasks. Alert task generation logic:

Because alert rules and application scopes are independent of each other, you can edit alert rules or application scopes separately in a configured alert template. When you edit both alert rules and application scopes, see the following description to determine whether submitting the alert template affects existing alert tasks or generates new alert tasks.

Does editing the alert template affect **existing alert tasks**:

Does editing the alert template **generate new alert tasks**:

<span id=".5Yib5bu65oql6K2m5qih5p2_"></span>
## Create an alert template


1. Login [Application Performance Monitoring Console](https://console.byteplus.com/observe/apmplus-server). 

2. Select the service region.

3. In the upper left corner of the console, select **Alert Management \> Alert Template**.

4. On the **Alert Template** page, click **Create Alert Template**.

7. On the **Create Alert Template** page, complete the configuration, then click **Confirm**.

   Parameter description:

   * **Template name**: Custom name used to identify the template.

   * **Template type**: Only the service alert type is supported.

      After creation, you are automatically redirected to the **Template Details** page.

8. Click **Add Alert Rule**.

9. On the **Create Alert Rule** page, complete the configuration, then click **Save**.

   Parameter description:

   
   |**Configuration area** |**Parameter** |**Descriptions** |
   |---|---|---|
   |Basic information |Alert rule name |Custom name used to identify the alert rule. |
   |Alert Strategy |Alert level |Multiple alert levels can be selected, and different alert levels can be set for different metric values.<br><br><br>* **Notice**: Note<br><br>* **Warn**: Warning<br><br>* **Fatal**: Critical |
   ||Alert engine |Threshold engine. |
   ||Relationships among multiple policies |When configuring multiple policies, you can set relationships between policies.<br><br><br>* **All policies met**: This is the default configuration. Alerts are triggered only when all policies are satisfied.<br><br>* **Any policy met**: Alerts are triggered when any one of the policies is satisfied. |
   ||Alert Trigger Policy |* **Alert query**: Different alert types have different metrics.<br><br>   * **Filter condition**: Based on the metric, add filter conditions to locate more precise data.<br><br>      Filter conditions include: service type, service name, interface name, downstream service type, downstream service name, downstream interface name, status code, host, and process ID.<br><br>   * **Grouping**: Supports multi\-dimensional grouping.<br><br>      After turning on grouped alerts, an alert is triggered if any group meets the alert condition. For example, if there are multiple services and service grouping is enabled, an alert is triggered if any service meets the alert threshold. This feature allows a single alert rule to monitor and alert for all groups.<br><br>* **Trigger condition**: The AVG/SUM/MAX/MIN value reaches the set value within a certain period of time.<br><br>   * **AVG**: The average value of the metric within N minutes<br><br>   * **SUM**: The sum of metrics within N minutes<br><br>   * **MAX**: The maximum value of metrics within N minutes<br><br>   * **MIN**: The minimum value of metrics within N minutes<br><br>   * **阈值**: When the number of exceptions within a single time window reaches a certain amount, an alert will be triggered.<br><br>   * **比**: Indicates whether the increase or decrease in the value within a single time window, compared to the value in the same time window n time units earlier, exceeds the set threshold. |
   ||No data policy |Method for handling the absence of data.<br><br><br>* **Ignore**<br><br>* **Notify about absence of data.**  |
   ||Custom tag |Custom tag and value. You can filter the alert list by tag. |
   |Alert sending policy |Rule execution frequency |Set the rule execution frequency (every few minutes). The default is once per minute. |
   ||Sending policy |* Set the sending interval; by default, one minute is used as a sending interval.<br><br>* Set which alert occurrence within a sending interval triggers the alert notification. By default, if an alert is triggered once within a sending interval, the alert is sent on the first occurrence. |
   ||Send rate limiting |When enabled, if alerts are triggered continuously, the sending interval will gradually increase.<br><br>The decay policy is: next sending interval = current sending interval \* 2. For example, the first sending interval is 1 minute, the second is 2 minutes, the third is 4 minutes, the fourth is 8 minutes, and so on. |
   ||Alert batch aggregation interval |Set alert aggregation for intervals not exceeding n minutes.<br><br><br>* When an alert is generated, if there is an alert within the previous n minutes, it will be merged into one alert group with alerts from the previous n minutes.<br><br>* When an alert is generated, if there is no alert within the previous n minutes, a new alert group will be created and will not be merged with alerts from the previous n minutes. |
   

10. Click the **Application Scope** tab, then click **Add Application Scope**.

11. On the **Apply to Service** page, complete the configuration, then click **Confirm**.

   Parameter description:



|**Configuration Area** |**Parameter** |**Descriptions** |
|---|---|---|
|Select Service |Language |Filter by service language. For example, Go, Java. |
||Monitoring system |Filter through the monitoring system. For example, APMPlus, OpenTelemetry. |
||Service Type |Filter by service type. For example, http, consumer. |
||Service |Select the services to which the alert template needs to be applied. |
|Notification method |Alert method |Alerts are supported via **email**, **Feishu Webhook**, and **alert callback**. |
||Email notification recipient/group |Configure email notification recipients or groups. When an alert occurs, the designated recipient or group will receive a notification. This field is required when the alert method is set to email. |
||Escalation notification recipient/group |Configure email recipients or notification groups. If five alerts are sent within 30 minutes and not acknowledged (ACK), the recipient or group can receive notifications. This field is optional when email is selected as the alert method. |
||Feishu Webhook |Configure the Feishu Webhook address. This field is required when the alert method is set to Feishu Webhook.<br><br>For details on webhook configuration, see [How to configure a webhook?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook). |
||Webhook |Configure a publicly accessible URL to push alert information to this address via a POST request. This field is required when the alert method is set to alert callback. |



12. Return to the **Template Details** page, then click **Submit**.

13. In the **Submit** dialog box, click **Confirm**. The console will automatically generate alert tasks.


<span id=".57yW6L6R5oql6K2m5qih5p2_"></span>
## Edit alert template


1. Login [Application Performance Monitoring Console](https://console.byteplus.com/observe/apmplus-server). 

2. In the upper left corner of the console, select **Alert Management \> Alert Template**.

3. In the alert template list, find the target template. In the **Actions** column on the right, click **Edit**.

7. Edit alert rule.

   
   |Action category |Step |
   |---|---|
   |Add Alert Rule |For detailed operations and parameter descriptions, see [Create alert template](https://docs.byteplus.com/en/docs/apmplus/Alert_templates#.5Yib5bu65oql6K2m5qih5p2_). |
   |Change an existing alert rule |1. On the **Alert Rule** page, find the target alert rule and click **Edit** in the Actions column on the right.<br><br>2. On the **Edit Alert Rule** page, modify the configuration and then click **Save**.<br><br>3. In the **Select Change Method** dialog box, select the change method and then click the Submit button. |
   |Delete an existing alert rule |1. On the **Alert rule** page, locate the target alert rule, and in the Actions column on the right, click **delete**.<br><br>2. On the **Delete alert rule** page, select and associate the relationship with the alert task, and then click **confirm delete**. |
   

8. Edit application scope.

   
   |Actions Category |Steps |
   |---|---|
   |Add scope of application |For detailed operations and parameter descriptions, see [Create alert template](https://docs.byteplus.com/en/docs/apmplus/Alert_templates#.5Yib5bu65oql6K2m5qih5p2_). |
   |Change an existing application scope |1. Click the **Application scope** tab, locate the target application scope, and in the Actions column on the right, click **edit**.<br><br>2. On the **Apply to service** page, modify the configuration, and then click **confirm**.<br><br>3. In the **Select change method** dialog box, select the change method, and then click the submit button. |
   |Delete the existing application scope |1. On the **Application scope** page, locate the target application scope, and in the Actions column on the right, click **delete**.<br><br>2. On the **Delete application scope** page, select and associate the relationship with the alert task, and then click **confirm delete**. |
   

9. Return to the **Template Details** page, then click **Submit**.

10. In the **Submit** dialog box, click **Confirm**.


<span id=".5Yig6Zmk5oql6K2m5qih5p2_"></span>
## Delete alert template

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting an alert template will also delete the corresponding alert rules, application scope, and alert tasks. Please proceed with caution.</div>



1. Login [Application Performance Monitoring Console](https://console.byteplus.com/observe/apmplus-server). 

2. Select the service region.

3. In the upper left corner of the console, select **Alert Management \> Alert Template**.

4. In the alert template list, find the target template. In the **Actions** column on the right, click **Delete**.

7. In the **Delete Alert Template** dialog box, select how to handle the relationship with associated alert tasks, and then click **Confirm Delete**.

   * **Delete template, disassociate alert task**: Delete this alert template and retain the alert tasks generated by the template.

   * **Delete template and associated alert tasks**: Delete this alert template and delete the alert tasks generated by the template.


<span id="cXsM9Bdv"></span>
## Apply a preset alert template


1. Log in [Application Performance Monitoring Console](https://console.byteplus.com/observe/apmplus-server). 

2. Select **Alert Template** in the left navigation bar, click the **Preset Alert Template** tab to view the preset alert templates provided by the system. Preset alert templates can be filtered by alert type.

3. Click **Apply** in the Actions column on the right side of the target template to go to the **Alert Rule** tab on the Preset Alert Template Details page and view the detailed configuration of the alert rule.

4. Go to the **Application Scope** tab, click **Add Application Scope**, and configure the application scope for the alert.

   
   |Parameter |Descriptions |
   |---|---|
   |Service scope |The service scope to which the current alert template applies.<br><br><br>* **All ** **services**: The alert rules in the template apply to all services, including those added later.<br><br>* **Filter services**: Specify certain services to apply the alert rules in the template. Filtering by platform or service name is supported. |
   |Notification method |The receiving method for notification messages supports email, Feishu Webhook, and alert callback. You can select the appropriate option based on your needs. |
   |Project |Select the appropriate project based on actual requirements. Project management is a resource management method provided by the platform, which allows you to group and manage cloud resources used by different businesses or projects. |
   

6. Return to the preset alert template details page, click **Submit** in the alert change prompt, and the system will automatically create alert tasks according to the configuration and monitor the metric health status in real time.


&nbsp;

&nbsp;

&nbsp;
