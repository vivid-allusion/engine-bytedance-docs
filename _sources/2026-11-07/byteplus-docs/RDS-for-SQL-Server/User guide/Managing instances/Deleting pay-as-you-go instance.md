---
title: "Deleting pay-as-you-go instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-pay-as-you-go-instance"
---

You can release a volume\-based billing instance manually based on business requirements. This article describes how to delete a volume\-based billing SQL Server instance.

<span id="prerequisite"></span>
## **prerequisite**

The [instance was created](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) and is **in the running** state.

<span id="billing-instructions"></span>
## Billing instructions

After the volume\-based billing master or read\-only instance is successfully deleted, the instance will stop billing immediately. For more information about volume billing, see [volume billing](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/pay-as-you-go).

<span id="precautions"></span>
## Precautions


* After the instance is deleted, it is immediately cleared, and the data is no longer retained.

* If the master instance contains read\-only instances, deleting the master instance also deletes the read\-only instances.

* After deleting a read\-only instance, the read\-only instance will be cleared immediately. Backup and recovery are not supported. If there is a request to read data, you can create a new read\-only instance. For the steps to create a read\-only instance, see [Create a read-only instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-read-only-instance).


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instance List** page, click Delete Instances in the Target Instance Action column.

4. Are you **sure to delete the selected instance?**  Dialog box, configure the following information.

   * **Backup policy**: Choose a backup policy based on instance type. The details are as follows:

      * **Create a final backup**: Indicates that the instance goes into Recycle Bin after deletion and is kept for seven days. You can also rebuild your instance and recover your data within seven days. When deleting a primary instance, only the option to create a final backup is supported.

      * **Do not keep backups**: means that the instance will be wiped immediately after deletion, and the data will not be retained. When deleting a read\-only instance, only the option not to keep a backup is supported.

   * **Delete Confirmation**: Enter your instance name for secondary confirmation.

5. Click **Delete**.
