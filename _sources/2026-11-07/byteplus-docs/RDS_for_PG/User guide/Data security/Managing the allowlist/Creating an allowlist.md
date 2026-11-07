---
title: "Creating an allowlist"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist"
---

This topic describes how to manually add the client IP address or IP address range to the allowlist to successfully access the PostgreSQL instance.

<span id="uRzpu1SN"></span>
## Background information


* Allowlist is a security prevention and control method for database connections, only IP addresses in the allowlist can access the database. After a PostgreSQL instance is created, it will not be associated with any allowlist, and all IP addresses are prohibited from accessing the instance by default. Therefore, whether you access the instance through a private network or a public network connection, you need to configure an allowlist for the instance to ensure that the instance can be connected.

* The allowlist supports setting IP address segments in CIDR format, such as: `192.168.0.0/24` (any integer between 1 and 32 can be entered after (/)), allowing access by IP addresses in this network segment.

* The allowlist needs to be maintained regularly to remove IP addresses that are no longer needed to access the PostgreSQL instance to ensure the security of database connections.


<span id="AxNPDMQF"></span>
## Precautions


* If `0.0.0.0/0` is set, the instance will allow access from all addresses. If `127.0.0.1` is set, access from all addresses will be disabled. If both `0.0.0.0/0` and `127.0.0.1` are set, access is allowed from all addresses.


<span id="syQ0RS5Z"></span>
## Usage restrictions


* Each tenant can create up to 500 allowlists for PostgreSQL under each region.

* Each allowlist can contain up to 300 IP addresses or IP address ranges.

* Each allowlist can be associated with up to 1,000 instances.

* Each instance can associate up to 100 allowlists.

* The total number of IP addresses or IP address segments in all allowlists associated to each instance cannot exceed 300. When there are many IP addresses, it is recommended to merge scattered IP addresses into IP address segments.

* It is forbidden to add IP addresses in the form `x.x.x.x/0` other than `0.0.0.0/0` to the allowlist.


<span id="AVonyRtw"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar, click **Create allowlis**t to enter the **Create allowlist** page.

4. After completing the following settings on the Create allowlist page that pops up, click **OK**.

   
   |Parameters |Note |
   |---|---|
   |Allowlist name |Required The naming convention for allowlist names is as follows:<br><br><br>* Within the current region, the allowlist name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* The name length is limited to 1~128 characters. |
   |Description |Optional The description information can be used to search for the allowlist in the allowlist list, and the length of the description should not exceed 200 characters. |
   |IP address |Required. Only IP addresses added to the allowlist can access the instance. Supports pasting IP addresses or IP address segments, separated by Chinese and English commas, spaces or newlines. |
   |Default allowlist |Select whether to configure this allowlist as default allowlist. After the tenant dimension is set to the default allowlist, this allowlist is selected by default when creating an instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">An allowlist can associate up to 500 instances. After exceeding the upper limit, please modify the default allowlist.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you specify an allowlist as the default allowlist when creating or editing it, the allowlist will replace the default allowlist (if any).</div><br> |
   |Security group |RDS for PostgreSQL allowlist supports associating ECS security groups. If you adjust the ECS security group after the association, you can synchronize the security group in RDS for PostgreSQL allowlist to get the latest IP list in a timely manner.<br><br>Click **Select security group**, select the security group you want to associate in the **Edit security group** window, and then click **OK**. Support for binding through two modes:<br><br><br>* **Associated ECSIP**: Allows the ECS within the security group to access the database, currently only the IP information import of the main network interface card is supported.<br><br>* **Inbound IP**: Allow IP access to the database involved in the TCP and ALL protocols in the source address of the security group entry direction. If the source address is configured as security group, it will be ignored.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Each allowlist can add up to 10 security groups.</div><br><br><br>* <div data-tips="true" data-tips-type="default">ECS security groups can be associated in two ways simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When binding a security group using <strong>Inbound IP</strong> mode, an address in the security group is not added to the PostgreSQL allowlist if the policy is Denied.</div><br> |
   


<span id="vCyspkTp"></span>
## Related APIs


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/createallowlist) |Call the CreateAllowList API to create an allowlist. |
