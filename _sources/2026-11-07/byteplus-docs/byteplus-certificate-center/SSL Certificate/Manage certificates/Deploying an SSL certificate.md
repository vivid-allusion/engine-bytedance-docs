---
title: "Deploying an SSL certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-deploy-certificate-to-byteplus-cdn"
---

This article describes how to deploy SSL certificates hosted in BytePlus Certificate Center to supported BytePlus cloud products and how to check the deployment status of SSL certificates.

<span id="background-information"></span>
## Background information

Some BytePlus cloud products require you to configure SSL certificates to implement specific features. For example, to enable HTTPS access for a domain name in BytePlus CDN, you must associate an SSL certificate with that domain name. SSL certificate deployment refers to distributing issued SSL certificates from BytePlus Certificate Center to supported BytePlus cloud products for use.

> Example:

> Suppose you have configured the domain name `www.example.com` in BytePlus CDN, and you have a certificate in BytePlus Certificate Center issued for `www.example.com` or `*.example.com`. By deploying this certificate to CDN, you can associate it with the domain name `www.example.com` to enable HTTPS access for the domain.


<span id="supported-cloud-products"></span>
### Supported cloud products

Some BytePlus cloud products support certificate deployment, meaning you can deploy SSL certificates from BytePlus Certificate Center to these cloud products or check the deployment status of SSL certificates on these products. See the following table for details.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To apply certificates to other BytePlus cloud products not listed here, you can first download the certificate from BytePlus Certificate Center and then configure it in the respective cloud product console.</div>



|Supported cloud product |Deploy certificate (from BytePlus Certificate Center) |Check certificate deployment status (in BytePlus Certificate Center) |
|---|---|---|
|BytePlus CDN |Supported<br><br>For specific operations, see [Deploy certificate to cloud products](https://docs.byteplus.com/en/docs/29/8593#deploy-certificate-to-cloud-products). |Supported<br><br>For specific operations, see [View certificate deployment status](https://docs.byteplus.com/en/docs/29/8593#view-certificate-deployment-status). |
|Application Load Balancer (ALB) |||
|Classic Load Balancer (CLB) |||
|BytePlus VOD |Not supported<br><br>Currently, you can only configure certificates in the [BytePlus VOD](https://console.byteplus.com/vodpaas) console. For detailed instructions, refer to the [BytePlus VOD product documentation](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-ssl-certificates). ||


<span id="deploy-certificate-to-cloud-products"></span>
## Deploy certificate to cloud products

<span id="prerequisites"></span>
### Prerequisites

Your certificate is hosted in BytePlus Certificate Center (purchased from or uploaded to BytePlus Certificate Center) and meets the following conditions:


* The certificate is issued, not expired, and not revoked.

* The certificate uses RSA or ECC as the key algorithm.


<span id="steps"></span>
### Steps


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center/ssl/certificate).

2. In the left navigation pane, choose **SSL Certificates** \> **Certificates**.

3. In the certificate list, find the certificate you want to deploy and click **Deploy** in the **Actions** column.

4. On the **Deploy certificate** page, locate the **Deploy to** area, and select a cloud product from the **BytePlus service** dropdown list.

5. Complete the service access authorization.

   When you deploy a certificate to a new cloud product for the first time, you must complete service access authorization. This authorizes BytePlus Certificate Center to access your resources in the cloud product to obtain a list of resources applicable to the certificate.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Service access authorization only needs to be performed once for each cloud product. If you have already completed the authorization, you can skip this step.   </div>
   

   1. In the **Deploy to** area, click **Authorize now**.

   2. On the **Service access request** page, click **Authorize**.

      After successful authorization, the authorization page will automatically close. You will return to the **Deploy certificate** page.

6. In the **All resources** list, select one or more resources to use the current certificate and add them to the **Selected resources** list on the right.

   BytePlus Certificate Center automatically retrieves resources applicable to the current certificate from the cloud product you selected. For the specific conditions that resources need to meet, see [Description of certificate-applicable resources](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-deploy-certificate-to-byteplus-cdn?lang=en#gmzMVI1X).

   * **Bind certificate**: If a resource is not bound to any certificate, the deployment operation will bind the current certificate to it.

   * **Update certificate**: If a resource is already bound to another certificate, the deployment operation will replace the original certificate with the current one. Please proceed with caution.

   * **No deployment needed**: If a resource is already bound to the current certificate, there is no need to deploy it again.

7. Click **Deploy**.

8. In the **Deployment confirmation** dialog box, verify the resources to be deployed. Once confirmed, click **Confirm and deploy**.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260410060144-1494435737764.webp) </span>

   The dialog box will display the deployment progress and results. It is recommended that you wait for the deployment to complete before closing the dialog box.

   * Deploying:

      <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260511080102-711920245818.webp) </span>

   * Succeeded:

      <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260410060843-1584015127126.webp) </span>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If the deployment takes a long time to complete, you can submit a ticket to contact us for assistance.</div>


* <div data-tips="true" data-tips-type="default">If you close the dialog box before the deployment is finished, you can return to the <strong>All resources</strong> list to check the deployment result.</div>


* <div data-tips="true" data-tips-type="default">After a successful deployment, we recommend that you go to the corresponding cloud product console to double\-check the result.</div>



<span id="gmzMVI1X"></span>
### Description of certificate\-applicable resources

The following table describes the resources included in the **All resources** list and the conditions they must meet to appear in the list.


|Cloud product |Corresponding resource |Conditions to appear in the "All resources" list |Related information for configuring resources in cloud products |
|---|---|---|---|
|BytePlus CDN |Domain name |* **Status** is **Enabled** or **Deploying**<br><br>* Can be protected by the certificate |[Add your domain name](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-add-your-domain-name) |
|Application Load Balancer (ALB) |Listener |**Listener protocol** is **HTTPS** |[Create an HTTPS listener](https://docs.byteplus.com/en/docs/clb/ALB-Creating-an-HTTPS-listener) |
|Classic Load Balancer (CLB) |Listener |**Listener protocol** is **HTTPS** |[Create an HTTPS listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener) |


<span id="view-certificate-deployment-status"></span>
## View certificate deployment status

You can view the deployment status of certificates on the [Certificates](https://console.byteplus.com/certificate-center/ssl/certificate) page. The **Used by** column in the certificate list shows the cloud product to which the certificate is deployed and the number of resources associated with the certificate in the cloud product.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d643000353be91ad26fb24b994778a64.png) </span>
