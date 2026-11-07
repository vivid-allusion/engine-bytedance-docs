---
title: "Upload certificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-upload-certificate"
---

To enable BytePlus CDN to handle your users' HTTPS requests, you need to upload your site's certificate. This guide shows you how to upload your certificate and private key files to the CDN console, assuming you have already exported them from your certificate provider.


1. In the left navigation bar of the BytePlus CDN management console, click **Security Center** \> **Certificate Center**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Certificates you upload to CDN are stored in the BytePlus Certificate Center. Therefore, you must authorize CDN to access the Certificate Center the first time you open this page. Click <strong>Authorize Access</strong>, and then click <strong>Authorize</strong> on the page that appears.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac8f6a3116124cada3832ed4d2971778~tplv-goo7wpa0wc-image.image" width="2012px" />   </div>
   

2. In the left navigation bar of the BytePlus CDN management console, click **Security Center** \> **Certificate Center** again.

3. On the **Certificate Center** page, click **Upload Certificate**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcc1289400a84913b9708d5fb26920b7~tplv-goo7wpa0wc-image.image) </span>

4. On the **Upload Certificate** page, set **Import Method** to **Upload Certificate Files**.

5. In the **Certificate File** and **Private Key File** fields, upload your certificate and private key files, respectively. Then, click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The certificate file has an extension of .crt or .pem, and its content starts with <code>-----BEGIN CERTIFICATE-----</code>.</div>


* <div data-tips="true" data-tips-type="tip">The private key file has an extension of .key or .pem, and its content starts with <code>-----BEGIN XXX PRIVATE KEY-----</code>.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57ccf9b2b92346cd8a805819a48b3e4a~tplv-goo7wpa0wc-image.image) </span>

On the **Certificate Center** page, the certificate you just uploaded will appear in the certificate list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/204622cceec348d69f716fe1bc0db9f9~tplv-goo7wpa0wc-image.image) </span>

Next, let's add your domain name to CDN.
