---
title: "Managing event rules"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule"
---

You can manage the status of existing event rules in the Cloud Monitor console or delete event rules that you no longer need.

<span id=".5L-u5pS56KeE5YiZ54q25oCB"></span>
## Modify rule status


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Event Center \> Event Rule**.

3. Select one or more target rules in the event rule list, and then perform one of the following operations:

   * **Enable**: You can enable rules that are in the **Disabled** state. The enabled rules will continue to monitor and deliver cloud service events according to the specified effective period, delivery channel, and other conditions.

   * **Disable**: You can disable rules that are in the **Enabled** state. The disabled rules will no longer take effect and will not deliver cloud service events.

   * **Delete**: If you no longer use an event rule, you can delete the rule.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A rule cannot be restored after being deleted. Proceed with caution.   </div>
   

<span id=".57yW6L6R6KeE5YiZ"></span>
## Edit an event rule


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Event Center \> Event Rule**.

3. Click **Edit rules** in the **Actions** column that corresponds to the target event rule.

4. On the **Edit event rule** page, modify the **basic information**, **event rule**, and **delivery method** of the rule.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot modify the <strong>Resource type</strong> parameter in the <strong>Event Rule</strong> section.   </div>
   

5. Click **OK**.
