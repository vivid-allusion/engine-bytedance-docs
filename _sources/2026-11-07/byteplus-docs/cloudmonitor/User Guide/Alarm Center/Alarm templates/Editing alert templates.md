---
title: "Editing alert templates"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-template"
---

You can create a new alert template by editing an existing alert template, which helps you quickly change configurations such as the trigger conditions and the filter conditions of the alert template based on your business requirements.

<span id=".57yW6L6R5bey5YWz6IGU5a-56LGh5YiG57uE55qE5oql6K2m5qih5p2_"></span>
## Edit an alert template associated with an object group


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center** \> **Alert Template**.

3. Find the target alert template in the alert template list, and click **Edit** in the **Actions** column.

4. On the **Edit alert template **  page, modify the configuration and then click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you edit an alert template, take note of the following rules when you add a new resource and rule:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The content and ID of the generated alert policy are not affected.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the new resource type overlaps with that in the object group, a new alert policy will be generated.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you edit an alert template, take note of the following rules when you modify some existing resources and rules:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The content and IDs of the resources and rules that are not modified are not affected.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For modified resources and rules, the ID of the generated alert policy remains unchanged, and the content will be synchronously updated.   </div>
   


<span id=".57yW6L6R5pyq5YWz6IGU5a-56LGh5YiG57uE55qE5oql6K2m5qih5p2_"></span>
## Edit an alert template not associated with an object group


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center** \> **Alert Template**.

3. Find the target alert template in the alert template list, and click **Edit** in the **Actions** column.

4. On the **Edit alert template** page, modify the configurations and click **Confirm**.

   
   |**Parameter** |**Descriptions** |
   |---|---|
   |Name |The template name.<br><br><br>* The name must be 1 to 128 characters in length.<br><br>* The name cannot start with a digit, a hyphen (\-), or other special characters.<br><br>* The name can contain special characters. |
   |Description |The description of the template. |
   |Resource type |Select a cloud service. |
   |Subnamespace |The alert dimension of the cloud service. |
   |Rule name |The name of the alerting rule.<br><br><br>* The name must be 1 to 64 characters in length.<br><br>* The name cannot start with a digit, a hyphen (\-), or other special characters.<br><br>* The name can contain special characters. |
   |Metric type |* Single metric<br><br>* Multiple metrics |
   |Trigger condition |The metric trigger condition.<br><br>A metric triggers an alert if the maximum, minimum, or average value of the metric within a specific period of time meets the filter condition.<br><br><br>* Metric: Metrics vary based on different dimensions of cloud services.<br><br>* Filter conditions: include \>, \>=, <, <=, !=, and =. |
   |Alert level |* Notification<br><br>* Warning<br><br>* Critical |
   |Mute For |The internal at which an alert is sent. |
   

   In the alert template list, you can view the content of the edited alert template.
