---
title: "Viewing instance information"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details"
---

This topic describes how to view instance information for RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

On the **Summary** tab, you can view the instance’s **Summary**, **Configuration**, **Usage statistics**, and **Billing method**.


|Scope |Details |
|---|---|
|Summary |Summary includes instance ID, instance name, network information (Virtual Private Cloud and subnet), instance type, storage type, availability zone, project, maintenance window, and tag.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the instance is not in the Running state, hover over the status text to view the associated task or operation and maintenance event.</div><br> |
|Configuration |Configuration information includes database version, kernel version upgrade policy, primary node specifications, specification type, number of nodes, cores, memory, disk size, data synchronization method, and global read\-only.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The database version includes the compatible version and kernel version of the instance. For example, the version number MySQL 5.7.32_20240615 indicates that this is a MySQL 5.7 instance, and the kernel minor version is MySQL 5.7.32_20240615.</div><br> |
|Usage statistics |Usage statistics includes disk usage, basic backup usage, and settings for automatic storage expansion. Basic backup usage is the total data volume of all retained log and data backups within the current region, excluding cross\-region backup usage.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To save storage space and improve backup download efficiency, RDS for MySQL compresses backup files that meet certain conditions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each instance receives free backup storage space equal to the storage space of its primary node.</div><br> |
|Billing information |Billing information includes billing method, creation time, and enable automatic renewal (displayed when the instance billing method is Subscription). |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Instances** to view the list of RDS for MySQL instances.

4. In the **Instances**, click the name of the target instance to enter the **Summary** tab and view detailed information about the instance.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps


* [Upgrade instance kernel version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version)

* [Kernel version upgrade policy settings](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Modifying_instance_kernel_minor_version_upgrade_policy)

* Analyzing instance storage space usage

   On the **Summary** tab, in the **Usage statistics** section, click **Spatial analysis** to open the **Spatial analysis** page in Database Workshop. This page provides a spatial analysis feature for visualizing the space usage of an instance, such as tablespace analysis. For more information, refer to [Spatial analysis management](https://docs.byteplus.com/en/docs/DBW/spatial-analysis-management-for-mysql).
