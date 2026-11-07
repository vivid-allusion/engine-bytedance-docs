---
title: "Creating allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/create-allowlist"
---

Allowlist is a security measure for database connection. When you create a SQL Server instance, all devices whose IP address belongs are disabled from accessing the instance by default. This article describes how to manually add client side IP addresses or address segments to the allowlist for successful access to a SQL Server instance.

<span id="background-information"></span>
## **Background information**


* Whether accessing an instance through a private network or a public network connection, you need to configure the allowlist of the instance first to ensure that the instance can be connected.

* Please maintain the allowlist regularly to clear the IP addresses of devices that do not require access to SQL Server instances to ensure the security of database connections.


<span id="usage-restrictions"></span>
## usage restrictions


* Each product per tenant can create up to 500 allowlists per region.

* A single instance can bind up to 300 IPs or IP segments through the allowlist.

* Each allowlist can be bound to up to 500 instances.

* Each allowlist can be associated with up to 10 ECS security groups.

* A single instance can bind up to 100 IP allowlists, with each allowlist supporting up to 300 IPs or IP segments. When there are many IP addresses, it is recommended to merge the fragmented IP into IP segments, such as `10.10.10.0/24`.


<span id="precautions"></span>
## **Precautions**


* Setting up the allowlist does not affect the normal operation of your SQL Server instance.

* Support setting a single IP address, such as: `192.168.0.1`, only allow access to that IP address.

* If you set `0.0.0.0/0`, it means that all addresses are allowed to access, and the `0.0.0.0/0` field has higher priority than other network segments.

* Support setting the IP address segment in CIDR format, such as: `192.168.0.0/24`( `/` can be entered after any integer between 0 and 31), allowing IP address access in the network segment.

* If the allowlist is created and specified as the default allowlist, the allowlist replaces the default allowlist (if any).

* If the allowlist is set as the default allowlist, the allowlist cannot be deleted directly. You need to modify it to a normal allowlist by editing the allowlist and unbind it from the instance before deleting it.

* If you set the allowlist as the default allowlist, the default allowlist will be automatically selected when creating new instances and rebuilding instances without manual settings. Since each allowlist can bind up to 500 instances, binding beyond 500 instances is not possible. It is recommended to periodically check the number of instances of default allowlist bindings and update the default allowlist regularly. Restoring to a new instance inherits the allowlist information of the original instance.

* If the security group is updated after being associated with the allowlist, you need to click on the operation column of the target allowlist in the allowlist list to **synchronize security groups** so that the allowlist gets the updated IP of the security group.

* If a security group is updated after being allowlisted, the update of the security group is automatically synchronized when editing the allowlist associated with that security group and submitting it.


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. Click **Allowlist list** in the left navigation bar.

4. Click **Create allowlist**. Add the **Allowlist name**, **Description** and **IP address** to the pop\-up Create allowlist page and click **OK**.



|**Parameters** |**Description** |
|---|---|
|**Allowlist names** |The naming rules are as follows:<br><br><br>* names are unique.<br><br>* Begins with Chinese, a letter, or an underscore (_).<br><br>* can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>* Length is 1 to 128 characters. |
|**Description** |Description Information can be used to search for allowlists in allowlists, and the description content should not exceed 200 characters in length. |
|**IP Address** |Only IP addresses added to the allowlist can access the instance. Support pasting IP addresses or address segments, separated by Chinese and English commas, spaces or newline characters. |
|**Default allowlist** |Select whether to be the default allowlist. You can set a default allowlist in the tenant dimension, which is selected by default when you create an instance of RDS for SQL Server.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Allowlist can bind up to 500 instances. Please modify the default allowlist after exceeding the upper limit.</div><br> |
|**Security groups** |Support for allowlist cloud databases SQL Server editions with ECS security groups. Click **Select security group** and select the mode for binding security groups as needed in the **Modify security group** dialog box. Binding is supported through the following modes:<br><br><br>* **Associated ECSIP**: Allows Cloud as a Service in the security group to access the database, currently only the IP information import of the main network interface card is supported. Check the target security group from the drop\-down list of **Security groups** to support multiple selection.<br><br>* **Inbound IP**: Allows secure group entry direction in the source address of TCP protocol and ALL protocol involved in IP access to the database, if the source address is configured as a security group will be ignored. Check the target security group from the drop\-down list of **Security groups** to support multiple selection.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you adjust the ECS security group after association, you can synchronize the security group in the cloud database SQL Server version allowlist to get the latest IP list in time.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">ECS security groups can be associated in two ways simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist supports the association of up to 10 ECS security groups.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When binding a security group by <strong>Inbound IP</strong>, an address in the security group will not be added to the SQL Server allowlist if the policy is denied.</div><br> |
