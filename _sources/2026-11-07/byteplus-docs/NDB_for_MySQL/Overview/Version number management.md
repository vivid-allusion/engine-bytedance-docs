---
title: "Version number management"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Version_number_management"
---

A version number is an identifier for changes to the database structure or content. Whenever a major change is made to the database, the version number is incremented. This article describes the meaning and update rules of the NDB for MySQL Kernel version.

<span id=".54mI5pys5Y-36K-05piO"></span>
## Version number explanation

The version number format for NDB for MySQL is `Major version.Minor version.Revision version.Patch version`. The meaning of each field is as follows:


|Field |Major version |Minor version number |Revision version number |Patch version number |
|---|---|---|---|---|
|**Description** |Indicates the major version compatible with community MySQL. |* A minor version of a major community MySQL version.<br><br>* NDB for MySQL has a version with significant updates in features, architecture, and compatibility. |New or optimized features do not affect compatibility. |Indicates bug fix versions only. |
|**Update rules** |The major version number is updated when the major version of MySQL compatible with NDB for MySQL changes. |* The baseline version changes, for example, from MySQL 8.0.27 to MySQL 8.0.36.<br><br>* Compatibility changes, for example, being unable to upgrade in\-place. |* New features<br><br>* Existing feature optimizations |An update is required to fix bugs in a specific version. |
|**Value** |* `3`: compatible with MySQL 8.0<br><br>* `2`: compatible with MySQL 5.7 |`0`，`1`，`2`，...... |`1`，`2`，`3`，...... |`1`，`2`，`3`，...... |


<span id=".54mI5pys5Yqf6IO96K-05piO"></span>
## Version features


|Minor version |Kernel version |Description |
|---|---|---|
|**NDB for MySQL 2.0** |**2.0.\*.\***  |Compatible with the community version of MySQL 5.7.44. |
|**NDB for MySQL 3.0** |**3.0.\*.\***  |A stable version compatible with community MySQL 8.0.27. |


<span id=".5p-l55yL5a6e5L6L54mI5pys"></span>
## View the instance version


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the name of the target instance.

4. On the **Summary** page, you can view the **Kernel version** and **Compatible version** of the target instance in the **Configuration** section.
