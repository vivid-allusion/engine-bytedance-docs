---
title: "Restore to existing instance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Restoring_to_an_existing_instance"
---

This topic describes the procedure for restoring data to an existing instance. 

<span id="USC5DIBb"></span>
## Prerequisites


* A logical backup has been created for the data to be restored. For more information, see [Creating a backup](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_manual_backup).

* Both the backup instance and the recovered target instance are in the **Running** state.


<span id="kVuKLtgW"></span>
## Precautions


* Restoring a database to an existing instance through a logical backup is supported only.

* The compatible version of the target instance needs to be the same as the instance where the backup is located.

* Supports restoring the instance where the backup is located as the target instance.

* In a single recovery operation, only restoring data to one target instance is supported.


<span id="23ZqYheE"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name to enter the instance details page.

4. At the top of the page, click the **Backups** tab.

5. On the **Backups** tab, click **Restore to existing instance** under the **Data backup** tab.

6. On the **Restore to existing instance** page, click **Next** step after completing the following configuration.

   
   |**Parameters** |**Is it required?**  |**Note** |
   |---|---|---|
   |Restore method<br><br> |Yes |Choose a recovery method Currently only restore **By backup** set is supported. The recovery method by backup set refers to restoring instances from a specified backup set, and the selection range of the backup set is determined according to the number of days the backup is retained. |
   |Backup and recovery |Yes |Select the backup set to restore. |
   |Target instance |Yes |Select the target instance for data recovery.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The compatible version of the target instance needs to be the same as the instance where the backup is located.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Supports restoring the instance where the backup is located as the target instance.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only one target instance can be selected.</div><br> |
   |Target instance account |Yes |Select the account in the target instance to use as the owner of the newly restored database.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only super accounts that have not had their DDL permissions disabled are supported.</div><br> |
   |Database management |Yes |Select the database that needs to be restored from the backup set.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can choose up to 50 libraries for recovery at a time.</div><br> |
   



&nbsp;

7. After confirming the selected data to be recovered and the restored database name, click **OK**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">By default, the restored database is named according to [original library name] _bak_ [backup ID].</div>


* <div data-tips="true" data-tips-type="default">Modifying the database name is supported. The following rules should be met when modifying. If not, the recovery task cannot be initiated.</div>


   * <div data-tips="true" data-tips-type="default">The name is unique within the instance.</div>


   * <div data-tips="true" data-tips-type="default">2 to 63 characters in length.</div>


   * <div data-tips="true" data-tips-type="default">Must start with a letter and end with a letter or a digit.</div>


   * <div data-tips="true" data-tips-type="default">Can contain letters, digits, underscores (_) and hyphens (\-).</div>


   * <div data-tips="true" data-tips-type="default">Some reserved words or keywords cannot be used in the database name, see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_forbidden_keywords">Reserved keywords</a> for all reserved keywords.</div>



<span id="A5BJxSoB"></span>
## Related APIs


|API |Note |
|---|---|
|[RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/RestoreToExistedInstance) |Call RestoreToExistedInstance API to restore data to an existing instance. |


&nbsp;

&nbsp;
