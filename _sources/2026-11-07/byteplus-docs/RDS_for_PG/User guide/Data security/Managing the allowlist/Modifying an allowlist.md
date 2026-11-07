---
title: "Modifying an allowlist"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_an_allowlist"
---

This article introduces the operation process of modifying the allowlist.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After modifying the allowlist, the modification will be synchronized to all instances associated to the allowlist.

* If you remove certain IP addresses, those IP addresses will no longer be able to access those database instances associated to the allowlist, so please proceed with caution.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage restrictions


* Each allowlist can contain up to 300 IP addresses or IP address segments.

* The total number of IP addresses or IP address segments in all allowlists associated with each instance cannot exceed 300. When there are many IP addresses, it is recommended to merge scattered IP addresses into IP address segments.

* It is forbidden to add IP addresses in the form `x.x.x.x/0` other than `0.0.0.0/0` to the allowlist.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. Click the **Edit** button in the **Actions** column of the target allowlist to enter the **Modify allowlist information** page.

5. Complete the settings in the **Edit allowlist information** panel and click **OK**.

   
   |Parameters |Note |
   |---|---|
   |Allowlist name |Required The naming convention for allowlist names is as follows:<br><br><br>* Within the current region, the allowlist name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* The name length is limited to 1~128 characters. |
   |Description |Optional. The description information can be used to search for the allowlist in the allowlist list, and the length of the description should not exceed 200 characters. |
   |IP address |Required. Only IP addresses added to the allowlist can access the instance. Supports pasting IP addresses or IP address segments, separated by Chinese and English commas, spaces or newlines. |
   |Default allowlist |Select whether to use the default allowlist. After the tenant dimension is set to the default allowlist, this allowlist is selected by default when creating an instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">An allowlist can associate up to 500 instances. After exceeding the upper limit, please modify the default allowlist.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you specify a allowlist as the default allowlist when creating or editing it, the allowlist will replace the default allowlist (if any).</div><br> |
   |Security group |RDS for PostgreSQL allowlist supports associating ECS security groups. If you adjust the ECS security group after the association, you can synchronize the security group in RDS for PostgreSQL allowlist to get the latest IP list in a timely manner.<br><br>Click **Select security group**, select the security group you want to associate in the **Edit security group** window, and then click **OK**. Support for binding through two modes:<br><br><br>* **Associated ECSIP**: Allows the ECS within the security group to access the database, currently only the IP information import of the main network interface card is supported.<br><br>* **Inbound IP**: Allow IP access to the database involved in the TCP and ALL protocols in the source address of the security group entry direction. If the source address is configured as security group, it will be ignored.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Each allowlist can add up to 10 security groups.</div><br><br><br>* <div data-tips="true" data-tips-type="default">ECS security groups can be associated in two ways simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When binding a security group using <strong>Inbound IP</strong> mode, an address in the security group is not added to the PostgreSQL allowlist if the policy is Denied.</div><br> |
   


&nbsp;

<span id=".55u45YWzIEFQSQ=="></span>
## **Related APIs**


|API |Description |
|---|---|
|[ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/modifyallowlist) |Call the ModifyAllowList API to modify the whitelist. |


&nbsp;

&nbsp;
