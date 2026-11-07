---
title: "Upload certificates"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-upload-certificates-certfiicate-center"
---

To use a certificate purchased from another provider with BytePlus CDN, you need to upload it to the **Certificate Center**.

This guide provides step\-by\-step instructions for uploading your certificate, either by pasting its content or by uploading the public and private key files.

<span id="steps"></span>
## Steps


1. On the **Certificate Center** page, click **Upload Certificate**.

2. On the **Upload Certificate** page, refer to the [Configuration Instructions](https://docs.byteplus.com/en/docs/18/6607#configuration-instructions) for settings, then click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3288a715444a44f48a67ba9aa04486cc~tplv-goo7wpa0wc-image.image) </span>

<span id="configuration-instructions"></span>
### Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Import Method |The method for uploading the certificate. The configuration has the following options:<br><br><br>* **Paste Certificate Content**: Indicates pasting the content of the certificate file and private key file.<br><br>* **Upload Certificate Files**: Indicates uploading the certificate file and private key file. |
|Public Key |The certificate file. The certificate file must contain a complete certificate chain, with an extension of .crt or .pem, and the content begins with `-----BEGIN CERTIFICATE-----`.<br><br><br>* If **Import Method** is set to **Paste Certificate Content**, paste the content of the certificate file into the **Public Key** input box.<br><br>* If **Import Method** is set to **Upload Certificate Files**, upload the public key file. |
|Private Key |Indicates the private key file of the certificate. The private key file has an extension of .key or .pem, and the content begins with `-----BEGIN XXX PRIVATE KEY-----`.<br><br><br>* If **Import Method** is set to **Paste Certificate Content**, paste the content of the private key file into the **Private Key** input box.<br><br>* If **Import Method** is set to **Upload Certificate Files**, upload the private key file. |
|Description |Optional. Enter remarks to help you identify the certificate. |
