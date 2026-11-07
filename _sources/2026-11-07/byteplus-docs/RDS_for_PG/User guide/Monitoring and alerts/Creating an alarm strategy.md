---
title: "Creating an alarm strategy"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/creating_alert_policies"
---

RDS for PostgreSQL is integrated with Cloud Monitor to better manage alerting rules.

<span id="fM8yxGpW"></span>
## Precautions

When creating an alarm policy with multiple trigger conditions configured, you need to select the logical relationship between conditions (All or Any), which determines how alarms are triggered:


* **All**: Indicates that the system will trigger an alarm only when all configured conditions are satisfied simultaneously.

* **Any**: Indicates that the system will trigger an alarm as long as any one of the configured conditions is satisfied.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. Click on the **Monitoring** tab at the top of the page.

5. Click **Create an alert strategy** to open the ** Create alarm strategy** page of Cloud Monitor.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring alert objects on the <strong>Create alarm strategy</strong> page, you are required to select <strong>RDS for PostgreSQL</strong> as the resource type.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deployment monitoring and proxy monitoring support instance\-based alarm strategies, while resource monitoring and engine monitoring support node\-based alarm strategies. When creating an alarm policy based on node dimensions, only the primary node and read\-only node of the instance are supported for selection. When the primary node is selected, if the instance switches between primary and secondary nodes, the alarm policy will be automatically applied to the new primary node.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To simplify the operation process, you can also apply a preset alert template. For more information about the preset alarm templates for RDS for PostgreSQL, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_alarm_templates">List of preset alarm templates</a>. For detailed information about enabling preset alert template, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-a-preconfigured-alarm-template">Enabling a preset alert template</a>.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e3e3f7569c92eb316a9a307bf3c3c670.png" />   </div>
   


<span id=".55u45YWz6ZO-5o6l"></span>
## Related links


* [Viewing an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy)

* [Modifying an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Modifying-an-alarm-strategy)

* [Enabling an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-an-alarm-strategy)

* [Disabling an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Disabling-an-alarm-strategy)

* [Deleting an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Deleting-an-alarm-strategy)

* [Viewing alarm history](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history)

* [Alarm callback instructions](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions)

* [Alarm callback linked to Feishu group bot](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups)

* [Alarm callback linked to DingTalk group bot](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups)

* [Alarm callback linked to WeChat work group bot](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups)
