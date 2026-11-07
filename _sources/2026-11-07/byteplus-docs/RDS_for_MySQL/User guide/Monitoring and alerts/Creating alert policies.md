---
title: "Creating alert policies"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_alert_policies"
---

RDS for MySQL is integrated with Cloud monitor (VCM) for managing alarm rules through Cloud monitor (VCM).

<span id=".5pON5L2c5q2l6aqk"></span>
## Precautions

When creating an alarm policy with multiple trigger conditions configured, you need to select the logical relationship between conditions (All or Any), which determines how alarms are triggered:


* **All**: Indicates that the system will trigger an alarm only when all configured conditions are satisfied simultaneously.

* **Any**: Indicates that the system will trigger an alarm as long as any one of the configured conditions is satisfied.


<span id="CdoRnn8b"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click on the **Monitoring** tab at the top of the page.

6. Click **Create alarm rule** to open the creating alarm strategy page in Cloud monitor (VCM).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring alarm objects on the creating alarm strategy page, select <strong>RDS for MySQL</strong> as the resource type. For more information, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating alarm strategy</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Resource monitoring, deployment monitoring, and rngine monitoring support creating alarm policies at the Node level, while proxy monitoring supports creating alarm strategies at the instance level. If your instance does not support creating node\-level alarm strategies for resource monitoring, deployment monitoring, and engine monitoring, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to upgrade your instance version.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To simplify the operation process, you can also apply a preset alert template. For Details about the preset alarm templates for RDS for MySQL, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_alarm_templates">List of preset alarm templates</a>. For more information, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-a-preconfigured-alarm-template">Creating alarm strategy</a>.   </div>
   


<span id=".55u45YWz6ZO-5o6l"></span>
## Related links


* [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy)

* [Viewing an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy)

* [Modifying an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Modifying-an-alarm-strategy)

* [Enabling an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-an-alarm-strategy)

* [Disabling an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Disabling-an-alarm-strategy)

* [Deleting an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Deleting-an-alarm-strategy)

* [Viewing alarm history](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history)

* [Creating an alarm Policy](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-a-preconfigured-alarm-template)

* [Alarm callback instructions](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions)

* [Alarm callback linked to Feishu group bot](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups)

* [Alarm callback linked to DingTalk group bot](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups)

* [Alarm callback linked to WeChat work group bot](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups)
