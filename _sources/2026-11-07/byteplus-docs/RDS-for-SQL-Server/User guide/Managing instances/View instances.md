---
title: "View instances"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-instance-details"
---

After an instance is created, it is displayed in the Instances. In the instance list, you can customize the columns to select the information to display, and export the instance list to a local CSV file. This topic describes how to **View the instances**, **Customize the instance list**, and **Export the instance list**.

## **Prerequisites**

An instance has been created and is in the **Running** state. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

## **Procedure**

1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. In the **instances**, click the target instance to go to the **Summary** page.

4. On the **Summary** page, you can view the **Instance information**, **Configuration information**, **Usage statistics**, and **Billing information** for the instance.

   * The **Summary** section displays details such as the **Instance ID**, **Instance name**, **storage type**, **instance type**, **Super account**, **VPC**, **Availability zone**, **Project**, **Subnet**, **Tags**, **System database character set**, **System time zone**, and **Maintenance window**.

      > **tip**

      * > If an instance is created with its primary and secondary nodes deployed in different availability zones, the **Summary** section will display the availability zone and subnet for both nodes.

      * > If you are viewing information for a read\-only instance, the **Summary** area will display the ID of the primary instance.

      * > In the **Summary** section, click the **Reset Password** button to reset the password for the high\-permission user account. For more information, see [Reset password](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Reset_password).

      * > You can also use SSMS to view the instance's time zone and character set. For details, see [How to query the Time zone and character set of an SQL Server instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/how-do-I-query-time-zone-and-character-set-of-rds-for-sql-server-instance).

      * > To change the instance's maintenance window, click Edit. For detailed steps, see [Configur maintenance window](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/configuring-maintenance-window).

   * The **Configuration information** section displays the instance's **Database version**, **Instance specification**, **Minor version information**, **Specification family**, **CPU cores**, **Memory**, and **Disk size**.

   * The **Usage statistics** section displays the instance's **Disk usage** and **Backup usage**.

      * **Disk** **usage:**  The used and total disk space of the instance.

      * **Backup usage:**  The instance's backup usage and free backup quota.

   * The **Billing information** section displays the **billing type** and **Creation time** of the instance.

      > **tip**

      * > For a subscription instance that is not automatically renewed, you can click **Renewal management** to the right of **Billing type** to renew it manually. For more information, see [Renewal description](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/renewal-management).

      * > If an instance is undergoing a temporary upgrade, you can view its start and end dates in the **Billing information** section.

## Next steps

### Customize the instance list

The instance list displays information for each instance, such as the instance name and instance ID. You can customize the information to be displayed.

#### **Procedure**

1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region where the instance is located.

3. In the left navigation pane, click **Instances**.

4. On the **Instances** page, click **Customize Columns** in the upper\-right corner.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5435e383ac539ea5f89ce02d07e6b0eb.jpg)Customize the columns to be displayed in the instance list. You can customize which columns to display, except for **Instance name/ID** and **Actions**.

### Export the instance list

You can view your cloud instance resources offline. This topic describes how to export the instance list.

> **tip**

> If a primary instance includes read\-only instances, the read\-only instances are also exported by default. You can not choose to export only the primary instance or only the read\-only instances.

#### **Procedure**

1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region of the instance.

3. In the left navigation pane, click **Instances**.

4. On the **Instances** page, click the **Export** icon on the right.

5. In the **Export Instance list** dialog box, select the information you want to export. The following table lists the information that you can export:

   |Information |Required |
   |---|---|
   |Instance name/ID |Required |
   |State |Optional |
   |Availability zone |Optional |
   |Instance type |Optional |
   |Instance specification |Optional |
   |Database version |Optional |
   |Creation time |Optional |
   |Project |Optional |

6. Click **OK**.

> **tip**

> After exporting, the instance information is saved as a CSV file. You can download this file to your computer and open it with a text editor.
