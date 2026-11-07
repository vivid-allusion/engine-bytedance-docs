---
title: "ALB uses certificates from the Certificate Center"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Using-certificates-from-BytePlus-Certificate-Center"
---

ALB is integrated with the [BytePlus Certificate Center](https://docs.byteplus.com/en/docs/6638/1051811). The Certificate Center is a full lifecycle management platform for digital certificates. You can purchase, upload, and manage certificates all in one place in the [Certificate Center console](https://console.byteplus.com/certificate-center/ssl/overview). The services provided by the Certificate Center include [SSL certificates](https://docs.byteplus.com/docs/6638/93503) In ALB, SSL certificates are mainly used for HTTPS one\-way authentication.

To use certificates from the Certificate Center on the ALB side, you need to:


1. Prepare the certificate in the Certificate Center.

2. Select the certificate from the Certificate Center on the ALB side.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When ALB uses certificates from the Certificate Center, you must manage the certificates in the Certificate Center.</div>


<span id="ece800e8"></span>
## Prepare the certificate in the Certificate Center

<span id="9bf00453"></span>
### SSL certificate

You can purchase SSL certificates in the Certificate Center or upload SSL certificates obtained from other platforms to the Certificate Center for unified management. You can follow the flowchart below to complete certificate purchase, application, and usage.

<span id="23d86c47"></span>
#### Purchase certificate

Refer to [creating an SSL certificate order](https://docs.byteplus.com/docs/6638/118034) and [submitting an SSL certificate request](https://docs.byteplus.com/docs/6638/118035) to purchase certificates.

<span id="28121a3e"></span>
#### Upload certificate

Refer to [uploading an SSL certificate](https://docs.byteplus.com/docs/6638/118039) to upload your certificate in the Certificate Center.

<span id="fa0a5c5c"></span>
## select certificate on ALB side

after preparing certificates in the certificate center, you can select them on the ALB side.

you need to select a server certificate when performing the following operations:


* [create HTTPS listener](https://docs.byteplus.com/docs/clb/ALB-Creating-an-HTTPS-listener)

* [create HTTP/2 listener](https://docs.byteplus.com/docs/clb/Creating-an-HTTP_2listener)

* [create QUIC listener](https://docs.byteplus.com/docs/clb/Creating-a-QUIC-listener)

* [Configure multiple certificates for HTTPS listener (Basic edition)](https://docs.byteplus.com/docs/clb/Configuring-SNI-for-an-HTTPS-listener), [configure multiple certificates for HTTPS listener (Standard edition)](https://docs.byteplus.com/docs/clb/Configuring-SNI-for-an-HTTPS-listener_Standard-edition)


You need to select a CA certificate when performing the following operations:


* [Mutual authentication](https://docs.byteplus.com/docs/clb/Mutual-authentication)


<span id="00a27b5f"></span>
## Manage certificates in the Certificate Center

When ALB uses certificates from the Certificate Center, you must manage the certificates in the Certificate Center. For example, in the Certificate Center, you can view the listeners associated with a certificate, check the certificate’s expiration time, and renew certificates.

After renewing a certificate, you need to manually associate the new certificate with the listener. For related operations, refer to [Replace certificate](https://docs.byteplus.com/docs/clb/Replacing-a-certificate).
