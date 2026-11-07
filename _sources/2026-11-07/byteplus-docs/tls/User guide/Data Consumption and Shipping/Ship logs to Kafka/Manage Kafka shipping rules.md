---
title: "Manage Kafka shipping rules"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/manage_kafka_shipping_rules"
---

After you create shipping configurations, you can view and manage Kafka shipping configurations in the shipping configuration list, such as modifying shipping configurations, and pausing or resuming log shipping.

<span id="修改投递配置"></span>
## Modify a shipping configuration

After you create a shipping configuration, you can view the basic information about the rule in the list of shipping configurations on the **Kafka shipping** page. You can also click the name of the shipping configuration to view its details, or modify the parameter values of the shipping configuration as needed. Perform the following steps:


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On **Kafka shipping** tab, find the target shipping configuration, then click **Modify** in the **Actions** column.

4. Reconfigure the shipping configuration.

   To configure a shipping configuration, refer to [Ship logs to Message Queue for Kafka](https://docs.byteplus.com/docs/tls/ship_logs_to_message_queue_for_kafka).


<span id="暂停或启动-kafka-投递配置"></span>
## Pause or resume a shipping configuration

After you create a shipping configuration, the rule is enabled by default. Disable the rule as needed. If you pause a rule and resume it, log data collected during the pause period is also shipped to Message Queue for Kafka.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On **Kafka shipping** tab, find the target shipping configuration, then enable or disable the rule in the **Status** column.


<span id="查看日志投递状态"></span>
## View the log shipping status

The execution progress and status of a log shipping task are recorded in service logs. You can view the log data in `tls_shipper-log Topic` of the `tls_service-project` project. The Status field indicates the execution result of each shipping task. The following table describes the field.


|Status |Description |
|---|---|
|Success |The task is executed, and the logs entries are shipped. |
|Failed |The task fails. View the Message field for the failure details. Common causes:<br><br><br>* `Shipper Task is cancelled`: The task fails as the shipping task was canceled.<br><br>* `User is not authorized to action on resource`: The authentication fails. For example, cross\-service access authorization is not configured. Authorize access and try again.<br><br>* `We have an internal error occurred`: Internal error. The system retries automatically. If the error is reported again, contact customer service support for assistance.<br><br><br>For a task that fails, handle the error based on the error message in the Message field. After you handle the error, we recommend that you create a shipping configuration again to ship the remaining data. |


<span id="删除投递配置"></span>
## Delete a shipping configuration

If a shipping configuration is no longer needed, you can promptly disable it to save resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A deleted shipping configuration cannot be restored. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="tip">After you delete a shipping configuration, log shipping stops but data already shipped to the Kafka instance is not affected.</div>



Perform the following steps:


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Data processing** \> **Log shipping**.

3. On **Kafka shipping** tab, find the target shipping configuration, then click **Delect** in the **Actions** column.

4. In the pop\-up dialog box, confirm the details of the shipping configuration you want to delete and click **Delect**.
