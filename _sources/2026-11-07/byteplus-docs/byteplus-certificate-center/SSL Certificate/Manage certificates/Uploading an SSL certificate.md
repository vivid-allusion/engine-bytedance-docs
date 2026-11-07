---
title: "Uploading an SSL certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-uploading-an-ssl-certificate"
---

If you already have an SSL certificate and want to apply it to your BytePlus cloud services or want to manage all SSL certificates (such as managing renewals), you can upload your SSL certificate to the BytePlus Certificate Center. This article describes how to upload an SSL certificate in the BytePlus Certificate Center console.

<span id="prerequisites"></span>
## Prerequisites


* Before uploading an SSL certificate, make sure you have the certificate files ready for upload. The certificate files include:

   * Certificate file in PEM encoding format. The file extension is `.crt` or `.pem`. The certificate file must include the complete certificate chain.

   * Private key file in PEM encoding format. The file extension is `.key` or `.pem`. The private key must not be password protected.

* The certificate uses RSA or ECC key algorithm.


<span id="operation-steps"></span>
## Operation steps


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, select **SSL Certificate** \> **Certificates**.

3. On the **Certificate management** page, click **Upload certificate**.

4. On the **Upload certificate** panel, complete the relevant configurations according to the [Configuration instructions](https://docs.byteplus.com/en/docs/29/8592#configuration-instructions), and then click **Upload**.


After the certificate is successfully uploaded, you can view the uploaded certificate on the **Certificate management** page.

<span id="configuration-instructions"></span>
## Configuration instructions


|Configuration item |Description |
|---|---|
|**Key algorithm** |Indicates the key algorithm supported by BytePlus certificate center. |
|**Upload method** |Select a upload method. Options:<br><br><br>* **Manual input**: Enter the certificate content for upload.<br><br>* **File upload**: Select the certificate file from your local computer for upload. |
|**Certificate file** |Specify the certificate file or the content of the certificate file. The certificate file must be in PEM encoding format with the file extension `.crt` or `.pem`, and it must include the complete certificate chain.<br><br><br>* If the **Upload method** is **Manual input**, you need to open the certificate file with a text editor, and then copy the file content to the **Certificate file** input box.<br><br>* If the **Upload method** is **File upload**, you can click the + icon to select the certificate file, or drag and drop the certificate file to the file upload area. |
|**Private key** |Specify the certificate private key file or the content of the private key file. The certificate private key file must be in PEM encoding format with the file extension `.key` or `.pem`. Additionally, the private key must not be password protected.<br><br><br>* If the **Upload method** is **Manual input**, you need to open the certificate private key file with a text editor, and then copy the file content to the **Private key** input box.<br><br>* If the **Upload method** is **File upload**, you can click the + icon to select the private key file, or drag and drop the private key file to the file upload area. |
|**Remark** |Set a remark for the certificate for future management. |
|**Allow uploading of duplicate certificates** |* When this setting is enabled, it allows you to upload certificates that are identical to the existing ones in the BytePlus Certificate Center.<br><br>* When this setting is disabled, the system prevents you from uploading certificates that are identical to the ones already present in the BytePlus Certificate Center. |
