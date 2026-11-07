---
title: "Demonstrating control over domain"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-conducting-domain-validation"
---

After submitting the certificate request, you must complete the domain validation according to the requirements of the CA to prove that you own the corresponding domain. This article introduces the relevant operations of domain validation.

<span id="domain-validation-methods"></span>
## Domain validation methods

When submitting a certificate request, you need to select a domain validation method. The available validation methods are shown in the following table.


|Validation method |Applicable domain types |Description |
|---|---|---|
|DNS validation |* Single domain (FQDN)<br><br>* Wildcard domain |This method requires you to log in to your DNS service provider's system and create a DNS TXT/CNAME record for the domain. The CA periodically checks if the specified record exists. When the CA confirms the existence of the specified record, the DNS validation will be completed. |
|File validation |* FQDN/IP |This method requires you to add the specified validation file to the designated path on the web server. The CA periodically checks if the specified file can be accessed. When the CA confirms that the specified file can be accessed, the file validation will be completed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Before selecting this method, you must ensure that the address (domain or IP) of the web server can be accessed via the internet.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The CA only supports sending validation requests to port 80 or 443. Before selecting this method, please ensure that your web server has opened port 80 or 443.</div><br> |


<span id="prerequisites"></span>
## Prerequisites

You have submitted an SSL certificate request. For related operations, please refer to [Requesting an SSL certificate](https://docs.byteplus.com/en/byteplus-certificate-center/docs/requesting-a-certificate).

<span id="operation-steps"></span>
## Operation steps


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. On the left navigation bar, select **SSL Certificate** \> **Certificates**.

3. In the certificate list, find your certificate and click the certificate ID.

   The **Status** of the certificate is **Validating**.

4. In the **Order progress** section, find the **Pending domain validation** part and view the domain validation requirements.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the current progress is <strong>CA processing</strong>, it means that your certificate request has just been submitted to the CA and the corresponding domain validation requirements have not been returned by the CA. Please wait for about 5 minutes, and the <strong>Pending domain validation</strong> part will appear.   </div>
   

5. Complete the relevant configuration according to the domain validation requirements.

   * [DNS validation instructions](https://docs.byteplus.com/en/docs/29/8586#6965ced8)

   * [File validation instructions](https://docs.byteplus.com/en/docs/29/8586#70a80671)

6. In the **Order progress** section, find the **Check your configuration** part and click **Check**.

   BytePlus Certificate Center will check whether your DNS records or validation files are configured correctly and return the check result. If "Configuration Error" is prompted, please carefully check your configuration and make necessary modifications before rechecking.

7. Wait for the CA to periodically check your configuration.

   The CA automatically checks whether you have completed the relevant configuration as required every 5 minutes. When the CA confirms that you have completed the configuration correctly, the domain validation will end.


If you request a DV certificate, the CA will issue the certificate to you within a few hours after the domain validation is completed. If you request an OV/EV certificate, the CA needs to perform organization validation after the domain validation. The organization validation may take several working days to complete and requires relevant personnel from your organization to answer the phone. For more information, please refer to [Organization validation instructions](https://docs.byteplus.com/en/byteplus-certificate-center/docs/understanding-the-review-process-for-certificate-requests#organization-validation).

<span id="dns-validation-instructions"></span>
## DNS validation instructions

<span id="validation-requirements"></span>
### Validation requirements

Assume you are requesting an SSL certificate for the domain `dns-validation.example.com`. You have selected **Domain validation method** as **DNS validation**. The following figure shows the corresponding domain validation requirements. You need to create the specified DNS TXT record for the domain.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_04b9197a6473eeb5335201fadf1dc5c4.png) </span>

Next, we will take GoDaddy as an example to introduce how to create DNS records for the domain.

<span id="operation-steps"></span>
### Operation steps


1. Log on to the [GoDaddy DNS console](https://dcc.godaddy.com/control/portfolio).

2. On the **DNS management** page, select your domain name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20fafc4f3c204922a47af75565bb5bb0~tplv-goo7wpa0wc-image.image) </span>

3. Click **Add New Record**.

4. In the **New Records** area, configure the record according to the following instructions:

   * **Type**: Select **TXT**.

   * **Name**: Enter the **Domain name prefix** obtained from the domain validation requirements in the input box.

   * **Value**: Enter the **Record value** obtained from the domain validation requirements.

   * **TTL**: Select **1 Hour**.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fffa14f88ac3fde1d82cd4019f784874.png) </span>

5. Click **Save**.


Next, you can manually check your configuration according to the instructions in **Order progress**.

<span id="file-validation-instructions"></span>
## File validation instructions

<span id="validation-requirements"></span>
### Validation requirements

Assume you are requesting an SSL certificate for the domain `file-validation.example.com`. You have selected **Domain validation method** as **File validation**. The following figure shows the corresponding domain validation requirements. You need to add the specified validation file to your web server.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c085146b51ab6cbbdb8226a8c3bec5d4.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you request a certificate for the root domain (such as <code>example.com</code>) or a subdomain with the <code>www</code> prefix (such as <code>www.example.com</code>), you need to complete file validation for both the root domain and the corresponding subdomain with the <code>www</code> prefix.</div>


<div data-tips="true" data-tips-type="warning">This is because in most cases, the root domain and the subdomain with the <code>www</code> prefix are protected by the same certificate. For example, if the certificate is issued for the root domain, it is usually also used to protect the subdomain with the <code>www</code> prefix, and vice versa. Therefore, the CA needs to verify that you have the authority to manage both the root domain and the subdomain with the <code>www</code> prefix at the same time.</div>


Next, we will take the Nginx service on Ubuntu system to introduce how to create the validation file. If your server uses a different type of operating system, please refer to the documentation for the corresponding operating system. The following content is for reference.

<span id="prerequisites"></span>
### Prerequisites


* The domain `file-validation.example.com` points to the IP address of the web server.

* The web server has opened port 80 or 443.

* You have the tools, accounts, and passwords required to log in to the web server.


<span id="operation-steps"></span>
### Operation steps


1. Log in to the server.

2. Access the main directory of `file-validation.example.com`.

   The default main directory for Nginx is `/var/www/html`. You need to access the corresponding main directory according to the actual configuration of the site.

   ```Shell
   cd /var/www/html
   ```
   

3. Create a folder (`.well-known/pki-validation`) in the main directory, and create a file (`fileauth.txt`) in the folder.

   You can obtain the folder name and the file name from the domain validation requirements.

   ```Shell
   mkdir -p .well-known/pki-validation
   vim .well-known/pki-validation/fileauth.txt
   ```
   

4. Add the specified content to the newly created file.

   You can obtain the file content from the domain validation requirements.


Next, you can manually check your configuration according to the instructions in **Order progress**.
