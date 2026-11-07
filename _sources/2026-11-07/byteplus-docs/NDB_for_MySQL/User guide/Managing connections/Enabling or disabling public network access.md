---
title: "Enabling or disabling public network access"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Enabling_or_disabling_public_network_access"
---

You can enable public network access for the NDB for MySQL instance on the console so that devices outside the VPC can access the NDB for MySQL instance. This topic describes how to enable or disable public network access.

<span id="背景信息"></span>
## Background

The public network access function is disabled by default. If you need to access the instance through the public network, you need to manually enable the public network access function and bind the public network IP to the connection endpoint.

<span id="前提条件"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id="费用说明"></span>
## Fee description

A public address is associated with an Elastic IP Address (EIP). Using an EIP incurs charges at EIP billing rates. For more information about public IP address billing, refer to [Billing overview](https://www.byteplus.com/en/docs/eip/Billing-overview).

<span id="注意事项"></span>
## Precautions


* Instances created before May 17, 2022 do not support binding to EIP when the public network access function is enabled. If you need to bind an EIP, please [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

* Public network connections have certain security risks. When devices outside the VPC no longer need to access the instance, it is recommended that you disable the public network access function in a timely manner.

* After disabling public network access, clients will no longer be able to access the instance through the original public domain name and port. Please make sure that your business does not use public network addresses to avoid unnecessary losses.

* After the public network access is disabled, the public network address will be deleted and the EIP will be automatically unbound. The untied EIP will continue to be retained and charged. If it is no longer used, please release the relevant resources by yourself.


<span id="开启公网访问"></span>
## Enable public network access


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. On the **Summary** page, click the **Connectivity** tab.

5. On the **Connectivity** tab, click **Edit** in the destination endpoint area.

6. In the **Connection information** area of the **Modify endpoint** sidebar, click **Enable public network access**.

7. On the **Enable public network access** page, select EIP.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have not applied for any public IP, click <strong>Apply for EIP</strong> above the list. For more detailed information about applying for an EIP, refer to <a href="https://www.byteplus.com/en/docs/eip/Applying-for-an-EIP">Applying for an EIP</a>.   </div>
   

8. Click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After successfully binding the EIP, you can access the instance through the public network address. For more information about connecting instances over the public network, see <a href="https://www.byteplus.com/en/docs/NDB_for_MySQL/Connecting_to_an_instance_1">Connecting to an instance</a>.   </div>
   

<span id="关闭公网访问"></span>
## Disable public network access


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. On the **Summary** page, click the **Connectivity** tab.

5. On the **Connectivity** tab, click **Edit** in the destination endpoint area.

6. In the **Connection information** area of the **Modify endpoin**t sidebar, click **Disable public network access**.

7. In the pop\-up dialog box, confirm the public network address and elastic public network IP to be untied, and click **Close**.


<span id="相关-api"></span>
## Related APIs


|API |Description |
|---|---|
|[CreateDBEndpointPublicAddress](https://www.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpointPublicAddress) |Call the CreateDBEndpointPublicAddress to enable public network access for instance. |
|[DeleteDBEndpointPublicAddress](https://www.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBEndpointPublicAddress) |Call the DeleteDBEndpointPublicAddress to disable the public network access function. |
