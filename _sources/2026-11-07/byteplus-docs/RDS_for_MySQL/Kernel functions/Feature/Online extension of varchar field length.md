---
title: "Online extension of varchar field length"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Online_extension_of_varchar_field_length"
---

This topic describes the feature for extending varchar field lengths online in RDS for MySQL.

<span id="TbD0P4zy"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20250815 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20250815 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<span id="aSO8Odvn"></span>
## Background

Native MySQL does not allow using the inplace algorithm when extending a varchar field's length beyond 256 bytes. Only the copy algorithm is permitted. During this copy phase, users cannot modify the old table. All write requests are blocked, and only read requests are allowed.

RDS for MySQL supports extending varchar fields online across the 256\-byte boundary without blocking write operations during DDL execution. Additionally, when extending a field's length from 127 bytes or less to 256 bytes or more, the extension can be completed in seconds by modifying only the metadata, not the data.

<span id="rGUDFdF4"></span>
## Feature description

This feature implements Online DDL by changing the algorithm for extending varchar fields from copy to inplace. During a DDL process, you can continue writing to the old table. Subsequent write operations are replayed to the new table through the row log.

By using the properties of varchar fields, it can extend a field from 127 bytes or less to 256 bytes or more in seconds, without modifying the data.

<span id="F1O7x04E"></span>
## Instructions

<span id="4liwCnlz"></span>
### Parameter description

A new parameter is added to manage the online extension of varchar fields.


|Parameter name |Description |Effective scope |Value range |Default value |
|---|---|---|---|---|
|loose_extend_varchar_enhance |Specifies whether to enable the extended varchar enhancement feature. |GLOBAL/SESSION |ON/OFF |OFF |


When the parameter is enabled, the extensions are classified as follows:


|Varchar field length |Whether to support online expansion |Whether to support modifying only metadata |
|---|---|---|
|Extensions within 256 bytes |Support |Support |
|Expansion from 0–127 bytes to 256 bytes or more |Support |Support |
|Extends from 128\-255 bytes to 256 bytes or more |Support |Not support |
|Expansion for lengths of more than 256 bytes |Support |Support |


<span id="9EAR4o6r"></span>
### Examples

After you set the `loose_extend_varchar_enhance` parameter to `ON`, the online varchar field extension feature is enabled. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).


* Extensions within 256 bytes

   ```SQL
   create table t(c1 varchar(100))charset ascii;
   Query OK, 0 rows affected (0.017 sec)
   
   alter table t modify column c1 varchar(170),algorithm=inplace,LOCK=NONE;
   Query OK, 0 rows affected (0.007 sec)
   Records: 0  Duplicates: 0  Warnings: 0
   ```
   

* Expansion from 0–127 bytes to 256 bytes or more

   ```SQL
   create table t(c1 varchar(100))charset ascii;
   Query OK, 0 rows affected (0.011 sec)
   
   alter table t modify column c1 varchar(300),algorithm=inplace,LOCK=NONE;
   Query OK, 0 rows affected (0.006 sec)
   Records: 0  Duplicates: 0  Warnings: 0
   ```
   

* Expansion from 128–255 bytes to 256 bytes or more

   ```SQL
   create table t(c1 varchar(170))charset ascii;
   Query OK, 0 rows affected (0.013 sec)
   
   alter table t modify column c1 varchar(300),algorithm=inplace,LOCK=NONE;
   Query OK, 0 rows affected (0.020 sec)
   Records: 0  Duplicates: 0  Warnings: 0
   ```
   

* Expansion for lengths of more than 256 bytes

   ```SQL
   create table t(c1 varchar(300))charset ascii;
   Query OK, 0 rows affected (0.012 sec)
   
   alter table t modify column c1 varchar(400),algorithm=inplace,LOCK=NONE;
   Query OK, 0 rows affected (0.005 sec)
   Records: 0  Duplicates: 0  Warnings: 0
   ```
