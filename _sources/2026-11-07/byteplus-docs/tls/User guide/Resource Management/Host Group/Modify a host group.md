---
title: "Modify a host group"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Modify_a_host_group"
---

You can modify the settings of existing host groups at any time based on your business requirements, such as adjusting the number of hosts in a host group. If you want to add or remove servers, you must add hosts to or delete hosts from the corresponding host group.

<span id="注意事项"></span>
## Precautions


* After modifying the settings of a host group, wait for 2 minutes before checking the heartbeat status of the host group.

* After a host is deleted from a host group, LogCollector running on the deleted host stops collecting logs.


<span id="修改机器组配置"></span>
## Modify the settings of a host group

You can modify the basic settings of an existing host group as needed. For example, change the name or type of the host group. Perform the following steps:


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Host group**.

3. On the **Host group** **management** page, find the target host group, then click **Edit** in the **Actions** column.

4. Modify the settings of the host group.

   For more information about the parameters, see [Create an IP address-based host group](https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group) or [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group).

5. Click **OK**.


<span id="解绑机器组"></span>
## Disassociate a host group from a collection rule

After you create a host group and associate it with a collection rule, you can disassociate it from the collection rule if you do not need to collect log data from the servers in the host group.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Host group**.

3. On the **Host group** **management** page, click the name of the host group.

4. On the **Associated collection configuration** tab, find the collection rule with which the host group is associated, then click **Unbind host group** in the **Actions** column.

5. In the dialog box, click **OK**.
