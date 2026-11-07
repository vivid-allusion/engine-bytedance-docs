---
title: "Upload certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Uploading-a-certificate"
---

This article introduces how to upload certificates.

## Prerequisites

* Please ensure the certificate is valid and not expired.

* Confirm that the domain name added in the Configuration forwarding rules exists in the certificate. Otherwise, an SSL connection cannot be established, causing the listener to fail to forward requests correctly.

* Wildcard domain certificates are supported, but note the wildcard rules. For example, if the wildcard domain certificate is `*.support.com`, it supports `a.support.com`, `b.support.com`, etc., but does not support `a.a.support.com`. To support that, apply for a `*.a.support.com` wildcard domain certificate.

## Procedures

### **Certificate Center operation (recommended)**

For unified certificate management, we recommend uploading the certificates via the Certificate Center console. For specific steps, please refer to Uploading a certificate.

### **CLB console action (not recommended)**

1. Log in to the CLB console.

2. In the left\-side navigation pane, select Certificate.

3. Click Upload server certificate.

4. Configure the following parameters.

   |**Parameter** |**Explanation** |**Value** |
   |---|---|---|
   |**Basic information** |||
   |Regions |The certificate’s region. Uploaded certificates can only be used for resources in this region and cannot be migrated. |China (Beijing） |
   |Name |Set the certificate name. |certificate\-01 |
   |**Certificate information** |||
   |Certificate type |Only server certificates are supported for upload. |Server certificate |
   |Public key certificate |Please upload the certificate in PEM format. If your certificate is in another format, please refer to the Conversion of certificate format. |PEM encoding of your public key certificate |
   |Private key certificate |Please upload the certificate encoded in PEM format. If your certificate is in another format, please refer to the Conversion of certificate format. |PEM encoding of your private key certificate |
   |**More information** |||
   |Affiliated Project |Select the project to which the certificate being uploaded belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/clb/Project-management). |default |
   |**Advanced option** |||
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the add icon, enter the tag key and tag value to add tags to the certificate. |* Tag key: certificate\-key<br><br>* Tag value: certificate\-test |

5. Click **Migrate** to complete the action.

## Related documents

[UploadCertificate](https://docs.byteplus.com/en/docs/clb/UploadCertificate)
