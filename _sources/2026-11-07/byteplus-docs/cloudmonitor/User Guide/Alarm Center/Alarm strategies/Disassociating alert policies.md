---
title: "Disassociating alert policies"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Unbinding-Alarm-Strategy"
---

You can disassociate alert policies from alert templates based on which the alert policies are generated. After disassociation, you can edit the alert templates to specify new object groups, alert rules, and alert methods based on your business requirements.

<span id="149eef58"></span>
## Prerequisites


* An alert policy has been created. For details, see [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

* An object group has been created. For more details, see [Creating object groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group).


<span id="c1cbf807"></span>
## Procedure

<span id="c1cbf807"></span>
### Step 1: Disassociate the alert policy


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center** \> **Alert Policy**.

3. Find the target alert policy and click **Unbind** in the Actions column.

4. In the message that appears, click **Confirm** to disassociate the alert policy from the corresponding alert template.


<span id="f78ba5e8"></span>
### Step 2: Edit the alert policy


1. Find the target alert policy and click **Edit** in the Actions column.

2. Select the created object group that you want to apply to the alert policy.

3. Reset parameters of the alert policy. For parameter configuration, see [Creating alert policies.](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy)

4. After you check that the information is correct, click **Save** to complete the configuration.
