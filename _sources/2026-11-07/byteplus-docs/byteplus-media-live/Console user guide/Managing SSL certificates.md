---
title: "Managing SSL certificates"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-certificates"
---

The added push\-pull domain name uses the HTTP protocol by default. If you want to achieve HTTPS encrypted transmission, you need to configure an SSL certificate for the domain name. MediaLive supports the certificate hosting feature. You need to upload the SSL certificate to the MediaLive console to achieve subsequent binding with the domain name.

<span id="67b2ec91"></span>
## Limitations

MediaLive supports uploading certificate files and certificate private key files of Nginx server type.

<span id="8c573f7b"></span>
## Adding SSL certificates


1. Download the PEM format SSL certificate file to your computer from the certificate service platform.

2. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

3. In the left\-side navigation pane, select **Settings** \> **Certificates** to enter the certificate list page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ba70f2ac8c4476688aa2ea51562caa5~tplv-goo7wpa0wc-image.image) </span>

4. Click **Add certificate** button to open the **Add HTTPS Certificate** dialog box, and follow the prompts to add the certificate.

   The parameters needed to be filled in are described in the table below:

   
   |**Parameters** |**Description** |
   |---|---|
   |Certificate name |Customize the certificate name without character type restrictions, and the maximum length is 40 characters. |
   |Select project |Select the project for the certificate, and after configuring the project, sub\-accounts with project permissions can manage the certificate. |
   |Upload method |Choose one way of adding.<br><br><br>* manual input<br><br>* file upload |
   |Certificate content |Certificate file content:<br><br><br>* When selecting manual upload, use text editor software to open the certificate file locally and copy the certificate content here.<br><br>* When selecting file upload, select the local certificate file to upload.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Automatic certificate chain completion is supported. You only need to upload the certificate issued for your domain name, and the certificate chain will be automatically completed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you choose to upload the certificate chain, it should be noted that the certificate chain includes the server certificate, intermediate certificate, and root certificate. They are in the correct order (the server certificate is in the front, and the intermediate certificate and root certificate are arranged in sequence). An incorrect order will make the certificate chain invalid.</div><br> |
   |private key |Certificate private key file content:<br><br><br>* When selecting manual upload, use the text editor software to open the certificate private key file locally and copy the certificate private key content here.<br><br>* When selecting file upload, select the local certificate private key file to upload.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Please ensure that the private key of the certificate is not set with password protection.</div><br> |
   

5. Click **Confirm** to save the certificate.


<span id="82892b1b"></span>
## Managing SSL certifications

On the **Certificates** page, you can perform the following operations on added certificates.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6939111c604049e19097063bce2601c5~tplv-goo7wpa0wc-image.image) </span>


|Operation |Description |
|---|---|
|Search for specific certificates |Filter certificates using the following conditions:<br><br><br>* Certificate status: Click different tabs to view certificates by their status. To ensure the HTTPS encryption transmission capability of the domain, you must update certificates that have expired or are about to expire in a timely manner.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02b6f7ae51b7482a9b75de171b3b4b85~tplv-goo7wpa0wc-image.image) </span><br><br>* Certificate name: Supports fuzzy search, case\-insensitive in English.<br><br>* Chain ID: Click the **Chain ID** text box, and enter the desired certificate chain ID in the pop\-up dialog box. You can enter up to 50 certificate chain IDs at a time, with each ID on a separate line. Case\-insensitive in English.<br><br>* Configurable domain name: Domains that can be bound to the current certificate. You can enter up to 1 domain at a time. Supports fuzzy search, case\-sensitive in English.<br><br>* Associated domain name: Domains that are currently bound to the certificate. Click the **Associated domain name** text box, and enter the desired associated domains in the pop\-up dialog box. You can enter up to 50 domains at a time, with each domain on a separate line. Case\-sensitive in English.<br><br>* Associated domain name status: Select one or more statuses of domains bound to the current certificate from the drop\-down list. When the domain status is **Online**, **Configuring**, **Offline**, or **ICP Filing missing**, you can update the certificate or bind another certificate for the domain.<br><br>* Search for projects: Select the certificate project from the **query item** drop\-down list.<br><br>* Certificate expiration time: Filter certificates that expire within a specific time range.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can get certificates of a certain status by clicking the corresponding tab. For other conditions, you must configure them and then click <strong>Search</strong> to get certificates that meet those conditions.</div><br> |
|View certificate information |View the certificate information.<br><br>Where,<br><br><br>* You can click the associated domain of the certificate to navigate to the HTTPS settings page of that domain.<br><br>* You can sort certificates by upload time and expiration time in either ascending or descending order. |
|Update certificate information |Click **Update** on the right side of the certificate to update certificate information. The updated certificate will only be effective for associated domains with statuses of **Online**, **Configuring**, **Offline**, or **ICP Filing missing**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To ensure the HTTPS encryption transmission capability of the domain, you must update certificates that have expired, are about to expire, or have changes in a timely manner.</div><br> |
|Delete certificate |If your certificate is no longer in use, click **Delete** on the right side of the certificate. |


<span id="a976fb30"></span>
## What's next

Bind an SSL certificate to the domain name and enable HTTPS. . Please refer to [HTTPS configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-https).

<span id="53a4af28"></span>
## FAQ

<span id="43d0f559"></span>
### Certificate chain order error

**Error**：There is an error in "The order of the certificate chain is wrong, please check the certificate and upload it again" when uploading the certificate.

**Reason**: This issue may be caused by your self\-splicing of the certificate chain. A certificate chain is composed of multiple certificates arranged in a certain order, and each preceding certificate is issued by the subsequent certificate. If the issuance relationship between the two preceding and subsequent certificates is not established, the certificate chain is invalid.

**Solution**: MediaLive certificate management supports automatic completion of the certificate chain. You only need to refer to the following method to obtain the certificate issued only for your domain name for upload, without submitting the entire certificate chain.

Suppose your original certificate chain contains three certificates, and its structure is as follows:

```Plain
-----BEGIN CERTIFICATE-----
Certificate A
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
Certificate B
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
Certificate C
-----END CERTIFICATE-----
```


You can use a certificate parsing tool to parse Certificate A, Certificate B, and Certificate C respectively to find the certificate issued to your domain name.

Suppose the certificate you found is Certificate A. Then, when uploading the certificate, you only need to enter the following content to successfully upload the certificate:

```Plain
-----BEGIN CERTIFICATE-----
Certificate A
-----END CERTIFICATE-----
```
