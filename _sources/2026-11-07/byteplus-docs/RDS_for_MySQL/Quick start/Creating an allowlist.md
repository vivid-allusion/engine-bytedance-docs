---
title: "Creating an allowlist"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_allowlist"
---

This topic describes how to manually add client IP addresses, CIDR segments, or ECS security groups to an allowlist in order to access MySQL instances.

<span id="cP4Nhfjt"></span>
## Background

Allowlist is a security prevention and control measure for database connections. Only IP addresses within the allowlist can access the database. After a MySQL instance is created, it will not be bound to any allowlist by default, and all IP addresses are prohibited from accessing the instance. Therefore, whether accessing the instance through the VPC internal network or the public network connection, it is necessary to configure the allowlist of the instance first to ensure that the instance can be connected.

The allowlist supports setting IP address segments in CIDR format, such as: `192.168.0.0/32` (any integer between 0 and 31 can be entered after (/)), allowing IP addresses within this network segment to access.

The MySQL allowlist already supports associating with ECS security groups, and it is possible to bind ECS security groups to the MySQL allowlist. After binding the ECS security group, the IP addresses of all ECS instances under the corresponding ECS security group can be imported into this allowlist, enabling all ECS instances under these ECS security groups to access the MySQL instance bound to this allowlist.

RDS for MySQL supports setting a certain allowlist as the default allowlist. After being set as the default allowlist, when creating new instances, restoring to new instances, and purchasing new instances, the default allowlist will be automatically bound.

If you have previously used the session management function provided by the Database Workshop (DBW), or have used the Database Transmission Service (DTS) to operate on MySQL instances, the instance will be added with a system\-built\-in allowlist. The system\-built\-in allowlist does not support editing, unbinding, or deletion.


* The name of the built\-in allowlist added by DBW for MySQL instances is `DBW_Sole_Group_Name_For_RDS`.

* The name of the built\-in allowlist added by DTS for MySQL instances is `dts_internal_for_EndpointVolcMySQL`.


The allowlist needs to be regularly maintained, removing IP addresses that no longer need to access the MySQL instance to ensure the security of database connections.

<span id="k9CgejWN"></span>
## Limits


* Each product of each tenant is allowed to create up to 500 allowlists in each region.

* Each allowlist can contain up to 300 IP addresses or CIDR segments.

* Each allowlist can be associated to up to 500 instances.

* A single instance can be associated to up to 100 allowlists (including the system built\-in allowlists).

* A maximum of 10 security groups can be added to an allowlist at a time.

* A single instance can support up to 300 IP addresses or CIDR segments (the sum of IP addresses or CIDR segments in all associated allowlists). When there are many IP addresses, we recommend you merge IP addresses into CIDR segments.


<span id="mWdCZFpU"></span>
## Precautions


* If `0.0.0.0/0` is set, access by all addresses is allowed. If `127.0.0.1` is set, access by all addresses is prohibited. If `0.0.0.0/0` and `127.0.0.1` are set simultaneously, access by all addresses is allowed.

* When accessing a MySQL instance across VPCs, you need to add `100.64.0.0/10` to the instance allowlist.

* If the allowlist is set as the default allowlist, when creating a new instance, restoring to a new instance, or purchasing an instance with the same configuration, the default allowlist will be automatically selected unless manual settings are made. Since each allowlist can be associated to a maximum of 500 instances, binding cannot occur when more than 500 instances are present. It is recommended to regularly check the number of instances associated to the default allowlist and update the default allowlist regularly.

* If the allowlist is set as the default allowlist, the allowlist cannot be deleted directly. You need to edit the allowlist to change it to a normal allowlist and unbind it from the instance before you can delete it.

* If the security group is updated after being associated with the allowlist, you need to click **Sync security group** in the action column of the target allowlist in the allowlist list to allow the allowlist to obtain the updated IP of the security group.

* If the security group is updated after being associated with the allowlist, when you edit the allowlist associated with the security group and submit it, the update of the security group will be automatically synchronized.

* If you specify it as the default allowlist when creating a allowlist, this allowlist will replace the original default allowlist (if any).


<span id="NXRuG2hx"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. Select the region for the allowlist in the upper\-left corner of the top menu bar.

3. Click **Allowlist** in the left\-side navigation bar.

4. Click **Create allowlist**. Fill in the parameters in the table below, and then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Allowlist name |Required.Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* The name starts with a Chinese character, letter, or underscore (_).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1 to 128 characters. |
   |Description |Optional. Description information can be used to search for an allowlist in the list of allowlists, and the length of the description content shall not exceed 200 characters. |
   |IP address |Required. The instance can only be accessed by IP addresses added to the allowlist. Pasting IP addresses or CIDR segments is supported, and they are separated by single\-byte or double\-byte commas, spaces, or line breaks. |
   |Default allowlist |Select whether to set this allowlist as the default allowlist. A default allowlist can be set in the tenant dimension, which will be checked by default when creating a MySQL instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An allowlist can bind up to 500 instances, modify the default allowlist after exceeding the limit.</div><br> |
   |Security group |Supports associating the MySQL allowlist with the ECS security group. If the ECS security group is adjusted after association, the security group can be synchronized in the allowlist of MySQL to obtain the latest IP list in a timely manner.<br><br>Click **Select security group** and select the security group to be associated in the **Editorial Security Group** window. Associating is supported in two modes:<br><br><br>* **Associated ECSIP**: Allows cloud servers in the security group to access the database. Currently, only the IP information of the main network card is supported.<br><br>* **Inbound IP**: Allow the IP involved in the TCP protocol in the source address of the security group in the inbound direction to access the database. If the source address is configured as a security group, it will be ignored.<br><br><br><div data-tips="true" data-tips-type="tip">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">ECS security groups can be associated in two ways at the same time.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When binding a security group using the <strong>Inbound IP</strong> method, if the policy of an address in the security group is Deny, the address will not be added to the MySQL allowlist.</div><br> |
   


&nbsp;

<span id="geuVD9CT"></span>
## FAQs

**Is it necessary to set an allowlist for a MySQL instance?** 

If a default allowlist is set, the MySQL instance will be associated to the default allowlist after creation. If no default allowlist is set, no allowlist will be associated to the instance after it is created, and no IP will be able to access the MySQL instance.

**What is the maximum number of allowlists a single instance can be associated to?** 

A single instance can be associated to up to 100 allowlists.

**How many IP addresses or CIDR segments does each allowlist support?** 

Each allowlist supports up to 300 IP addresses or CIDR segments.

**Can an allowlist be associated to multiple instances?** 

Supported. An allowlist can be associated to up to 500 instances.

<span id="FDwAslY7"></span>
## Related APIs


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createallowlist1) |Call the CreateAllowList interface to create a new allowlist. |


&nbsp;
