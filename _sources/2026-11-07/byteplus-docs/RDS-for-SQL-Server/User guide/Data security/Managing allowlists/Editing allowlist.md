---
title: "Editing allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/editing-allowlist"
---

Allowlist is a security measure for database connections. Only IP addresses added to the allowlist can successfully access SQL Server instances. To ensure the security of database connections, the allowlist needs to be maintained periodically to remove IP addresses that no longer need to access the database. This article describes how to edit allowlist to manage allowlist and IP addresses in allowlist.

<span id="background-information"></span>
## Background information


* Allowlist is a security measure for database connection, and only IP addresses in the allowlist can access the database. After a SQL Server instance is created, it is not bound to any allowlist, and all IP addresses are prohibited from accessing the instance by default. Therefore, whether you access an instance through a private network or a public network connection, you need to configure the allowlist of the instance first to ensure that the instance can be connected. The allowlist supports setting the IP address segment in CIDR format, such as: `192.168.0.0/32`((/) can be followed by any integer between 0 and 31), allowing IP address access in the network segment.

* SQL Server allowlists already support associating ECS security groups and binding ECS security groups for SQL Server allowlists. After binding the ECS security group, you can import the IP addresses of all ECS instances under the corresponding ECS security group into the allowlist, so that all ECS instances under these ECS security groups can access the SQL Server instances bound to the allowlist.

* RDS for SQL Server supports setting the allowlist as the default allowlist. When the default allowlist is set, the default allowlist is automatically bound when creating a new instance, restoring to a new instance, and purchasing a new instance.

* If you have previously used the session management features provided by the Database Workbench (DBW), or have used the Database Transport Service (DTS) to operate on a SQL Server instance, the instance is added to the system's built\-in allowlist. The system's built\-in allowlist does not support editing, unbinding, or deleting.

* The built\-in allowlist that DBW adds for SQL Server instances is named `DBW_Sole_Group_Name_For_mssql`.

* The built\-in allowlist that DTS adds to SQL Server instances is named `dts_internal_for_EndpointVolcMSSQL`.

* allowlists require regular maintenance to remove IP addresses that no longer require access to SQL Server instances to ensure the security of database connections.


<span id="precautions"></span>
## Precautions


* If you remove certain IP addresses, it means that those IP addresses will no longer be able to access the database instances that are bound to the allowlist. Please proceed with caution.

* Sessions and connections initiated from the removed IP are not actively closed at the server level and can be queried and processed in session management.

* If there is an update to the ECS security group bound to the SQL Server allowlist, you can directly synchronize the update to the allowlist. For more information, see [Synchronizing security groups](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/synchronizing-security-group).


<span id="usage-restrictions"></span>
## usage restrictions


* A single instance can bind up to 300 IPs or IP segments through the allowlist.

* Each allowlist can be bound to up to 500 instances.

* Each allowlist can be associated with up to 10 ECS security groups.

* A single instance can bind up to 100 IP allowlists, with each allowlist supporting up to 300 IPs or IP segments. When there are many IP addresses, it is recommended to merge the fragmented IP into IP segments, such as `10.10.10.0/24`.

* If you modify the allowlist by specifying it as the default allowlist, it will replace the default allowlist (if any).


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. Click **Allowlist list** in the left navigation bar.

4. On the **Allowlist list** page, click Edit of the target allowlist action column.

5. In the **Edit allowlist Information** Control Panel, set the allowlist information as needed, and the specific parameter configuration is shown in the following table.



|**parameter** |**explain** |
|---|---|
|**Allowlist name** |Modify the name of the allowlist as needed. The naming convention is as follows:<br><br><br>* The name is unique.<br><br>* Start with Chinese, letter or underscore (_).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>   The length is 1 to 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also directly on the <strong>Allowlist list</strong> page, place the mouse over the target allowlist name, click the edit icon next to the name, enter a new allowlist name in the pop\-up text box and click OK to modify the name of the allowlist.</div><br> |
|**Describe** |Modify the description of the allowlist as needed. This information can be used to search the allowlist in the allowlist list. The length of the description content should not exceed 200 characters. |
|**IP address** |Modify the IP address of the access instance as needed. Support pasting IP addresses or address segments, separated by Chinese and English commas, spaces or newline characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Support setting the IP address segment in CIDR format, such as: <code>192.168.0.0/24</code>( <code>/</code> can be entered after any integer between 0 and 31), allowing IP address access in this network segment.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Support setting a single IP address, such as: <code>192.168.0.1</code> only allow access to that IP address.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If <code>0.0.0.0/0</code> is set, it means that all addresses are allowed to access, and the <code>0.0.0.0/0</code> field has higher priority than other network segments.</div><br> |
|**Default allowlist** |Select whether to use the default allowlist. You can set a default allowlist in the tenant dimension, which is selected by default when you create an instance of RDS for SQL Server.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Allowlist can bind up to 500 instances. After exceeding the upper limit, please modify the default allowlist.</div><br> |
|**Security Group** |allowlist associated security groups on demand. Support for associating a RDS for SQL Server allowlist with an ECS security group. Click **Select security group** and select the mode for binding security groups as needed in the **Modify security group** dialog box. Binding is supported through the following modes:<br><br><br>* **Associated ECSIP**: Allows Cloud as a Service in the security group to access the database, currently only the IP information import of the main network interface card is supported. Check the target security group from the drop\-down list of **Security groups** to support multiple selection.<br><br>* **Inbound IP**: Allows secure group entry direction in the source address where TCP protocol and ALL protocol involve IP access to the database, if the source address is configured as a security group it will be ignored. Check the target security group from the drop\-down list of **Security groups** to support multiple selection.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the ECS security group is adjusted after association, the security group can be synchronized in the cloud database SQL Server version allowlist to obtain the latest IP list in a timely manner.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">ECS security groups can be associated in two ways simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist can be associated with up to 10 ECS security groups.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When binding a security group by <strong>associating an Inbound IP</strong>, if the policy for an address in the security group is denied, the address will not be added to the SQL Server allowlist.</div><br> |



6. Click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After clicking <strong>OK</strong>, the system will determine whether the security group bound to the allowlist has been updated. If there is an update, the <strong>presence of an update is detected in the bound security group, whether to synchronize</strong> the dialog box lists the IP changes of the security group. Choose to <strong>synchronize</strong> or <strong>not synchronize as needed:</strong></div>


   * <div data-tips="true" data-tips-type="tip"><strong>Synchronization</strong>: The system will automatically identify the IP changes of the security group bound to the allowlist and update it to the allowlist. Please confirm whether the synchronization will affect the business.</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Out of sync</strong>: Ignore these IP changes and keep the original IP in the security group in the allowlist.</div>


* <div data-tips="true" data-tips-type="tip">After the modification is successful, this modification will be applied to all instances bound to the allowlist binding.</div>



<span id="related-documentation"></span>
## Related Documentation


* Binding instances and allowlist, see [Associating instances and allowlist](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-instance-to-allowlist).

* To unbind instances and allowlists, see [Disassociating instances from allowlists](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/disassociating-instance-from-allowlist) and [Disassociating allowlists from instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/disassociating-allowlist-from-instance).

* Delete allowlist, for details, see [Delete allowlist](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-allowlist).
