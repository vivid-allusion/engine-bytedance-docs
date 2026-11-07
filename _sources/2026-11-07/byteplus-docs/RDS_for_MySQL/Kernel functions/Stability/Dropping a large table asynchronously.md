---
title: "Dropping a large table asynchronously"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_a_table_asynchronously"
---

This topic describes how to use RDS for MySQL to drop large tables asynchronously.

<span id=".6IOM5pmv"></span>
## Background

When the data file of a table is large, deleting the table synchronously can impact the running instance and cause I/O jitters.

<span id=".5Yqf6IO95LuL57uN"></span>
## Function introduction

RDS for MySQL supports dropping large tables asynchronously. After you enable the feature to drop large tables asynchronously, the kernel automatically deletes large tables asynchronously, which reduces the performance fluctuations on the instance caused by the delete operation. You do not need to perform any other operations after deleting a table. The kernel automatically completes the remaining tasks. When you delete a large table asynchronously, its data file is first renamed to a temporary file. Then, a background thread smoothly truncates the temporary file.

<span id=".6YCC55So5Zy65pmv"></span>
## Use cases

This feature is suitable for business scenarios that require deleting large tables and are sensitive to performance fluctuations.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20241015 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20240215 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5L2_55So6K-05piO"></span>
## Instructions

Asynchronous deletion of large tables is disabled by default. You can use this feature by setting the modifiable parameters `loose_innodb_data_file_logic_drop` and `loose_innodb_data_file_logic_drop_max_size`.


* Modify `loose_innodb_data_file_logic_drop` to `ON` to enable this feature.

* Modify `loose_innodb_data_file_logic_drop_max_size` to specify the file size to be truncated in the background each time a large table is deleted asynchronously.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The background truncation frequency of RDS for MySQL is 5 times per second. For example, if <code>loose_innodb_data_file_logic_drop_max_size</code> is configured as 1024 MiB, theoretically, 5 GiB of data files are truncated per second.   </div>
   

For more information about `loose_innodb_data_file_logic_drop` and `loose_innodb_data_file_logic_drop_max_size`, refer to the following table.


|Parameter name |Parameter description |
|---|---|
|loose_innodb_data_file_logic_drop |Specifies whether to enable asynchronous cleanup of large tables. Values:<br><br><br>* OFF: disable (Default).<br><br>* ON: enable.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect after modification without an instance restart.</div><br> |
|loose_innodb_data_file_logic_drop_max_size |The size of each file to be truncated in the background when asynchronously deleting large tables. Value range: 128\-2048. Default value: 1024. Unit: MiB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter takes effect after modification without an instance restart.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The current truncate frequency for RDS for MySQL is 5 times per second, and the theoretical speed for asynchronously deleting large tables is <code>loose_innodb_data_file_logic_drop_max_size</code> \* 5.</div><br> |


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**

You can use this feature by setting the modifiable parameters `loose_innodb_data_file_logic_drop` and `loose_innodb_data_file_logic_drop_max_size`. RDS for MySQL supports modifying parameters through the console and Open API.


* Modify through the console

   Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql) and modify parameters on the **Parameter configuration** tab. For more information, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

* Modify via Open API

   Call the ModifyDBInstanceParameters API to modify parameters. For more details, refer to [ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceparameters).
