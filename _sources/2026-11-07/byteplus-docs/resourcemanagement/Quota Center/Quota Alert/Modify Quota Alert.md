---
title: "Modify Quota Alert"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Modify_Quota_Alert"
---

You can modify the quota alert as needed.

<span id="procedure"></span>
# Procedure


1. Log in to [Quota center](https://console.byteplus.com/quota/productList).

2. Go to Alert strategy.

3. Select the alert item and click Edit in the Actions column to enter the Edit alert strategy page.

4. Set the relevant parameters as described below.



|**Parameter** |**Description** |
|---|---|
|Alert name |The name of the quota alert. |
|Alert type |* Usage alert: The alert on quota usage.<br><br>* Remaining quota alert(Balance alert): The alert on the remaining available quota. |
|Alert threshold |* Numeric value: The specific preset value for quota alerts, which should be within the range.<br><br>   * For usage alerts, if the quota usage is greater than the preset value, you will receive an alert notification.<br><br>   * For remaining quota alerts, if the remaining available quota is less than the preset value, you will receive an alert notification.<br><br>* Percentage: The specific preset percentage of quota alerts, which should be within the range.<br><br>   * For usage alerts, if the quota usage is greater than the preset percentage, you will receive an alert notification. Percentage range: (30%, 100%]<br><br>   * For remaining quota alerts, if the remaining available quota is less than the preset percentage, you will receive an alert notification. Percentage range: [0%, 70%).<br><br>> If the alert threshold you configure is less than the current usage, an alert will only be triggered in the case of a usage change. |
|Notification type |By default, alerts are sent through private messages, emails, and SMS messages. You can also go to [Message center](https://console.byteplus.com/user/message) to customize the recipients or other receiving methods such as Feishu. The message type option needs to be set to Quota center alert reminder.<br><br>> The current alert silence period is 1 hour by default, and up to 40 messages can be received through each alert method at the same time. Up to 70 messages can be received a day. |



5. Click Submit.
