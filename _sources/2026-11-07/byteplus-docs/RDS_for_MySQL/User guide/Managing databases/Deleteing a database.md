---
title: "Deleteing a database"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_a_database"
---

This topic describes how to delete a database.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* A database has been created. For more information, refer to [Creating a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After a database is deleted, its data will be lost. Proceed with caution.

* Only databases that meet the [database naming rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database#.5pON5L2c5q2l6aqk) can be deleted from the console.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Databases**.

6. On the **Databases** tab, click **Delete** in the **Actions** column for the target database.

7. In the **Deletion confirmation** text box, enter the name of the database to be deleted, and then click **OK**.

8. In the displayed dialog box, complete the following settings, and then click **OK**.

   
   |Configuration item |Description |
   |---|---|
   |Confirm to delete |In the **Deletion confirmation** text box, enter the name of the database to be deleted to confirm. |
   |Retain account permissions |Select whether to retain the privileges of the associated account for a database with the same name when deleting the database.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This option does not impact global privileges (\*.\*).</div><br> |
   


<span id=".55u45YWzLWFwaQ=="></span>
## FAQ

How to view the deletion time of a database?


* For databases deleted via the **database management** page of the console, click **Task Center** on the left‑side navigation bar of the console, and you can view the deletion time on the **Task Center** page.

* For databases deleted via SQL commands, if you have enabled database auditing, click **Database Workshop** on the top menu bar, and you can view the deletion time in the **Database Audit** page.


<span id="rYhDl3mF"></span>
## Related API


|API |Description |
|---|---|
|[DeleteDatabase](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedatabase1) |Call the DeleteDatabase API to delete a database. |
