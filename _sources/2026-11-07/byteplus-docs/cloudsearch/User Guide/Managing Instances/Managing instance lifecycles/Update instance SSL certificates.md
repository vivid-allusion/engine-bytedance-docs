---
title: "Update instance SSL certificates"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Update_instance_SSL_certificates"
---

Cloud Search service instances enable SSL certificates by default, providing encrypted transmission capabilities for HTTP and Transport layers. SSL certificates have a validity period; once expired, clients cannot establish secure connections normally, potentially causing business interruptions. To avoid business impact from expired certificates, the system sends reminders before expiration, allowing you to update the instance SSL certificate promptly according to the notice. This topic describes how to update the instance SSL certificate.

<span id="OmHhaHSA"></span>
## Precautions


* If the client accesses the instance using TransportClient, you must first add the new root certificate to the client’s trust list and replace the client certificate; otherwise, client connections may be interrupted after the certificate update. For details, [submit a ticket](https://console.byteplus.com/workorder/create?step=1&SubProductID=P00000255) for consultation.

* If the client accesses the instance using RESTful API and has enabled SSL certificate verification, you need to add the new root certificate to the client’s trust list in advance; otherwise, client connections may be interrupted after the certificate update. For details, [submit a ticket](https://console.byteplus.com/workorder/create?step=1&SubProductID=P00000255) for consultation.

* After SSL certificate expiration, communication between internal nodes of the instance will fail, causing the instance to become unavailable. If the instance has HTTPS enabled and the client enables certificate verification, the client and instance will also fail to establish a connection due to certificate expiration.

* During the update, the system will perform a rolling restart on the cluster nodes. For 6.x instances or instances where HTTPS is disabled, the certificate update requires two complete rolling node upgrades. For later\-version instances with HTTPS enabled, only one rolling node upgrade is required. We recommend that you perform actions during off\-peak hours.


<span id="TSvgvYl7"></span>
## Procedure

When an instance's SSL certificate is about to expire, a certificate expiration reminder appears at the top of the Instances page.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Click **View details** in the note message at the top of the page.

4. In the **Certificate expiration details** panel, view the affected instances and expiration time, then click **Update certificate** to the right of the target instance.

5. In the pop\-up dialog, review the precautions, check **I acknowledge the above risks and confirm to execute the certificate update**, then click **Confirm update**.

   After the system issues the update task, you can click **Task center** on the right side of the target instance to check the progress.
