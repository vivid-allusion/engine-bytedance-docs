---
title: "Creating an alert policy"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy"
---

If you need to monitor the data status of a specific cloud service resource, you can create a Cloud Monitor alert policy. When the data of the monitored cloud service resource meets the alert trigger condition, the system will push an alert notification through your specified method, which helps you identify resources with abnormal data at the earliest opportunity.

<span id="gLFAGZgF"></span>
## Prerequisites

You have selected an appropriate notification method and created a matching notification policy. For more details, see[ Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

<span id="09b646db"></span>
## Limits

<span id="20bd51b4"></span>
### General limit


* When you **manually select** resources, if you select **all** resources, the number of resources is not limited.

* When you **manually select** resources, if you select **part of** resources, the number of resources is limited by the following rules:

   * Up to 1,000 resources of the same type can be added to an alert policy.

   * Up to 5,000 resources of all types can be added to an alert policy.

* When you select resources by **resource name**, **project** and **label**, up to 1000 resources can be matched.


<span id="380a0aa6"></span>
### Select resources by **project**

The following cloud services allow you to select resources by **project**.


|**Service name** |**Namespace** |
|---|---|
|NAT Gateway |VCM_NAT |
|Classic Load Balancer (CLB) |VCM_CLB |
|EIP |VCM_EIP |
|Bandwidth Package |VCM_BandwidthPackage |
|TR |VCM_TransitRouter |
|Transit Router (TR) Bandwidth Package |VCM_TransitRouterBandwidthPackage |
|RDS for MySQL |VCM_RDS_MySQL |
|Cache for Redis \- Community Edition |VCM_Redis |
|Elastic Compute Service (ECS) |VCM_ECS |
|EBS |VCM_EBS |
|Cloud Enterprise Network (CEN) |VCM_CEN |
|Application Load Balancer (ALB) |VCM_ALB |
|Torch Object Storage (TOS) |VCM_TOS |
|RDS for PostgreSQL |VCM_RDS_PostgreSQL |
|Document Database for MongoDB \- replica set |VCM_MongoDB_Replica |
|Document Database for MongoDB \- sharding cluster |VCM_MongoDB_Sharded_Cluster |


<span id="626e0f4d"></span>
### Select resources by label

The following cloud services allow you to select resources by **label**.


|**Service name** |**Namespace** |
|---|---|
|NAT Gateway |VCM_NAT |
|Classic Load Balancer (CLB) |VCM_CLB |
|EIP |VCM_EIP |
|Bandwidth Package |VCM_BandwidthPackage |
|Cloud Enterprise Network (CEN) |VCM_CEN |
|Direct Connect (DC) \- DC gateway |VCM_DirectConnectGateway |
|DC \- virtual interface |VCM_DirectConnectVIF |
|Cache for Redis Community Edition |VCM_Redis |
|Elastic Compute Service (ECS) |VCM_ECS |
|EBS |VCM_EBS |
|RDS for MySQL |VCM_RDS_MySQL |
|Application Load Balancer (ALB) |VCM_ALB |
|Torch Object Storage (TOS) |VCM_TOS |
|RDS for PostgreSQL |VCM_RDS_PostgreSQL |
|Document Database for MongoDB \- replica set |VCM_MongoDB_Replica |
|Document Database for MongoDB \- sharding cluster |VCM_MongoDB_Sharded_Cluster |


<span id="8ff5ddae"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/observe/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center \> alert policy**. Click **Create alert policy** to configure the alert policy details.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Available regions and subnamespaces vary based on the cloud service type. The options displayed in the console shall prevail.   </div>
   

   
   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Name |Specify a name for the Cloud Monitor alert rule as a unique identifier. Duplicate names are not allowed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Alert notifications sent through SMS messages may fail to be delivered if certain characters are used in the name.</div><br> |
   |Alert object |Resource type |Specify the type of cloud products under monitoring. Supported cloud service types displayed in the console shall prevail. |
   ||Subnamespace |Specify the resource subnamespace of the monitored cloud service. |
   ||Selection method |* **Manually select**: Manually select resources.<br><br>* **Resource name**: Match resources by resource name.<br><br>* **Object Group**: Select resources based on object groups. For details, see [Creating object groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group).<br><br>* **Project**: selects resources based on projects. <br><br>* **Label**: selects resources based on labels.  |
   ||Region |If you set the **Selection method** parameter to **Manual selection**, **Resource name**, **Project**, or **Label**, you can select one or more regions to which the monitored resources are deployed. |
   ||Resource group |If you set the **Selection method** parameter to **Object Group**, you can select a created Object Group. |
   ||Resource |If you set the **Selection method** parameter to **Manual selection**, you can specify a resource range to which the alert policy applies, which means only resources within the resource range can be monitored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select <strong>all resources</strong>, the number of resources is not limited.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select <strong>part of</strong> resources, the number of resources is limited by the following rules:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Up to 1,000 resources of the same type can be added to an alert policy.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Up to 5,000 resources of all types can be added to an alert policy.</div><br><br><br>* **All**: The alarm strategy is configured for all resources matching the specified resource type, region, and subnamespace within the current account.<br><br>   After selection, newly created resources that meet these conditions will be automatically added to the alert policy.<br><br>* **Part**: You need to manually select one or more resources.<br><br>   After selection, the alert policy is configured only for these resources. |
   ||Resource name |If you set the **Selection method** parameter to **Resource name**, you can specify a resource range to which the alert policy applies, which means only resources within the resource range can be monitored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can add multiple matching rules. Up to 10 matching rules can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The resource name can be up to 100 characters in length.</div><br><br><br>* You can select the relationship between matching rules, which include **arbitrary satisfaction** and **All satisfied**.<br><br>* If you select Specific resources, you can match resources by resource name. The matching rules include **Prefix match**, **Suffix match**, **Contain**, **Not contain**, **Equal to**, and **Not equal to**.<br><br>   * If you set the **matching rule** to **Contain**, **Not contain**, **Prefix match**, or **Suffix match**, you can enter one resource name.<br><br>   * If you set the **matching rule** to **Equal to** or **Not equal to**, you can select multiple resources and must specify the **Region** parameter. |
   ||Project |If you set the **Selection method** parameter to **Project**, you can specify a resource range to which the alert policy applies, which means only resources within the resource range can be monitored. For supported cloud services, refer to the [Select resources by project](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy#380a0aa6) section of this topic. |
   ||Tags |If you set the **Selection method** parameter to **Label**, you can specify a resource range to which the alert policy applies, which means only resources within the resource range can be monitored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can add multiple matching rules. Up to 10 matching rules can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The tag value can be up to 50 characters in length.</div><br><br><br>* For supported cloud services, refer to the [Select resources by label](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy#626e0f4d) section of this topic.<br><br>* You can select the relationship between matching rules, which include **arbitrary satisfaction** and **All satisfied**.<br><br>* You can select a label key and filter resources with the label key by the following rules, including **Exists and the prefix matches**, **Exists and the suffix matches**, **Exists and contains**, **Exists and does not contain**, **Exists and is equal to**, **Exists, but not equal to**, **Exist**, and Does not exist.<br><br>   * If you set the **matching rule** to **Exist or Does not exist**, all label values of the corresponding label keys are included, and you cannot enter a label value.<br><br>   * If you set the **matching rule** to **Exists and is equal to** or **Exists, but not equal to**, you can select multiple label values.<br><br>   * If you set the **matching rule** to **Exists and contains**, **Exists and does not contain**, **Exists and the prefix matches**, or **Exists and the suffix matches**, you can enter one label value. |
   |Alert rules |Preset trigger condition<br><br> |The preset alert trigger conditions. Click **Use preset trigger conditions** and the system will automatically populate the metric type and trigger condition. You can modify, delete, and add automatically generated trigger conditions.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a certain <strong>dimension</strong> of a cloud product does not have preset trigger conditions, this button will be grayed out and trigger conditions cannot be generated automatically.</div><br> |
   ||Metric type |Select the metric type. Available options: **Single\-metric** and **Multi\-metric**. If you need to monitor multiple metrics of a resource, you can select Multiple\-metrics. |
   ||Trigger condition<br><br> |The trigger condition. When the monitored resource metric reaches the trigger condition, the system will send an alert notification. The following items are included:<br><br><br>* **Condition operator**: When **Metric type** is set to **Multi\-metric**, you can configure the relationship between multiple alert trigger conditions. Available types:<br><br>   * **All**: Multiple alert trigger conditions have a logical **AND** relationship. This means that all conditions must be met simultaneously to trigger an alert.<br><br>   * **Any**: Multiple alert trigger conditions have logical **OR** relationship. This means that meeting any one condition will trigger an alert.<br><br>* **Cycles**: Specify the number of cycles that must meet the alert trigger condition to trigger an alert. For example, you can configure **In 1 cycles (1 cycle = 1 minute)** . You can also specify that N of M cycles meet the condition. For example: **In 3 periods (1 cycle = 1 minute), there are 2 cycles**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the <strong>Metric type</strong> parameter is set to <strong>Single metric</strong>, only one trigger condition can be set. When <strong>Metric type</strong> is set to <strong>Multi\-metric</strong>, you can configure one or more trigger conditions, with a minimum of 1 and a maximum of 10.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can use the same metric to configure multiple trigger conditions. However, for the same alert policy, the quadruple <strong>metric name + statistical cycles + aggregation type + comparison operator</strong> must not be identical.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a rule triggers both a threshold alert and a NoData alert at the same time, two notifications will be sent.</div><br><br><br>* **Metric name**: The alert metric for a cloud service. Supported metrics vary by cloud service. For example, when monitoring an ECS instance, you can select metrics such as CPU usage and CPU idle rate.<br><br>* **Statistical cycle**: The statistical cycle of the alert metric. Valid values: Recent 1 cycles, Recent 2 cycles, Recent 3 cycles, Recent 4 cycles, Recent 5 cycles, etc.<br><br>* **Aggregation method**: The method used to aggregate the alert metric within a statistical cycle. Valid values:<br><br>   * **Average**: The value calculated by averaging the raw values within the statistical cycles.<br><br>   * **Maximum**: The highest value among the raw values within the statistical cycles.<br><br>   * **Minimum**: The lowest value among the raw values within the statistical cycles.<br><br>* **Comparison operator**: As shown in item 6 in the figure above. The comparison operator between the alert metric value and the threshold. Available options include \>, \>=, <, <=, !=, =, Compare to Last Period Increase, Compare to Last Period Decrease, Compare to Last Period Increase or Decrease, Compare to The Same Period of Yesterday Increase, Compare to The Same Period of Yesterday Decrease, Compare to The Same Period of Yesterday Increase or Decrease, Compare to The Same Period of Last Week Increase, Compare to The Same Period of Last Week Decrease, and Compare to The Same Period of Last Week Increase or Decrease.<br><br>* **Alert level**: As shown in item 7 in the figure above. The alert severity level and its corresponding threshold. Different thresholds can be configured for different severity levels. Alert level options include **Critical**, **Warning**, and **Notification**.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For example, when the trigger condition is configured as "Average disk usage \> 60%, 120 cycles (1 cycle = 1 minute)", the system checks the resource metric every 1 minute. An alert is triggered if the average disk usage of a resource exceeds 60% for 120 consecutive minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After you configure trigger conditions, you can click <strong>Preview</strong> or <strong>Alert test</strong> to preview and test alerts based on the trigger conditions.</div><br> |
   ||Mute For<br><br> |After an alert policy is triggered, if the monitored resource continuously triggers alerts, the system will periodically send alert notifications to prevent excessive notifications.<br><br><br>* You can set the alert sending cycle to 5 minutes, 10 minutes, 15 minutes, 30 minutes, 60 minutes, 3 hours, 6 hours, 12 hours, or 24 hours.<br><br>* The default value is 5 minutes. |
   ||Notify mode<br><br> |* **Rule**: If any resource in an alert rule continuously exceeds the alert threshold within a notification cycle, only one alert notification is sent during that cycle.<br><br>* **Rule and Resource**: If different resources in an alert rule continuously exceed the alert thresholds within a notification cycle, an alert notification is sent separately for each resource during that cycle. If the monitored metrics are not recovered after the notification cycle ends, Cloud Monitor sends another alert notification for each resource. |
   ||Alert recovery notification<br><br> |A recovery notification is sent to users after the alert is cleared. The feature is enabled by default.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For threshold alerts, if the resource generates no alert for consecutive 5 minutes, the alert is cleared.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For NoData alerts, if the resource reports data for consecutive 5 minutes, the alert is cleared.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you set "Notification aggregation policy" to <strong>"Rule"</strong>, one alert recovery notification is sent after the alerts for all resources are recovered.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you set "Notification aggregation policy" to <strong>"Rule and Resource"</strong>, one alert recovery notification is sent each time the alerts for a resource are recovered.</div><br> |
   ||NoData alert<br><br> |Configure the NoData alert.<br><br><br>* Configure a trigger condition. If no data is reported for the specified resource for consecutive n cycles, a NoData alert will be triggered.<br><br>* Configure the level of the NoData alert. Valid values: **Critical**, **Warning**, and **Notification**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can configure 3 to 20 cycles. The default value is 10 cycles.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Not all cloud service metrics support NoData alerts. "NoData alert" can be configured only when the following two conditions are met: <strong>"Dimension"</strong> in the "Alert object" section is set to <strong>"Instance"</strong> and the resource involves only one level of cloud service metrics. The actual console display shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a rule triggers both a threshold alert and a NoData alert at the same time, two notifications will be sent.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">NoData alert notifications will not be sent if the corresponding resource is deleted.</div><br><br><br>   <div data-tips="true" data-tips-type="warning">For example, the Resources parameter is set to All in the Alert object section. If Resource A is deleted and no data is reported for consecutive n cycles, no NoData alert will be sent.   </div><br>    |
   |Advanced Settings |Project |Specify the project to which the alert policy belongs. The default project is selected by default.  |
   ||Tags |Click **Add tag** to add tags to the alert policy. |
   |Alert way |Notification policy |Select an appropriate notification policy based on actual circumstances. A notification policy defines the recipients, delivery channels, and content display format for alert notifications when alerts of different levels are triggered or recovered. |
   


<span id="UdXior8a"></span>
## Validate results

After the alert policy is configured, you can view and manage the created alert policy. For specific operations, see [Viewing alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy).

<span id="cc60af67"></span>
## Other configurations

<span id="cc60af67"></span>
### Preview alerts

When you configure an alert policy, you can preview alerts for a trigger condition. You can preview monitoring charts for single and multiple metrics. You can select a specific resource and the chart will display the configured threshold and the time range during which the exceptions of the resource are detected to help you check whether the alert threshold configuration covers the exceptions of the resource.


1. When you configure an alert rule, click **preview** to preview alerts after you specify the **Trigger condition** parameter.

2. Select the target resource and query time period to preview the alerts of the specified resource during the specified time period.

      * You can select up to 10 target resources.

      * A dashed line in a chart indicates a configured metric threshold, as shown by the dashed lines that correspond to 80, 60, and 40 on the Y axis in the following figure.

      * A solid line in a chart indicates the specific value of a resource metric. You can move the pointer over the solid line to view the resource name and metric threshold, as shown by the blue solid line in the following figure.

      * A shadow in a chart indicates that alert information is generated during the corresponding time period, as shown by the blue shadow in the following figure.

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Description      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The alert result displayed in the alert preview image only indicates whether the resource should trigger alerts at specific time points, regardless of the configured duration.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The alert preview curve is not completely synchronized with the metric curve. The value at each time point on the alert curve indicates the result under the alert trigger condition for the metric at the time point.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The shadow in the chart indicates that <strong>at least one resource</strong> meets the threshold condition of the corresponding level at the current time point.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the comparison method of the trigger condition is set to <strong>periodicity\-valued comparison</strong> or <strong>interval\-valued comparison</strong>, the value at each time point in the preview image indicates the periodicity\-valued comparison result or interval\-valued comparison result.      </div>
      


<span id="YrxUQfLL"></span>
### Test alerts

When you configure an alert policy, you can perform an alert test for a trigger condition to verify the current configurations and the execution status of alert metrics within the specified time period. The system will display the resources of different alert states within the specified time period.


1. When you configure an alert rule, click **preview** to preview alerts after you specify the **Trigger condition** parameter.

2. Select a time point and a cycle to view the alert test charts and resources for each cycle within the specified time period, including the number of resources at different alert levels in each alert cycle. Click the alert cycle list, and the system will display the resource list and the corresponding alert levels.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can perform an alert test for up to 15 cycles. You can directly select a cycle including <strong>5 cycles, 10 cycles, and 15 cycles</strong>.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The alert test result only applies to threshold alerts and does not apply to NoData alerts.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can perform an alert test for up to 20 resources.   </div>
   


&nbsp;

&nbsp;
