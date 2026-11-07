---
title: "Certificate hosting"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificate-hosting"
---

Certificate hosting is an automated certificate management service provided by BytePlus Certificate Center. When you enable hosting for a certificate, BytePlus Certificate Center will automatically renew the certificate before it expires and deploy the newly\-issued certificate to BytePlus cloud services, replacing the old certificate that is about to expire. This article will guide you on how to enable hosting, disable hosting, and delete hosting tasks for a certificate.

<span id="background-information"></span>
## Background information

The certificate hosting service is based on DigiCert EE free certificates and DNS validation proxy. To enable hosting for a certificate, you need to configure a specified DNS CNAME record for your domain. As long as this record exists, BytePlus Certificate Center can complete the configuration required to verify domain ownership on your behalf.

Once you enable hosting for a certificate, BytePlus Certificate Center will automatically renew the certificate to ensure its continuous validity. If the certificate has been deployed to BytePlus cloud services (such as BytePlus CDN), BytePlus Certificate Center will also automatically replace the old certificate used on BytePlus cloud services.

The hosting service operates in cycles based on the certificate's validity period until you actively disable hosting.

<span id="usage-restrictions"></span>
### Usage restrictions


* Hosting can only be enabled for DigiCert EE certificates obtained through BytePlus Certificate Center.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">DigiCert EE free certificates can only be associated with a fully qualified domain name (FQDN).   </div>
   

* Currently, the certificate hosting service only supports automatic certificate replacement on BytePlus CDN.


<span id="enabling-hosting"></span>
## Enabling hosting

**Prerequisites**


* You have obtained a DigiCert EE certificate through BytePlus Certificate Center, and the certificate is in the "Issued" status.

* A certificate must have at least 30 days remaining before expiration in order to enable hosting.


**Steps**


1. Log in to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center/).

2. In the left navigation bar, click **Certificates**.

3. In the certificate list, find your certificate and click **Enable hosting** in the **Actions** column.

4. On the **Create a hosting task** page, you can configure the hosting task. First, locate the **Auto\-replace cert on** parameter and select the BytePlus services where you want the renewed certificate to be automatically replaced.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, <strong>BytePlus CDN</strong> is the only supported service.   </div>
   

5. Go to the the **Hosting method** area and review the CNAME record configuration requirements under the **DNS validation proxy** card.

6. Configure the DNS CNAME record for your domain as required.

   **Configuration example**

   Suppose you are enabling hosting for the domain `auto.example.com`. The **Hosting method** is **DNS validation proxy**. The following image shows the corresponding CNAME record configuration requirements. You need to create the specified DNS CNAME record for the domain.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a883a02d2de8cee7e54dc661acf7d4ca.png) </span>#{style="margin: 0"}#

   Next, using BytePlus DNS Suite as an example, here is how to configure the DNS CNAME record for the domain.

   1. Log in to the [BytePlus DNS Suite console](https://console.byteplus.com/dns-suite/dns).

   2. On the **Domain management** page, click your domain.

   3. On the **DNS records** tab, click **Create record set**.

   4. In the **Create record set** panel, configure the record as follows:

      * **Domain name**: Enter the domain name prefix from the CNAME record configuration requirements.

      * **Record type**: Select **CNAME**.

      * **Record value**: Enter the **Record value** from the CNAME record configuration requirements.

      Other parameters can remain as default.

      
      |Configuration requirements |Record configuration |
      |---|---|
      |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_eedf8f847dd7fef755419a2f930a19b2.png) </span>#{style="margin: 0"}# |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_be334159ad443deca30a22e47c5f480b.png) </span>#{style="margin: 0"}# |
      

   5. Click **Submit**.

7. Return to the **Create a hosting task** page, and click **Verify configuration** under the **DNS validation proxy** card. Wait for the verification to pass.

   You can enable hosting only if the CNAME record is successfully verified.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not modify the DNS CNAME record configured as required. Doing so will cause the hosting task to fail.   </div>
   

8. Confirm the **Runs periodically at** parameter. Its default value is **30 days before expiration**, which indicates that the automatic renewal and replacement of the certificate will begin 30 days prior to expiration.

9. In the **Remark** field, you can enter a custom name for the hosting task to help identify it. This is optional but recommended for easier task management.

10. After completing the above configurations, check the **Service agreement**, and then click **Create**.


After the hosting task is successfully created, a "Hosted" mark will appear next to the corresponding certificate ID. You can go to the **Hosting tasks** page to view the hosting tasks automatically created by the system.

<span id="disable-hosting"></span>
## Disable hosting

For enabled hosting tasks, you can disable them at any time to immediately end the task. Once the hosting task is disabled, BytePlus Certificate Center will no longer automatically renew and replace the certificate.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Disabled hosting tasks cannot be restored. To re\-host the certificate, you need to re\-enable hosting for the certificate.</div>


**Prerequisites**

You have a certificate hosting task in the **Enabled** status.

**Steps**


1. Log in to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center/).

2. In the left navigation bar, click **Hosting tasks**.

3. In the hosting task list, find your task and click **Disable** in the **Actions** column.

4. In the pop\-up dialog box, click **Disable**.


<span id="delete-hosting-tasks"></span>
## Delete hosting tasks

Disabled hosting tasks can be deleted from the console. After a hosting task is deleted, you will not be able to view the related records of the task.

**Prerequisites**

You have a certificate hosting task in the **Disabled** status.

**Steps**


1. Log in to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center/).

2. In the left navigation bar, click **Hosting tasks**.

3. In the hosting task list, find your task and click **Delete** in the **Actions** column.

4. In the pop\-up dialog box, click **Delete**.
