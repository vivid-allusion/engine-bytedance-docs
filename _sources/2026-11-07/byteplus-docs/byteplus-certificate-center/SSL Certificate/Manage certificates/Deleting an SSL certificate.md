---
title: "Deleting an SSL certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-deleting-an-ssl-certificate"
---

For SSL certificates that are no longer needed or cannot be used, you can delete them in the BytePlus Certificate Center console. Once you delete an SSL certificate, BytePlus Certificate Center will no longer retain the record of the corresponding certificate.

<span id="conditions-for-deleting-certificates"></span>
## Conditions for deleting certificates


|Certificate type |Conditions for deletion |
|---|---|
|Certificates ordered through BytePlus Certificate Center |* Not associated with other certificates<br><br>* Not used by cloud resources<br><br>* Order cancelled, request failed, or certificate expired/revoked |
|Certificates uploaded to BytePlus Certificate Center |Not used by cloud resources |


<span id="check-methods"></span>
### Check methods


* Check if the certificate is associated with other certificates:

   Open the certificate details and check the **Related cert** in the **Basic information** section. If it shows `-`, it means the certificate is not associated with other certificates; if it shows **View related cert**, it means the certificate is associated with other certificates.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c45cdd4e497ac87e01117423ce458173.png) </span>#{style="margin: 0"}#

* Check if the certificate is used by cloud resources:

   In the certificate list, check the content of the **Used by** column. If it shows `-`, it means the certificate is not used by cloud resources; if it shows other content, it means the certificate is used by cloud resources.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9a4f350499debfca6ecc87d50de0a093.png) </span>#{style="margin: 0"}#

* Check the status of the certificate:

   In the certificate list, check the **Status** and **Validity period** columns:

   * If **Status** is **Cancelled**, it means that the certificate order has been cancelled.

   * If **Status** is **Rejected**, it means that the certificate request has failed.

   * If **Validity period** includes **Expired**, it means that the certificate has expired.

   * If **Validity period** includes **Revoked**, it means that the certificate has been revoked by the CA.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6ba8f3dba0b562693bb5bfe1bb788691.png) </span>#{style="margin: 0"}#


<span id="precautions-before-operation"></span>
## Precautions before operation

Once a certificate is deleted, it cannot be recovered. Please proceed with caution.

<span id="operation-steps"></span>
## Operation steps


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, select **SSL Certificates** \> **Certificates**.

3. In the certificate list, find your certificate and click **Delete** in the **Actions** column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Delete</strong> button only appears when the certificate meets the conditions for deletion.   </div>
   

4. Confirm that the current certificate is not being used by any servers or BytePlus cloud services.

5. In the pop\-up dialog box, select **Confirm** and then click **Delete**.
