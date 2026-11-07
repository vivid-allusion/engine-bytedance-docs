---
title: "Delete a host group"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Deleting_a_host_group"
---

This topic describes how to delete a host group.

<span id="注意事项"></span>
## Precautions


* After you delete a host group, LogCollector running on each host in the host group stops collecting and reporting log data.

* If a collection rule is associated with multiple host groups, the other host groups continue to collect log data based on the rule after one of the host groups is deleted.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Host group**.

3. On the **Host group** **management** page, find the target host group, then click **Delete** in the **Actions** column.

4. Confirm the information about the host group, then click **OK**.
