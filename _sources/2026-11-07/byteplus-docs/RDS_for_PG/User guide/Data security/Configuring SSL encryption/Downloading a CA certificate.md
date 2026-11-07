---
title: "Downloading a CA certificate"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Downloading_a_CA_certificate"
---

This topic introduces the procedure for downloading SSL certificates of PostgreSQL instances.

<span id="mjdbrAnV"></span>
## Prerequisites


* Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* The instance has SSL encryption enabled. If it is not enabled, please refer to [Enabling SSL encryption](https://docs.byteplus.com/en/docs/RDS_for_PG/Enabling_SSL_encryption).


<span id="U1S25n8o"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. On the instance details page, click the **Security** tab.

5. On the **SSL** tab, click **Download the CA Certificate**.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The downloaded CA certificate is a compressed PEM file named after the instance ID. You can specify the SSL parameters and the corresponding certificate when accessing from the client.</div>


<span id="DAcze1pR"></span>
## Related APIs


|**API** |**Note** |
|---|---|
|[DownloadSSLCertificate](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadSSLCertificate) |Call the DownloadSSLCertificate interface to download the SSL certificate of the specified instance. |
