---
title: "Associating allowlists with instances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_instances_to_allowlists_1"
---

After adding an IP address to an allowlist, you must also associate the allowlist with an instance to allow the IP address to successfully access the MySQL instance. Since allowlists and instances have a many\-to\-many relationship, you can either associate an instance to an allowlist or associate an allowlist to an instance. This topic describes how to associate an instance with an allowlist.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Allowlist is a security prevention and control method for database connections, only IP addresses in the allowlist can access the database. A MySQL instance is not associated with any allowlists after it is created. By default, all Internet protocol addresses are denied access to the instance. Therefore, whether you access the instance through a VPC intranet or the public network, you must configure an allowlist for the instance to ensure it is connectable.

Allowlists support IP address ranges in CIDR format, such as `192.168.0.0/32` (where any integer from 0 to 31 can be entered after the slash), which allows access from any IP address within that network segment.

You can now associate Elastic Computing Services security groups with MySQL allowlists. After associating an ECS security group, you can import the IP addresses of all ECS instances in that security group to the allowlist. This allows all these ECS instances to access the MySQL instance associated with the allowlist.

RDS for MySQL supports setting an allowlist as the default. After an allowlist is set as the default, it is automatically associated when you create a new instance, restore to a new instance, or purchase a new instance.

If you have previously used the session management feature provided by the Database Workshop (DBW) or operated on a MySQL instance using the Database Transmission Service (DTS), the instance will be added to the system built\-in allowlist. System built\-in allowlists cannot be edited, disassociated, or deleted.


* The built\-in allowlist added by DBW for MySQL instances is named `DBW_Sole_Group_Name_For_RDS`.

* The built\-in allowlist added by DTS for MySQL instances is named `dts_internal_for_EndpointVolcMySQL`.


The allowlist needs to be maintained regularly to remove IP addresses that no longer need to access the MySQL instance to ensure the security of database connections.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Each allowlist can contain up to 300 IPs or IP segments.

* Each allowlist can be associated with up to 500 instances.

* Each instance can associate up to 100 IP allowlists.

* Each instance supports up to 300 IP addresses or IP address segments in total across all associated allowlists. If you have a large number of IP addresses, it is recommended to consolidate individual IP addresses into IP address segments.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL](https://console.byteplus.com/db/rds-mysql) console.

2. In the upper\-left corner of the top menu bar, select the region where the allowlists and instance are located.

3. Click **Allowlists** on the left navigation bar.

4. Click **Associate with an allowlist** in the **Actions** column of the target allowlist to open the **Associate instances** page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, click the name of the target allowlist to go to the <strong>Allowlist details</strong> page. On the <strong>Allowlist details</strong> page, click <strong>Associate instance</strong> to open the <strong>Associate instances</strong> page.   </div>
   

5. On the **Associate instances** page, select the target instances in the instances list and click **OK** to complete the association.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can search by instance name or instance ID to quickly locate the target instance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can associate up to 200 instances to an allowlist in a single operation.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[AssociateAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associateallowlist1) |Call the AssociateAllowList API to associate the target instance with the specified IP address allowlist. |
