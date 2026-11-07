---
title: "Enabling SSL encryption"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Enabling_SSL_encryption"
---

To enhance the security of the link, RDS for PostgreSQL provides SSL (Secure Sockets Layer) encryption service. This topic introduces how to set up SSL encryption for a PostgreSQL instance in the console.

<span id="k3CgPmUb"></span>
## Background information

SSL (Secure Sockets Layer) is a security protocol specifically designed for secure communication and data security. It encrypts network connections at the transport layer, which improves the security of communication data while ensuring the integrity of the data. After SSL 3.0, it was renamed TLS (Transport Layer Security).

RDS for PostgreSQL supports TLS versions 1.2 and 1.3.

<span id="HjVjlzjX"></span>
## Prerequisites

Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id="AkIpqnGD"></span>
## Precautions


* Since enabling SSL encryption will increase the network response time of the PostgreSQL service, it is recommended to enable SSL encryption only when encryption is required (for example, when connecting to a PostgreSQL instance via the public network).

* Modifying the SSL configuration of an instance will restart the instance. Please proceed with caution.

* The Database Workshop currently does not support operations on instances with SSL encryption enabled. If you rely on using the database workbench, please enable this feature with caution.

* After enabling SSL encryption, be sure to update the SSL certificate in a timely manner. The validity period of the SSL certificate is one year from the time SSL encryption is enabled.


<span id="8JELs4ga"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. On the instance details page, click the **Security** tab.

5. On the **Security** tab, click the **SSL** tab.

6. On the right side of the **SSL** tab, click the state button of the SSL feature.

7. In the pop\-up dialog box, click **OK** to Enable the instance’s SSL encryption feature.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After clicking OK, the instance will restart. After the instance completes restarting and you refresh the page, you can view the instance’s protected address.   </div>
   

<span id="a5xaKp7t"></span>
## Subsequent Steps


* [Configuring SSL force encryption](https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_SSL_force_encryption)

* [Downloading a CA certificate](https://docs.byteplus.com/en/docs/RDS_for_PG/Downloading_a_CA_certificate)

* [Updating an SSL certificate](https://docs.byteplus.com/en/docs/RDS_for_PG/Updating_an_SSL_certificate)


<span id="iIgGsYm3"></span>
## Related APIs


|**API** |**Note** |
|---|---|
|[DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceSSL) |Call the DescribeDBInstanceSSL API to query the SSL settings of the specified instance. |
|[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBInstanceSSL) |Call the ModifyDBInstanceSSL interface to modify the SSL configuration of the specified instance. |
