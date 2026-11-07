---
title: "Suppressing alerts"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Alarm_silence"
---

Frequent, low\-severity alerts triggered by cloud resource instances or alert policies can bury more important notifications, making it hard to spot critical issues. You can use alert suppression to block this noise so you can focus on what really matters.

<span id="a64812a5"></span>
## Limits


* If **Suppression resource** is set to **All resources**, no limit applies to the match rule quantity.

* If **Suppression resource** is set to **Partial resources**, up to 10 match rules can be configured per suppression policy.

* Each root user can have up to 1000 suppression policies at the same time.


<span id="2a8d8c2e"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification** \> **Suppression policy**.

3. On the **Suppression policy** page, click **Create suppression policy**.

4. On the **Create suppression policy** page, configure the suppression policy details.

   * **Basic information**

   
   |Parameter |Descriptions |
   |---|---|
   |Name |Specify a custom suppression policy name to identify this suppression policy.<br><br><br>* The name can contain special characters.<br><br>* The name cannot start with a digit, a hyphen (\-), or other special characters.<br><br>* The name must be 1 to 128 characters in length. |
   |Description |Provide a description of the suppression policy. |
   

   * **Silence strategy**

    &nbsp;

   
   |Parameter |Descriptions |
   |---|---|
   |Suppression type |Select **Alert policy** or **Event rule**. In this scenario, select **Alert policy**. |
   |resource type |Select the cloud product for which you want to suppress alerts. |
   |Alerting strategy |Select the alert policy to be suppressed.<br><br><br>* If you specify an alert policy and select **All resources** for **Suppressed resource**, alert notifications generated for resources under the specified alert policy will be suppressed.<br><br>* If you specify no alert policy and select **All resources** for **Suppressed resource**, alert notifications generated for all resources of the specified resource type will be suppressed. |
   |Suppressed resource |Select the scope of resources for which you want to suppress alerts. You can select **All resources** or **Partial resources** to suppress alerts at the level of monitored resources.<br><br><br>* If you select **Partial resources**, you can configure the relationship between match rules, including:<br><br>   * **Anyone is met**: Individual rules have a logical **OR** relationship. Any match rule satisfied will trigger this suppression policy.<br><br>   * **All are met**: Individual match rules have a logical **AND** relationship. All the specified rules must be satisfied to trigger this suppression policy.<br><br>* If you select **Partial resources**, resources can be matched based on tags of cloud resources.<br><br>   * Supported resource tags include **ResourceID**, **ResourceName**, **ResourceProject**, **Tag**, and more. Supported tags may vary with cloud products. You can query the supported tags for a specific cloud product in the console.<br><br>   * Supported matching methods include **Prefix matches**, **Suffix matches**, **Contain**, **Not contain**, **Equal to**, and **Not equal to**.<br><br>   * You can specify multiple tag values. After you enter a tag value, press Enter to confirm it. You can enter up to 50 tag values, with each tag value not exceeding 128 characters in length. |
   

   * **Suppression time**

   
   |Parameter |Descriptions |
   |---|---|
   |Effective time |You can specify one of the following suppression time options:<br><br><br>* **Suppress permanently**: No specific suppression time is required. As long as the suppression policy is effective, suppression is enabled. To disable suppression, stop the corresponding suppression policy.<br><br>* **Suppression at absolute time**: The suppression policy applies within the specified, fixed period of time.<br><br>* **Suppression at relative time**: The suppression applies periodically within the specified cycle. |
   |Time range |If you select **Suppression at absolute time** for **Effective period**, configure the **Time range** for suppression.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can specify up to three time ranges.</div><br><br><br>Available options include 3 hours, 6 hours, One day, This week, Next week, and Custom. If you select **Custom**, specify a **Start date** and **End date**. |
   |Cyclic time type |If you select **Suppression at relative time** for **Effective period**, you also need to configure **Cyclic time type** for suppression. You can select **Cycle permanently** or **Cycle in specified days**.<br><br><br>* If you select **Cycle permanently**, specify the start time and end time for suppression.<br><br>* If you specify **Cycle in specified days**, specify a time range, suppression start time, and suppression end time.<br><br>   The time range options include This week, Next week, and Custom. If you select **Custom**, specify a **Start date** and **End date**. |
   

5. Click **Submit** to complete the configuration.


<span id="o6yiU6YA"></span>
## Verifying results

After configuring an alert suppression policy, you will not receive alerts for the corresponding resources during the specified suppression time. You can view suppressed alerts under the suppression policy on the **Suppression history** tab of the suppression policy details.

Meanwhile, you can still view alert logs on the **Alert history** page. To view details of suppressed alerts, find the target alert log and click **Details** in the **Actions** column.

&nbsp;

&nbsp;

&nbsp;

&nbsp;
