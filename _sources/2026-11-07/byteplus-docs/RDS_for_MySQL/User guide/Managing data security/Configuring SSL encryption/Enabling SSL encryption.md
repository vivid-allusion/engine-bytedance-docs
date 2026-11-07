---
title: "Enabling SSL encryption"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_ssl_encryption"
---

MySQL provides Secure Sockets Layer (SSL) encryption to improve link security. This topic describes how to enable SSL encryption in the MySQL console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

SSL encryption encrypts network connections at the transport layer, improving the security and integrity of communication data.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1), and the instance is in the **Running** status.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Because enabling SSL encryption increases the network response time of the MySQL service, enable it only when encryption is required, such as when connecting to a MySQL instance via the public network.

* Modifying the SSL configuration of an instance will restart the instance. Please proceed with caution.

* The Database Workshop currently does not support operations on instances with SSL encryption enabled. If you rely on using the database workbench, please enable this feature with caution.

* MySQL 8.4 instances do not support enabling SSL encryption.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. On the **Instances** page, click the target instance name.

4. On the instance details page, click the **Security** tab.

5. On the **Security** tab, click the **SSL** tab.

6. On the right side of the **SSL** tab, click the state button of the SSL feature.

7. In the dialog box that appears, set the switch time and click **OK**. You can enable the feature immediately, within a specific time period, or during the maintenance window.

   * **Execute now**: Execute immediately after clicking OK.

   * **Specific time period**: Execute in the specific time period. If you select to enable the feature at a **Specific time**, you need to set the time period for enabling the feature in the window.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Setting the upgrade time period across days is not supported.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The shortest time period is two hours.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Set the upgrade time period within the time frame prompted by the console.      </div>
      

   * **Maintenance window**: Execute within the maintenance period set for the instance. If you choose to enable within the **Maintenance window**, you need to confirm the **Maintenance window** of the instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.      </div>
      


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps


* [Download SSL certificate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_a_ca_certificate)

* [Updating an SSL certificate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/updating_an_ssl_cert)


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancessl) |Call the DescribeDBInstanceSSL API to query the SSL settings of a specified MySQL instance. |
|[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancessl) |Call the ModifyDBInstanceSSL API to modify the SSL settings of a specified MySQL instance. |
