---
title: "Creating an allowlist"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_allowlist_1"
---

This topic describes how to manually add client IP addresses, address segments, or ECS security groups to allowlists to access MySQL instances.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Allowlist is a security prevention and control method for database connections, only IP addresses in the allowlist can access the database. A MySQL instance is not associated with any allowlists after it is created. By default, all Internet protocol addresses are denied access to the instance. Therefore, whether you access the instance through a VPC intranet or the public network, you must configure an allowlist for the instance to ensure it is connectable.

Allowlists support IP address ranges in CIDR format, such as `192.168.0.0/32` (where any integer from 0 to 31 can be entered after the slash), which allows access from any IP address within that network segment.

You can now associate Elastic Computing Services security groups with MySQL allowlists. After associating an ECS security group, you can import the IP addresses of all ECS instances in that security group to the allowlist. This allows all these ECS instances to access the MySQL instance associated with the allowlist.

RDS for MySQL supports setting an allowlist as the default. After an allowlist is set as the default, it is automatically associated when you create a new instance, restore to a new instance, or purchase a new instance.

If you have previously used the session management feature provided by the Database Workshop (DBW) or operated on a MySQL instance using the Database Transmission Service (DTS), the instance will be added to the system built\-in allowlist. System built\-in allowlists cannot be edited, disassociated, or deleted.


* The built\-in allowlist added by DBW for MySQL instances is named `DBW_Sole_Group_Name_For_RDS`.

* The built\-in allowlist added by DTS for MySQL instances is named `dts_internal_for_EndpointVolcMySQL`.


The allowlist needs to be maintained regularly to remove IP addresses that no longer need to access the MySQL instance to ensure the security of database connections.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation


* Each tenant can create up to 500 allowlists for each product in each region.

* Each allowlist can contain up to 300 IP addresses or IP address ranges.

* Each allowlist can be associated with up to 500 instances.

* Each instance can be associated with up to 100 allowlists (including the system's built\-in allowlist).

* Each allowlist can add up to 10 security groups.

* A single instance can support up to 300 IPs or IP segments (the total number of IP addresses or IP address segments from all associated allowlists, including the IP addresses in the system's built\-in allowlist). When there are many IP addresses, it is recommended to merge scattered IP addresses into IP address segments.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Setting `0.0.0.0/0` allows access from all addresses; setting `127.0.0.1` denies access from all addresses. If both `0.0.0.0/0` and `127.0.0.1` are set, access is allowed from all addresses.

* When accessing a MySQL instance across VPCs, add `100.64.0.0/10` to the instance's allowlist.

* If an allowlist is set as the default, it is automatically selected when you create a new instance, restore to a new instance, or buy a same instance, unless you configure it manually. Since each allowlist can be associated with a maximum of 500 instances, you cannot associate more instances after the limit is reached. It is recommended to regularly check the number of instances associated with the default allowlist and update the default allowlist periodically.

* A default allowlist cannot be deleted directly. To delete the allowlist, you must first edit it to a regular allowlist and remove its association with any instances.

* If a security group is updated after being associated with an allowlist, click **Sync Security Group** in the Actions column of the target allowlist to get the updated IP addresses from the security group.

* If a security group is updated after being associated with an allowlist, the updates are automatically synchronized when you edit and submit that allowlist.

* If you create an allowlist and set it as the default, it replaces the previous default allowlist, if any.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. Click **Create allowlist**. After completing the following settings on the Create allowlist page that pops up, click **OK**.



|Parameter |Description |
|---|---|
|Affiliate project |Required. Select the affiliated project for the allowlists from the drop\-down list. By default, allowlists are assigned to the **default**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources. For more details, see <a href="https://docs.byteplus.com/en/docs/6649/94333">Resource management</a>.</div><br> |
|Allowlist name |Required. Naming rules are as follows:<br><br><br>* The name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 1~128 characters. |
|Description |Optional. The description information can be used to search for the allowlist in the allowlist list, and the length of the description should not exceed 200 characters. |
|IP address |Required. Only IP addresses added to the allowlist can access the instance. Support pasting IP addresses or address segments. Separate multiple IP addresses or segments by commas, spaces, or line break (\n). |
|Default allowlist |Select whether to use the default allowlist. You can set a default allowlist for the tenant. This allowlist will be selected by default when you create a MySQL instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An allowlist can associate up to 500 instances. After exceeding the upper limit, please modify the default allowlist.</div><br> |
|Security group |You can associate RDS for MySQL allowlists with an ECS security group. If you adjust the ECS security group after the association, you can synchronize the security group in RDS for PostgreSQL allowlist to get the latest IP list in a timely manner.<br><br>Click **Select security group**, select the security group you want to associate in the **Edit security group** window, and then click **OK**. Support for binding through two modes:<br><br><br>* **Associated ECSIP**: Allows the ECS within the security group to access the database, currently only the IP information import of the main network interface card is supported.<br><br>* **Inbound IP**: Allow IP access to the database involved in the TCP and ALL protocols in the source address of the security group entry direction. If the source address is configured as security group, it will be ignored.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">ECS security groups can be associated in two ways simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When binding a security group using <strong>Inbound IP</strong> mode, an address in the security group is not added to the MySQL allowlist if the policy is Denied.</div><br> |


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

**Do MySQL instances require an allowlist?** 

If a default allowlist is set, the MySQL instance is associated with the default allowlist after it is created. If no default allowlist is set, the instance is not associated with any allowlist after it is created, and the MySQL instance is inaccessible from any IP address.

**How many allowlists can a single instance associate?** 

A single instance can associate up to 100 allowlists.

**How many IP addresses or IP address ranges can an allowlist support?** 

An allowlist can support up to 300 IP addresses or IP address ranges.

**Can an allowlist be associated with multiple instances?** 

Support. An allowlist can be associated with up to 500 instances.

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/6313/145077) |Call the CreateAllowList API to create a new IP allowlist. |
