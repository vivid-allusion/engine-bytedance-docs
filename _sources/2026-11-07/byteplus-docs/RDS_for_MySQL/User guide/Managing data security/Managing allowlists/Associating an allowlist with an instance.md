---
title: "Associating an allowlist with an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances"
---

Support pasting IP addresses or address segments. Separate multiple IP addresses or segments by commas, spaces, or line break (\n). Since allowlists and instances have a many\-to\-many relationship, you can either associate an instance to an allowlist or associate an allowlist to an instance. This topic describes how to associate an allowlist with an instance.

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

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation


* Each allowlist can contain up to 300 IPs or IP segments.

* Each allowlist can be associated with up to 500 instances.

* Each instance can be associated with up to 100 allowlists (including the system's built\-in allowlist).

* A single instance can support up to 300 IPs or IP segments (the total number of IP addresses or IP address segments from all associated allowlists, including the IP addresses in the system's built\-in allowlist). When you have many IP addresses, it is recommended to consolidate them into IP address ranges.

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. Select the region for the allowlist in the upper\-left corner of the top menu bar.

3. Click **Instances** in the left\-side navigation bar.

4. RDS for MySQL provides two ways to associate allowlists with an instance:

   * On the **Instances** page, click  **...**  \> **Configure allowlist** in the **Actions** column of the target instance to go to the **Security** tab.

   * On the **Instances** page, click the target instance name, and then click **Security** to go to the **Security** tab.

5. On the **Data Security** tab, under the **Allowlists** subtab, click **Associate with an allowlist** to enter the **Associate with an allowlist** page. On this page, you can associate with an allowlist by choosing either **Existing allowlist** or **New allowlist**. The rules for each are as follows:

   * **Associate an existing allowlist**

      1. On the **Associate with an allowlist** page, click **Existing allowlist** to go to the **Existing allowlist** list.

      2. On the **Existing allowlist** list, select the allowlist to associate with the current instance, and then click **OK**. The successfully associated allowlist appears in the **Associated allowlists list**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can associate up to 100 allowlists with one instance each time.      </div>
      

   * **Associate a new allowlist**

      1. On the **Associate with an allowlist** page, click **New allowlist** to enter the **create an allowlist** page.

      2. On the **Create allowlist** page, complete the following settings and click **OK**.

      
      |Parameter |Description |
      |---|---|
      |Allowlist name |Required. Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* Begin with a Chinese character, letter, or underscore.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 1~128 characters. |
      |Description |Optional The description information can be used to search for the allowlist in the allowlist list, and the length of the description should not exceed 200 characters. |
      |IP address |Required. Only IP addresses added to the allowlist can access the instance. Support pasting IP addresses or address segments. Separate multiple IP addresses or segments by commas, spaces, or line break (\n). |
      |Default allowlist |Select whether to use the default allowlist. You can set a default allowlist for the tenant. This allowlist will be selected by default when you create a MySQL instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An allowlist can associate up to 500 instances. After exceeding the upper limit, please modify the default allowlist.</div><br> |
      |Security group |You can associate RDS for MySQL allowlists with an ECS security group. If you adjust the ECS security group after the association, you can synchronize the security group in RDS for PostgreSQL allowlist to get the latest IP list in a timely manner.<br><br>Click **Select security group**, select the security group you want to associate in the **Edit security group** window, and then click **OK**. Support for binding through two modes:<br><br><br>* **Associated ECSIP**: Allows the ECS within the security group to access the database, currently only the IP information import of the main network interface card is supported.<br><br>* **Inbound IP**: Allow IP access to the database involved in the TCP and ALL protocols in the source address of the security group entry direction. If the source address is configured as security group, it will be ignored.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">ECS security groups can be associated in two ways simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When binding a security group using <strong>Inbound IP</strong> mode, an address in the security group is not added to the MySQL allowlist if the policy is Denied.</div><br> |
      


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[AssociateAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associateallowlist1) |Call the AssociateAllowList API to associate the target instance with the specified IP address allowlist. |
