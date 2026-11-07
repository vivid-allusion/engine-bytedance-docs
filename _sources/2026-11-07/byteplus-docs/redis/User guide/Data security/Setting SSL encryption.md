---
title: "Setting SSL encryption"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/setup-ssl"
---

Redis offers Secure Sockets Layer (SSL) encryption services to improve the security of the link. This topic describes how to configure SSL encryption on the Redis console.

## Background information

By encrypting network connections at the transport layer, SSL encryption improves communication data security and ensures data integrity.

## Precautions

* Enabling SSL encryption may increase the network response time of Redis services. Recommend to enable SSL encryption only encryption can be justified (such as when connecting to Redis instances via the internet).

* After enabling SSL encryption, if you need to connect to an instance via the Redis\-cli client, then:

   * Clients with a Redis\-cli version below 6 do not support verifying certificates during connection. Please use Redis\-cli version 6 or a higher version.

   * Before connecting to the instance, execute the `make BUILD_TLS=yes` command to compile the Redis\-cli client file. To connect to an instance via Redis\-cli, refer to [Connecting to instance via Redis-cli](https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli).

* SSL certificates are valid for 1 year by default. Please update the certificate validity period and re\-download and configure the CA certificate in time, otherwise client applications using encrypted connections will not be able to connect properly.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Security** tab.

5. Click the **SSL** sub\-tab.

6. On the **SSL** sub\-tab, you can execute corresponding commands according to your service requirements.

   **Enable SSL encryption**

Turn on the feature switch to the right of the SSL certificate.

   Once enabled, the **SSL certificate validity** status changes to **Valid**, indicating that SSL encryption is active.

   > Description

   > After enabling SSL encryption, clients must use the SSL certificate and connect to Redis instances using SSL. For specific procedures, refer to [Connecting to Redis from client via SSL encryption](https://docs.byteplus.com/en/docs/redis/connect-redis-from-client-via-ssl).

   **Disable SSL encryption**

Turn off the feature switch to the right of the SSL certificate.

   Once disabled, information such as **SSL certificate validity** will no longer be displayed, indicating that SSL encryption is disabled.

   > Description

   > If you need to connect to a Redis instance without using SSL, you must disable SSL encryption. For more information on how to connect to instance without using SSL, refer to [Connect to instance](https://docs.byteplus.com/en/docs/redis/connect-instance).

   **Update SSL certificate validity period**

After enabling SSL encryption, you can determine whether the current SSL certificate is within its validity period by checking **SSL certificate validity** status is **Valid**, and by checking the **SSL certificate validity period**. You can update the certificate validity by following these steps:

   1. Click **Renew certificate**.

   2. In the pop\-up dialog box, click **OK**.

   > **tip**

   * > The certificate is valid for 1 year, and you can update the certificate at any time. After updating, the certificate validity period will be extended by 1 year.

   * > We recommend that you promptly renew the SSL certificate's validity period before it expires, and re\-download and configure the CA certificate. Otherwise, client applications using encrypted connections will be unable to connect properly.

   **Modify minimum TLS version**

1. Click **the** ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) icon after TLS minimum version.

   2. In the pop\-up dialog box, select the target TLS version from the **TLS minimum version** dropdown list.

      Redis currently supports 3 TLS versions: **1.2**, 1.1, and **1.0**.

   **Download SSL CA certificate**

Click **Download CA certificate** to download the SSL CA certificate to a local device.

   The downloaded file is a ZIP compressed file containing the following three files:

      * `<Instance ID>_ca_certificate.p7b`: Used to import the CA certificate into Windows.

      * `<Instance ID>_ca_certificate.pem`: Used to import the CA certificate into other systems (such as Linux) or applications.

      * `<Instance ID>_ca_certificate.jks`: The truststore certificate storage file in Java, used to import the CA certificate into Java programs.

   > **tip**

   > After SSL encryption is enabled, you can download the SSL CA certificate to specify the SSL parameters and corresponding certificate for accessing Redis instances from the client. For specific procedures, refer to [Connecting to Redis from client via SSL encryption](https://docs.byteplus.com/en/docs/redis/connect-redis-from-client-via-ssl).
