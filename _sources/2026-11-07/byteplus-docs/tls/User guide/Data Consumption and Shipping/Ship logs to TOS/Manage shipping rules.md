---
title: "Manage shipping rules"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/manage_shipping_rules_tos"
---

This topic describes how to manage shipping configurations, such as modifying shipping configurations, and pausing or resuming log shipping.

<span id=".5L-u5pS55oqV6YCS6YWN572u"></span>
## Modify a shipping configuration

After you create a shipping configuration, you can modify the parameter values of the shipping configuration as needed. Perform the following steps:


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On **TOS shipping** tab, find the target shipping configuration, then click **Modify configuration** in the **Actions** column.

4. Reconfigure the shipping configuration.

   For more information on different formats for shipping configurations, refer to:

   * [Ship log data in JSON format](https://docs.byteplus.com/docs/tls/ship_log_in_json_format)

   * [Ship log data in CSV format](https://docs.byteplus.com/docs/tls/ship_log_in_csv_format)

5. Click **Submit**.


<span id=".5pqC5YGc5oiW5ZCv5Yqo5oqV6YCS6YWN572u"></span>
## Pause or resume a shipping configuration

After you create a shipping configuration, the rule is enabled by default. Disable the rule as needed. If you pause a rule and resume it, log data collected during the pause period is also shipped to TOS.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On **TOS shipping** tab, find the target shipping configuration, then enable or disable the rule in the **Status** column.


<span id=".5p-l55yL5oqV6YCS6YWN572u5ZKM5Lu75Yqh6K-m5oOF"></span>
## View the details of shipping configurations and tasks

After you create a shipping configuration, you can view the basic information about the rule in the list of shipping configurations on the **Log shipping** page. You can also click the name of the shipping configuration to view its details and all shipping tasks triggered within the last 3 days on the **TOS Shipping** page and the **Shipping configuration details** page, respectively.

On the **Shipping configuration details** page, you can select a time period to retrieve shipping tasks, and view the time period, start time, and end time of shipping tasks that meet the filtering conditions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only shipping tasks triggered within the last 3 days can be viewed.</div>



|Parameters displayed |Description |
|---|---|
|Time period during which log data is shipped to TLS |The time when the log data corresponding to the shipping task is collected to TLS. |
|Start time of a shipping task |The time when a shipping task starts. |
|End time of a shipping task |The time when a shipping task ends. |
|Status of a shipping task |The status of a shipping task.<br><br>For more information on the status, refer to the following table. |


After you enable a shipping configuration, TLS executes shipping tasks based on the shipping configuration. The following table describes the status details:


|Status |Description |
|---|---|
|Success |The shipping task is executed. |
|Fail |The shipping task fails. Possible causes:<br><br><br>* TOS authentication fails. For example, cross\-service access authorization is not configured. Authorize access and try again. For more information,refer to [Authorize cross-service access](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).<br><br>* The specified TOS bucket does not exist. Create a bucket or modify the shipping rule, then try again.<br><br>* Internal error. |


<span id=".6YeN6K-V5aSx6LSl5Lu75Yqh"></span>
## Retry a failed task

If a task fails, handle the error based on the error message. After you handle the error, try the task again. Otherwise, the log data corresponding to the task cannot be shipped to TOS.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On **TOS shipping** tab, find the target shipping configuration, then click its name.

4. In shipping task details, find the task whose **Status** is **Fail**, then click **Retry** in the **Actions** column.


<span id=".5Yig6Zmk5oqV6YCS6YWN572u"></span>
## Delete a shipping configuration

If a shipping configuration is no longer needed, you can promptly disable it to save resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A deleted shipping configuration cannot be restored. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="tip">After you delete a shipping configuration, log shipping stops but data already shipped to TOS is not affected.</div>



Perform the following steps:


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On **TOS shipping** tab, find the target shipping configuration, then click **Delete** in the **Actions** column.

4. In the pop\-up dialog box, confirm the details of the shipping configuration you want to delete and click **Delete**.
