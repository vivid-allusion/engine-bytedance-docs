---
title: "Getting a FairPlay certificate from Apple"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-fairplay-certificate"
---

This topic introduces how to get a FairPlay streaming certificate from Apple. You need to upload the certificate to BytePlus VOD and Intertrust if you want to implement FairPlay encryption on your live streams.

<span id="6b996089"></span>
## Prerequisite

An [Apple Developer account](https://developer.apple.com/).

<span id="c9a1dca0"></span>
## Procedure

<span id="5e330b38"></span>
### Acquiring the PEM file


1. Visit Apple's [FairPlay Streaming](https://developer.apple.com/streaming/fps/) overview page and log in with your Apple developer account.

2. Navigate to the bottom of the page and click [Request FPS Deployment Package](https://developer.apple.com/contact/fps/).

3. Follow the instructions on the page to download the FPS deployment package and decompress it.

4. Follow the instructions in the package to create a private key file in .pem format and a Certificate Signing Request file in .csr format. Make a note of the private key used to generate the private key file.


<span id="8ee81846"></span>
### Acquiring the ASK and certificate file


1. In the [Apple Developer Portal](https://developer.apple.com/), click **Certificates, ID & Profiles** in the left\-side navigation.

2. Click the + button.

3. Select **FairPlay Streaming Certificate**, and then click **Continue**.

4. Upload the CSR file you have obtained in the previous step. Once uploaded successfully, you will get an Application Secret Key (ASK).

5. Complete the instructions on the screen to generate the FairPlay certificate.

6. Download the FairPlay streaming certificate after it is issued.


<span id="46b74466"></span>
## What's next

Once you have acquired the FairPlay streaming certificate, you will need to upload the certificate to BytePlus VOD and Intertrust. For detailed instructions about how to upload, refer to [DRM licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-licenses) and [Uploading a FairPlay certificate to Intertrust](https://docs.byteplus.com/docs/byteplus-vod/docs-uploading-fairplay-certificate-to-intertrust).
