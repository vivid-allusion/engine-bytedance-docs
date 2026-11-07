---
title: "Managing DRM licenses"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-drm-licenses"
---

This article introduces how to upload the DRM key and FairPlay certificate to BytePlus MediaLive.

<span id="8aa0da77"></span>
## Uploading the DRM key

<span id="24fcd147"></span>
### Prerequisites

You must first acquire a DRM key from [Intertrust](https://portal.expressplay.com/). For detailed instructions on obtaining the key, please refer to [Acquiring a DRM key](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-drm-key).

<span id="bf440097"></span>
### Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Encryption**.

3. Click the **DRM** tab.

4. Click **Edit** in the **API key information** configuration area. A dialog box will appear.

5. Fill in the key.

6. Click **Confirm** to save the settings.


<span id="28aa3894"></span>
## Uploading a FairPlay certificate

To enable encryption on Apple devices, you must also upload a FairPlay certificate.

<span id="c7f3874e"></span>
### Prerequisites

A FairPlay certificate. For instructions on acquiring the certificate and other related information, please refer to [Acquiring a FairPlay certificate](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-fairplay-certificate).

<span id="ad2418f7"></span>
### Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Encryption**.

3. Click the **DRM** tab.

4. Click **Edit** in the **Certificate** configuration area. A dialog box will appear.

5. Configure the relevant settings.



|**Parameters** |**Description** |
|---|---|
|Certificate name |The name of your FairPlay certificate. |
|Certificate file |Upload a .cer file. |
|Private key file |Upload a .pem file. |
|Private key |The key that is used to decrypt the private key file. |
|ASK |The Application Secret Key (ASK) provided by Apple when applying for the certificate |



6. Click **Confirm** to save the settings.


<span id="54d8c93d"></span>
## What's next

Configure in the BytePlus MediaLive console which domain names and AppNames you want to encrypt. You can refer to [Managing encryption configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-a-drm-encryption-task) for detailed instructions on how to complete the configurations.
