---
title: "Updating an SSL certificate"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Updating_an_SSL_certificate"
---

An SSL certificate has a validity period. You can update the SSL certificate before it expires to extend its validity by one year. This topic introduces the procedure to update the SSL certificate validity period for a PostgreSQL instance.

<span id="ri1N0FJb"></span>
## Precautions


* Updating the SSL certificate validity period of an instance will restart the instance. Please proceed with caution.

* After updating the SSL certificate, the certificate validity period will be calculated as one year from the date of the update.


<span id="U3fwaBpR"></span>
## Prerequisites


* Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* The instance has SSL encryption enabled. If it is not enabled, please refer to [Enabling SSL encryption](https://docs.byteplus.com/en/docs/RDS_for_PG/Enabling_SSL_encryption).


<span id="Ka73kzUE"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. On the instance details page, click the **Security** tab.

5. On the **SSL** tab, click **Update certificate**, and in the pop\-up dialog box, click **OK**.


<span id="DoaItTql"></span>
## Related APIs


|**API** |**Note** |
|---|---|
|[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBInstanceSSL) |Call the ModifyDBInstanceSSL interface to modify the SSL configuration of the specified instance. |
