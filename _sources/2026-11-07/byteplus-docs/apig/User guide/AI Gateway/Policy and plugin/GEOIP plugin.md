---
title: "GEOIP plugin"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/GEOIP_plugin"
---

The GEOIP Plugin supports obtaining the user's country code based on the user's source IP address and adding it to the Header for use in subsequent business processes. This article describes how to create a GEOIP plugin.

<span id="2s3F324e"></span>
## Background information

The GEOIP plugin is a tool that can determine a user's geographic location based on their IP address. It is based on IP geolocation technology. By querying the IP geolocation database, it maps IP addresses to country, city, latitude and longitude, and other geographic information.

<span id="kIarxzgS"></span>
## Prerequisites


* The APIG instance has been created. For details about the actions, please refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The fixed domain name type Upstream has been created. For details about the actions, refer to [Create fixed domain name Upstream](https://docs.byteplus.com/en/docs/apig/Fixed_IP_type_Upstream). The domain name must be the TOS domain name of the bucket where the IP geolocation database file is located; HTTPS protocol must be enabled; and the domain name must be configured to use SNI.

* The storage bucket has been created. For details on operations, refer to [Create bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* The MaxMind IP geolocation database has been uploaded to storage. For details on the operation, refer to [Upload file](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

* The AccessKey (AK) and SecretKey (SK) of this account have been obtained. Obtain AK SK in  ** ** [Access control](https://console.byteplus.com/iam/identitymanage/user) ** \> API access key**.


<span id="qJo3K115"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In **Instance Management**, select the target instance.

3. In the left navigation bar, click **Plugin Center ** \> ** GEOIP Plugin** \> **Create Plugin**.

4. Configure plugin rules.

   
   |Parameter |Description |
   |---|---|
   |Take effect level |Select the activation level of the plugin, including:<br><br><br>* **Instance level**: The plugin takes effect within an instance. Specify the target instance where it will take effect.<br><br>* **Service level**: The plugin takes effect within the service, and you need to specify the target instance and service where the plugin takes effect.<br><br>* **Route level**: The plugin takes effect within the route. You need to specify the target instance, service, and route for which the plugin takes effect. |
   |Service |Select the service to which the plugin belongs. |
   |Associated route |Select the route associated with the plugin. |
   |IP acquisition method |Support the following methods for obtaining IP addresses.<br><br><br>* **Based on X\-Forward\-For**: Obtain the client IP from the HTTP header, including proxy layer IPs, which requires trusted proxy configuration.<br><br>* **Obtain via custom Header**: The header name must be agreed upon between both parties, which is flexible but depends on both parties' conventions.<br><br>* **Obtain source IP via TCP connection**: The source IP is obtained directly from the TCP connection, making it difficult to tamper with and highly accurate. This method is suitable for scenarios without a proxy. |
   |TOS configuration |Enter the configuration information of the TOS where the IP address database is located.<br><br><br>* AKSK configuration: Enter your account's AccessKey (AK) and SecretKey (SK).<br><br>* Bucket: Choose the TOS storage bucket of the IP address database.<br><br>* Object: Enter the file name of the IP address database in the storage bucket.<br><br>* Timeout: Set the timeout duration for downloading the database. If the timeout is exceeded, the download will fail. If the download fails, the plugin will trigger a re\-download every 3600 seconds after it is enabled.<br><br>* Upstream: Choose the fixed domain name "Upstream" that has already been created. |
   

4. Click **Confirm**.


<span id="11Nb0lFE"></span>
##
