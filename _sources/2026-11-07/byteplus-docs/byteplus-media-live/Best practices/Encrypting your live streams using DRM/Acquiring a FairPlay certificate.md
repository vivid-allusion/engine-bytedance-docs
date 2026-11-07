---
title: "Acquiring a FairPlay certificate"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-fairplay-certificate"
---

This topic introduces how to acquire a FairPlay streaming certificate from Apple. You need to upload the certificate to BytePlus MediaLive and Intertrust if you want to implement FairPlay encryption on your live streams.

<span id="9aa7496a"></span>
## Prerequisite

An [Apple Developer account](https://developer.apple.com/).

<span id="cd56ff31"></span>
## Procedure

<span id="79283f56"></span>
### Acquiring the PEM file


1. Visit Apple's [FairPlay Streaming](https://developer.apple.com/streaming/fps/) overview page and log in with your Apple developer account.

2. Navigate to the bottom of the page and click [Request FPS Deployment Package](https://developer.apple.com/contact/fps/).

3. Follow the instructions on the page to download the FPS deployment package and decompress it.

4. Follow the instructions in the package to create a private key file in .pem format and a Certificate Signing Request file in .csr format. Note down the private key used to generate the private key file.


<span id="c164d382"></span>
### Acquiring the ASK and certificate file


1. In the [Apple Developer Portal](https://developer.apple.com/), click **Certificates, ID & Profiles** in the left\-side navigation.

2. Click the + button.

3. Select **FairPlay Streaming Certificate**, and then click **Continue**.

4. Upload the CSR file you have obtained in the previous step. Once uploaded successfully, you will get an Application Secret Key (ASk).

5. Complete the instructions on the screen to generate the FairPlay certificate.

6. Download the Fairplay streaming certificate after it is issued.


<span id="1d180a9f"></span>
## What's next

Once you have acquired the FairPlay streaming certificate, you will need to upload the certificate to BytePlus MediaLive and Intertrust.

For detailed instructions about how to upload, refer to [Managing DRM licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-drm-licenses) and [Uploading a FairPlay certificate to Intertrust](https://docs.byteplus.com/docs/byteplus-media-live/docs-uploading-a-fairplay-certificate-to-intertrust).
