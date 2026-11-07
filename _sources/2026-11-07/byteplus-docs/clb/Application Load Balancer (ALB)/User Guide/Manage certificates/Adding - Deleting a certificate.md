---
title: "Adding/Deleting a certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Adding-and-deleting-a-certificate"
---

If your service requires HTTPS encrypted data transmission, you need to bind a certificate to the listener when configuring the HTTPS listener.

## Add certificate

**Certificate Center console operation (recommended)**

For unified certificate management, we recommend uploading the certificates via the Certificate Center console.

**ALB console operation (not recommended)**

**Limits**

When adding a certificate in the ALB console, you can only add RSA or ECC certificates.

**Procedures**

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left navigation pane, select **Certificate**.

3. Click **Add certificate**.

4. To configure the related parameters, see the table below.

   |Parameter |Explanation |Example |
   |---|---|---|
   |Areas |Specify the region where this certificate is located.<br><br><br>* The region for certificate upload must match your current region displayed at the top of the console. Certificates cannot be used across regions.<br><br>* If the same certificate is needed in two regions, you must upload the certificate information separately in each region. |China (Beijing） |
   |Name |Enter the certificate name. The specific format is as follows:<br><br><br>* Must start with an English letter or a Chinese character.<br><br>* Can only contain Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).<br><br>* Length must be 1 to 128 characters. |Certificate\-X |
   |Description |Enter the certificate description. The specific format is as follows:<br><br><br>* Must start with an English letter or a Chinese character.<br><br>* Can only contain Chinese characters, letters, numbers, commas (,), periods (.), underscores (_), hyphens (\-), spaces, equal signs (=), full\-width commas (，), and full\-width periods (。).<br><br>* Length must be between 0 and 255 characters. |\-\- |
   |Certificate type |Specify the type of certificate. Currently supports Server Certificate and CA Certificate. |Server certificate |
   |Public key certificate |Enter the content of the certificate public key. The public key must be encoded in PEM format. You can click **View sample** to see an example of the public key content. |\-\- |
   |Private key certificate |Enter the content of the certificate's private key. The private key must be encoded in PEM format. You can click **View sample** to see an example of the private key content. |\-\- |
   |Project |Select a project for the certificate.<br><br>If you do not select a project, the certificate will be added to the **default** project by default. |default |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the add icon, enter the tag key and tag value to add tags to the certificate. |Certificate:test |

5. Click **Add** to complete the action.

## Delete certificate

### Prerequisites

The certificate is not associated with any listener.

> **tip**

> In the **Certificate management** page's certificate list, you can view all listeners associated with this certificate in the **Associated listener** column.

### Procedures

**Certificate Center Delete Operation**

If a certificate is uploaded to the Certificate Center, please go to the Certificate Center to delete.

**ALB Console Delete Operation**

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left navigation pane, select **Certificate**.

3. Click **Delete** next to the target certificate.

4. Click **Delete** to complete the action.
