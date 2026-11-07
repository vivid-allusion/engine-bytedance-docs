---
title: "Modify allowlist"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_an_allowlist"
---

An allowlist is a security control for database connections. Only IP addresses added to the allowlist can access an RDS for MySQL instance. To ensure the security of database connections, maintain allowlists regularly to remove IP addresses that no longer need to access the database. This topic describes how to edit allowlists and manage the IP addresses they contain.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Allowlist is a security prevention and control method for database connections, only IP addresses in the allowlist can access the database. A MySQL instance is not associated with any allowlists after it is created. By default, all Internet protocol addresses are denied access to the instance. Therefore, whether you access the instance through a VPC intranet or the public network, you must configure an allowlist for the instance to ensure it is connectable.

&nbsp;

Allowlists support IP address ranges in CIDR format, such as `192.168.0.0/32` (where any integer from 0 to 31 can be entered after the slash), which allows access from any IP address within that network segment.

You can now associate Elastic Computing Services security groups with MySQL allowlists. After associating an ECS security group, you can import the IP addresses of all ECS instances in that security group to the allowlist. This allows all these ECS instances to access the MySQL instance associated with the allowlist.

RDS for MySQL supports setting an allowlist as the default. After an allowlist is set as the default, it is automatically associated when you create a new instance, restore to a new instance, or purchase a new instance.

If you have previously used the session management feature provided by the Database Workshop (DBW) or operated on a MySQL instance using the Database Transmission Service (DTS), the instance will be added to the system built\-in allowlist. System built\-in allowlists cannot be edited, disassociated, or deleted.


* The built\-in allowlist added by DBW for MySQL instances is named `DBW_Sole_Group_Name_For_RDS`.

* The built\-in allowlist added by DTS for MySQL instances is named `dts_internal_for_EndpointVolcMySQL`.


The allowlist needs to be maintained regularly to remove IP addresses that no longer need to access the MySQL instance to ensure the security of database connections.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If you remove certain IP addresses, those IP addresses will no longer be able to access those database instances associated to the allowlist, so please proceed with caution.

* Sessions and connections initiated from the removed IP are not actively closed at the server level and can be queried and processed in session management.

* If an ECS security group associated with a MySQL allowlist is updated, you can directly synchronize the updates to the allowlist. For more details, refer to [Synchronizing security group](https://docs.byteplus.com/en/docs/RDS_for_MySQL/sync_security_group).

* If the state of an instance associated with an allowlist is **Running**, modifications to the allowlist are immediately synchronized to the instance. If the state of the instance associated with the allowlist does not meet this condition, the system automatically synchronizes when the condition is met. If immediate synchronization does not occur after the instance state meets the condition, you can also manually [Synchronize the allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/synchronizing_allowlists) on the **Allowlist details** page.

* The RDS for MySQL allowlist feature has been upgraded to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar. It is not recommended to associate instances to the associate of other projects. If you do not have the required privileges for other projects, you cannot edit, delete, or perform other operations on allowlists.

* Sessions and connections initiated from IP addresses removed from an allowlist are not actively closed at the server level, and can be queried and processed in [Session management](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql) or through [Cleaning up non-allowlist IP sessions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Cleaning_up_non-allowlist_IP_sessions).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation


* Each allowlist can contain up to 300 IPs or IP segments. When you have many IP addresses, it is recommended to consolidate them into IP address ranges.

* Each allowlist can add up to 10 security groups.

* If you set an allowlist as the default when modifying it, it replaces the current default allowlist (if any).


<span id="PnVkjZTP"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. Click the **Edit** button in the **Actions** column of the target allowlist to enter the **Modify allowlist information** page.

5. After modifying the **name**, **description**, **Internet protocol address**, the setting for **default allowlist**, and the **security group** information, click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Allowlist name |Required. Naming rules are as follows:<br><br><br>* The name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 1\-128 characters. |
   |Description |Optional. The description information can be used to search for the allowlist in the allowlist list, and the length of the description should not exceed 200 characters. |
   |IP address |Required. Only IP addresses added to the allowlist can access the instance. Support pasting IP addresses or address segments. Separate multiple IP addresses or segments by commas, spaces, or line break (\n). |
   |Default allowlist |Select whether to use the default allowlist. You can set a default allowlist for the tenant. This allowlist will be selected by default when you create a MySQL instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An allowlist can associate up to 500 instances. After exceeding the upper limit, please modify the default allowlist.</div><br> |
   |Security group |You can associate RDS for MySQL allowlists with an ECS security group. If you adjust the ECS security group after the association, you can synchronize the security group in RDS for PostgreSQL allowlist to get the latest IP list in a timely manner. Click **Select security group**, and in the **Edit security group** window, select the security group to associate. Support for binding through two modes:<br><br><br>* **Associated ECSIP**: Allows the ECS within the security group to access the database, currently only the IP information import of the main network interface card is supported.<br><br>* **Inbound IP**: Allow IP access to the database involved in the TCP and ALL protocols in the source address of the security group entry direction. If the source address is configured as security group, it will be ignored.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">ECS security groups can be associated in two ways simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When binding a security group using <strong>Inbound IP</strong> mode, an address in the security group is not added to the MySQL allowlist if the policy is Denied.</div><br> |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you click <strong>OK</strong>, the system checks for updates to the security group associated with the allowlist. If updates are found, a dialog box appears with the message <strong>Updates detected in the associated security group. Do you want to synchronize?</strong>, which lists the IP changes in the security group. Select <strong>Synchronization</strong> or <strong>Do not synchronize</strong> as needed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Synchronization: The system automatically identifies IP changes in the associated security group and updates the allowlist.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Do not synchronize: The system ignores these IP changes and retains the original IPs from the security group in the allowlist.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyallowlist1) |Call the ModifyAllowList API to modify the settings of a target allowlist, such as the allowlist name and IP addresses. |
