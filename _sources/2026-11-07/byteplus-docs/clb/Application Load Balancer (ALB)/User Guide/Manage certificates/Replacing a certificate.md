---
title: "Replacing a certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Replacing-a-certificate"
---

ALB provides you with the functionality to replace certificates in bulk. This topic describes how to replace certificates in the ALB console. After replacing an old certificate with a new one, the listeners associated with the new certificate will be displayed in the **Associated listener** column of the certificate list.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When your certificate is about to expire, ALB does not automatically select a non\-expired certificate to replace the existing one. To avoid service disruption due to certificate expiration, please manually replace your existing certificate before it expires.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have prepared a new certificate that is not expired. You can prepare the new certificate in the following two ways:

   * Method 1: Upload the certificate in the ALB console. For detailed steps, see [Adding a certificate](https://docs.byteplus.com/docs/clb/Adding-and-deleting-a-certificate#.5re75Yqg6K-B5Lmm).

   * Method 2: Upload or purchase the certificate in the Certificate Center console. For detailed steps, see [ALB using Certificates from the Certificate Center](https://docs.byteplus.com/docs/clb/Using-certificates-from-BytePlus-Certificate-Center).

* Only PEM format certificates are supported. For methods to convert other certificate formats to PEM format, see [Converting certificate format](https://docs.byteplus.com/docs/clb/Converting-certificate-formats).


<span id="928b7dc2"></span>
## Limits


* You can only replace certificates that are already associated with HTTPS listeners.

* Currently, you can only upload RSA or ECC certificates in the ALB console. Therefore, when you choose **Use an existing certificate on ALB**, you can only use RSA or ECC certificates to replace old certificates. RSA or ECC certificates can replace any type of certificate.

* The type of the new certificate must match the type of the certificate being replaced. You can only replace a server certificate with another server certificate, or a CA certificate with another CA certificate.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left\-side navigation pane, select **Certificate**.

3. Click **Replace** to the right of the target certificate.

4. Select the replacement method:

   * **Replace with an existing certificate**, see the table below to configure the relevant parameters.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |Replacement method |Select an existing certificate to replace. |Replace with an existing certificate |
      |Certificate source |Select the certificate source to replace:<br><br><br>* Use an existing certificate on the ALB<br><br>* Use BytePlus Certificate Center Certificate |Use BytePlus Certificate Center Certificate |
      |Select certificate |Select the certificate for replacement. |cert\-1hnf\*\*\*\* |
      

   * Upload and replace with a new certificate, see the table below to configure the relevant parameters.

      
      |Parameter |Explanation |Example |
      |---|---|---|
      |Areas |Specify the region where this certificate is located.<br><br><br>* The region for certificate upload must match your current region displayed at the top of the console. Certificates cannot be used across regions.<br><br>* If the same certificate is needed in two regions, you must upload the certificate information separately in each region. |China (Beijing） |
      |Name |Enter the certificate name. The specific format is as follows:<br><br><br>* Must start with an English letter or a Chinese character.<br><br>* Can only contain Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).<br><br>* Length must be 1 to 128 characters. |test\-new |
      |Description |Enter the certificate description. The specific format is as follows:<br><br><br>* Must start with an English letter or a Chinese character.<br><br>* Can only contain Chinese characters, letters, numbers, commas (,), periods (.), underscores (_), hyphens (\-), spaces, equal signs (=), full\-width commas (，), and full\-width periods (。).<br><br>* Length must be between 0 and 255 characters. |test\-new |
      |Certificate type |Specify the type of certificate. Currently supports Server Certificate and CA Certificate. Must match the type of the certificate being replaced. |Server certificate |
      |Public key certificate |Enter the content of the certificate public key. The public key must be encoded in PEM format. You can click **View sample** to see an example of the public key content. |PEM encoding of your public key certificate |
      |Private key certificate |Enter the content of the certificate's private key. The private key must be encoded in PEM format. You can click **View sample** to see an example of the private key content. |PEM encoding of your private key certificate |
      |Project |Select the project to which the certificate being uploaded belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/clb/Projects-Overview). |default |
      |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the add icon, enter the tag key and tag value to add tags to the certificate. |* Tag key: certificate\-key<br><br>* Tag value: certificate\-test |
      

5. Click **Save** to complete the action.
