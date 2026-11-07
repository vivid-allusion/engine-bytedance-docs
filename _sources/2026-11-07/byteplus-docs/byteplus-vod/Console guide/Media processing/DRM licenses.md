---
title: "DRM licenses"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-drm-licenses"
---

BytePlus VOD supports Google Widevine, Apple FairPlay, and Microsoft PlayReady DRM encryption. To enable Widevine and PlayReady, simply add the API key. However, for FairPlay, in addition to the API key, you also need to provide a certificate. This article introduces how to upload the DRM key and FairPlay certificate to the BytePlus VOD console.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">DRM encryption is currently in MVP testing. If you have specific requirements related to this feature, please reach out to your <a href="https://www.byteplus.com/en/contact">sales representative</a> for further assistance.</div>


<span id="9f5143e8"></span>
## Uploading the DRM key

<span id="dc8970e3"></span>
### Prerequisites

You must first acquire a DRM key from [Intertrust](https://portal.expressplay.com/). For detailed instructions on getting the key, please refer to [Getting a DRM key from Intertrust](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-drm-key).

<span id="cb9b4d1d"></span>
### Procedure


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar and enter a specific space.

3. Click **Media processing** \> **DRM licenses**.

4. Click **Add API key**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f83e3fdb3464655897cfaeea664c108~tplv-goo7wpa0wc-image.image) </span>

5. In the dialog box that appears, fill in the key.

6. Click **Confirm** to save the settings.


<span id="b9866821"></span>
## Uploading the FairPlay certificate

To enable encryption on Apple devices, you must also upload a FairPlay certificate.

<span id="0fd350ee"></span>
### Prerequisites

You must have a FairPlay certificate. For instructions on acquiring the certificate and other related information, please refer to [Getting a FairPlay certificate from Apple](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-fairplay-certificate).

<span id="a7e435cc"></span>
### Procedure


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar and enter a specific space.

3. Click **Media processing** \> **DRM licenses**.

4. Click the **Certificate** tab.

5. Click **Add certificate**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1be5f251d9d64773891099dc8908f237~tplv-goo7wpa0wc-image.image) </span>

6. In the dialog box that appears, configure the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |Certificate name |The name of your FairPlay certificate. |
   |Certificate file |Upload a `.cer` file. |
   |Private key file |Upload a `.pem` file. |
   |Private key |The key that is used to decrypt the private key file. |
   |ASK |The Application Secret Key (ASK) provided by Apple when applying for the certificate |
   

7. Click **Confirm** to save the settings.
