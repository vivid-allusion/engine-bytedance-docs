---
title: "Managing HTTPS certificates"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-https-certificates"
---

This article introduces the operations related to HTTPS certificates after binding a custom domain name, including binding certificates, replacing certificates, and unbinding certificates.

<span id="15aee58b"></span>
## Prerequisite

The domain name has been bound and the domain name has been filed. For specific steps, please refer to [Setting up a custom domain](https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name).

<span id="21d2775f"></span>
## Certificate status overview


|**Certificate status** |**Description** |
|---|---|
|Unbound |Unbound HTTPS certificate. |
|Bound |The HTTPS certificate has been bound, and the custom domain name can be accessed using HTTPS. |
|Expired |The bound HTTPS certificate has expired.You can rebind after purchasing or uploading a new certificate in the [Certificate Center](https://console.byteplus.com/certificate-center/ssl/overview). |
|Deleted |The bound HTTPS certificate has been deleted. |
|Cross\-service authorization failed |The role of cross\-service authorization is removed, and TOS cannot access the Certificate Center. If you want normal use, you need to re\-authorize across services. |
|Status unknown |Unable to confirm the status of the HTTPS certificate. |


<span id="cdf758a4"></span>
## Bind certificate

If you need to use HTTPS to access your bound custom domain name, you can bind an HTTPS certificate to the custom domain name. This section describes the steps to bind a certificate.

<span id="f1263fc7"></span>
### Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane,click **Domain name and transfer acceleration** \> **Custom domain**.

4. On the **Custom domain** page, click on the **Associate certificate** to the target domain in the **Actions** column.

5. In the dialog box that pops up, select the certificate you want to bind and click **Associate**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When binding the certificate, you need to authorize TOS to access the Certificate Center service. You can click <strong>Click to</strong> <strong>Authorize</strong> after <strong>Service authorization</strong> in the dialog box to complete the cross\-service authorization; if you have authorized before, there is no need to re\-authorize.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only support binding certificates that are issued, not expired, and not revoked.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Make sure that the certificate you bind is within a valid period.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you don't have a certificate available, you can go to the <a href="https://console.byteplus.com/certificate-center/ssl/overview.">Certificate Center</a> and purchase or upload a certificate.   </div>
   


<span id="99959527"></span>
## Replace certificate

If the certificate you are binding is not in the valid period, or you need to replace the certificate for a custom domain name, you can choose to replace the certificate. This section describes the steps to replace the certificate.

<span id="aa53c20e"></span>
### Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane,click **Domain name and transfer acceleration** \> **Custom domain**.

4. On the **Custom domain** page, click on the **Replace certificate** to the target domain in the **Actions** column.

5. In the dialog box that pops up, select the certificate you want to replace and click ok.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you don't have a certificate available, you can go to the <a href="https://console.byteplus.com/certificate-center/ssl/overview.">Certificate Center</a> and purchase or upload a certificate.   </div>
   

<span id="e99e708d"></span>
## Unbind certificate

If you no longer need to use HTTPS to access your custom domain name, you can unbind the certificate. This section describes the steps to unbind a certificate.

<span id="af936f19"></span>
### Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane,click **Domain name and transfer acceleration** \> **Custom domain**.

4. On the **Custom domain** page, click on the **Disassociate certificate** to the target domain in the **Actions** column.

5. In the dialog box that pops up, select the certificate you want to unbind and click **Disassociate**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After unbinding the SSL certificate of the custom domain name, the domain name will not be accessible using the HTTPS protocol. Please proceed with caution.   </div>
