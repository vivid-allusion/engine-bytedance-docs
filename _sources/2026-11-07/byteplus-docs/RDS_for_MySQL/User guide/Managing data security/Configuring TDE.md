---
title: "Configuring TDE"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_tde"
---

This topic describes how to enable transparent data encryption (TDE) encryption.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

RDS for MySQL provides the transparent data encryption (TDE) function. TDE can execute real\-time I/O encryption and decryption for data files. Data is encrypted before being written to a disk and decrypted when being read into the memory from the disk, which can meet the compliance requirements of static data encryption. TDE does not increase the size of data files, and the developer can use TDE without modifying any application.

In RDS for MySQL, TDE adopts the AES_256_CBC encryption algorithm.

<span id="qkHZTW6Y"></span>
## Limitation


* Instances that use the RocksDB engine do not support transparent data encryption.

* MySQL 8.4 instances do not support the TDE encryption function.

* Transparent data encryption is currently only available in the following regions:

   
   |Region name |Region ID |
   |---|---|
   |China (Beijing) |cn\-beijing |
   |China (Shanghai) |cn\-shanghai |
   |China (Hong Kong) |cn\-hongkong |
   |Asia Pacific (Johor) |ap\-southeast\-1 |
   |Asia Pacific (Jakarta) |ap\-southeast\-3 |
   


<span id="ECwDEBFm"></span>
## Precautions


* To enable the TDE function, the instance must be restarted.

* Once the TDE function is enabled, it cannot be disabled.

* After turning on the transparent data encryption TDE function, if you want to restore the data, you need to decrypt the data first.

* After enabling TDE by following the procedure below, performing DDL operations on MySQL tables is required to encrypt or decrypt data. The specific methods are as follows:

   * Encryption: `ALTER TABLE `t` ENCRYPTION='Y';`

   * Decryption: `ALTER TABLE `t` ENCRYPTION='N';`


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1), and the instance is in the **Running** status.

* To enable TDE, you need to enable the Key Management System service first.

   * If you select **Use an automatically generated default key**, you need to enable the Cloud Service Hosted Key Management Service. To enable the service, refer to [Enable Cloud Service Hosted Key Management service](https://console.byteplus.com/common-buy/CloudKMS/?return_url=/kms/region:kms+cn-shanghai/primary).

   * If you select **Use an existing custom key**, you need to enable both the Key Management System service and the Cloud Service Hosted Key Management Service. To enable the services, refer to [Enable Key Management System service](https://console.byteplus.com/kms/region:kms+cn-shanghai/primary?projectName=default) and [Enable Cloud Service Hosted Key Management service](https://console.byteplus.com/common-buy/CloudKMS/?return_url=/kms/region:kms+cn-shanghai/primary).

* The account already has `STSAssumeRoleAccess`, `iam:CreateServiceLinkedRole` permissions.

* The instance is not a disaster recovery instance and there is no associated disaster recovery instance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click the **Security** tab, and then click **Data encryption**.

6. Turn on the **TDE state** switch.

7. In the popped\-up dialog box, after completing the following settings, click **OK**.

   
   |Configuration items |Details |
   |---|---|
   |Key type |Select the type of key to use for encryption.<br><br><br>* Use an automatically generated default key.<br><br>* Use an existing custom key<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using a custom key, you need to specify the key and keyring.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also refer to  and <a href="https://docs.byteplus.com/en/docs/kms/Getting_started_with_secret_management">Create a keyring</a> to create a new keyring and key.   </div><br>    |
   |Switch time |Select the time to enable the transparent data encryption(TDE) feature.<br><br><br>* **Execute now**: Execute immediately after clicking OK.<br><br>* **Specific time period**: Execute in the specific time period. If the switching time is selected to be performed within the **Specified time period**, the time period for opening the function needs to be set in the window.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Setting the upgrade time period across days is not supported.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The shortest time period is two hours.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Set the upgrade time period within the time frame prompted by the console.   </div><br>   <br><br>* **Maintenance window**: Execute within the maintenance period set for the instance. If you choose to enable within the **Maintenance window**, you need to confirm the **Maintenance window** of the instance.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.   </div><br>    |
   


&nbsp;

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DescribeDBInstanceTDE](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancetde) |Call DescribeDBInstanceTDE to query the enabled/disabled state of the transparent data encryption function of an instance. |
|[ModifyDBInstanceTDE](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancetde) |Call the ModifyDBInstanceTDE API to modify the TDE settings of an instance. |
