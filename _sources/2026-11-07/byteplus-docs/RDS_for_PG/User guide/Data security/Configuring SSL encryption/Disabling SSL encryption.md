---
title: "Disabling SSL encryption"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Disabling_SSL_encryption"
---

This topic describes how to disable SSL encryption for PostgreSQL instances.

<span id="09UfWvIl"></span>
## Prerequisites


* You have [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1), and the instance is in the **Running** status.

* The instance has SSL encryption enabled.

* Modifying the SSL configuration of the instance will <a i=1\>restart instance</a\>, please operate with caution.


<span id="RF68VG4d"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. On the instance details page, click the **Security** tab.

5. On the **Security** tab, click the **SSL** tab.

6. On the right side of the **SSL** tab, click the status button of the SSL feature.

7. In the pop\-up dialog box, click **OK** to disable the instance's SSL encryption feature.


<span id="gB0Ye1Jr"></span>
## Related APIs


|**API** |**Note** |
|---|---|
|[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBInstanceSSL) |Call the ModifyDBInstanceSSL interface to modify the SSL configuration of the specified instance. |
