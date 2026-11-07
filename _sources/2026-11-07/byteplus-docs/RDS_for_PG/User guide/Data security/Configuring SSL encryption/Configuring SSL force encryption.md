---
title: "Configuring SSL force encryption"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_SSL_force_encryption"
---

This topic describes the procedure to set SSL force encryption for an instance.

<span id="JZBlfluE"></span>
## Prerequisites


* Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* The instance has SSL encryption enabled. If not enabled, please see [Enabling SSL encryption](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_ssl_encryption).


<span id="YQgjFrCN"></span>
## Precautions

Enabling force encryption will interrupt non\-SSL connections to the instance, including connections between services such as DBW and DTS and the instance.

<span id="LFSKUFSs"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

4. On the **Instances** page, click the target instance name.

5. On the instance details page, click the **Security** tab.

6. On the **SSL** tab, click the state button on the right side of force encryption.

7. In the pop\-up dialog box, click **OK** to enable or disable the instance’s SSL force encryption function.


<span id="bFNxP5nl"></span>
## Related APIs


|**API** |**Note** |
|---|---|
|[DownloadSSLCertificate](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadSSLCertificate) |Call the DownloadSSLCertificate interface to download the SSL certificate of the specified instance. |
