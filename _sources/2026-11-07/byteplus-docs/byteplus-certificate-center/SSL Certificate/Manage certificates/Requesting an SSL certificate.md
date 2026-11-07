---
title: "Requesting an SSL certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-requesting-a-certificate"
---

CA (Certificate Authority) is the authoritative organization that issues trusted SSL certificates on the internet. You can submit SSL certificate requests to the CA through the BytePlus Certificate Center console. After the CA approves your certificate request, they will issue the certificate to you. This article introduces the method of submitting an SSL certificate request to the CA.

<span id="prerequisites"></span>
## Prerequisites

You have a certificate instance in the **Inactive** status.

If you selected **By quantity** as the **Purchase method** when creating the SSL certificate order (i.e., you did not immediately submit the certificate request), after the certificate order is created, you will obtain one or more certificate instances in the **Inactive** status. You can use these instances to submit certificate requests at any time. For more information, see [Creating an SSL certificate order](https://docs.byteplus.com/en/byteplus-certificate-center/docs/creating-certificate-order).

<span id="procedure"></span>
## Procedure


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, choose **SSL Certificate** \> **Certificates**.

3. In the certificate instance list, find your certificate instance and click **Request certificate** in the **Actions** column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Request certificate</strong> operation only appears when the status of the certificate instance is <strong>Inactive</strong>. You can click <strong>Inactive</strong> at the top of the list to display all certificate instances in the <strong>Inactive</strong> status.   </div>
   

4. On the **Request certificate** page, complete the configuration according to the [Configuration instructions](https://docs.byteplus.com/en/docs/29/8585#configuration-instructions), and then click **Submit**.


After the certificate request is submitted, the status of the corresponding certificate instance will change from **Inactive** to **Validating**.

<span id="configuration-instructions"></span>
## Configuration instructions


|Configuration item |Description |
|---|---|
|**Key algorithm** |Choose the key algorithm used by the certificate. Options:<br><br><br>* **RSA** (default): RSA, full name Rivest, Shamir, Adleman, is a widely used asymmetric key algorithm with good compatibility.<br><br>* **ECC**: ECC (Elliptic Curve Cryptography) is a more advanced and secure key algorithm. ECC encryption is faster, more efficient, and consumes fewer server resources compared to RSA. ECC is supported by mainstream browsers.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration item only appears when the <strong>CSR from</strong> is <strong>Auto generate</strong>.</div><br> |
|**CSR from** |Select the method of generating the CSR file. CSR (Certificate Signing Request) is your certificate signing request file, which contains the certificate public key and information such as your domain name and organization name. The CSR needs to be submitted to the CA for review. Options:<br><br><br>* **Auto generate** (recommended): BytePlus Certificate Center automatically generates the CSR and private key for you using the key algorithm you specify. After the CA issues the certificate to you, you can download the certificate and private key files from the BytePlus Certificate Center console.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only with correct CSR content can the certificate request be successful. It is recommended that you choose to automatically generate the CSR to avoid certificate request failure due to incorrect CSR content.   </div><br>   <br><br>* **Manual input**: You manually generate the CSR and private key and enter the CSR content in the **CSR** input box. You can use OpenSSL, Keytool, or other tools to generate the CSR and private key.<br><br>   To facilitate unified management, you can also paste the private key content generated manually into the **Private key** input box. In this way, BytePlus Certificate Center helps you manage your private key as well. If you do not provide a private key, you need to keep the private key by yourself.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The information in the CSR you fill in must match the content of the <strong>Information template</strong> you selected.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please keep your private key secure. Once the private key is compromised, your certificate will no longer be secure.   </div><br>    |
|**CSR** |Enter the content of the CSR.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration item only appears when the <strong>CSR from</strong> is <strong>Manual input</strong>.</div><br> |
|**Private key** |Enter the content of the private key.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration item only appears when the <strong>CSR from</strong> is <strong>Manual input</strong>.</div><br> |
|**Domain name** |Enter the domain name to which the certificate will be issued, according to the instructions in the input box. This configuration corresponds to the CN (Common Name) field of the certificate.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration item only appears when the <strong>CSR from</strong> is <strong>Auto generate</strong>.</div><br><br><br>Depending on the **Domain type** selected when ordering the certificate, different content is allowed.<br><br><br>* If the **Domain type** is **Single domain (FQDN)** , you can enter a FQDN or an IP address. Example: `example.com`, `www.example.com`, `1.XX.XX.1`<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can only enter an IP address when requesting certain brands of SSL certificates.   </div><br>   <br><br>* If the **Domain type** is **Wildcard domain**, you can enter a wildcard domain. Example: `*.example.com` |
|**Information template** |Choose an information template. Information templates are categorized into two types: **Individual** and **Organization**.<br><br><br>* **Individual** information templates contain the name, mobile number, and email address of the contact person.<br><br>* **Organization** information templates contain not only the name, mobile number, and email address of the contact person, but also the information of the organization.<br><br><br>If you have not created an information template, you can click **Create template** to create one. Information templates will be saved in the BytePlus Certificate Center for reuse.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When requesting OV/EV certificates, you must choose an <strong>Organization</strong> type information template.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Please ensure that the contact information provided in the information template is accurate, otherwise it may cause the certificate request to fail.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After you submit the certificate request, BytePlus Certificate Center will send validation notification to the contact person's mobile number and email address.</div><br> |
|**Domain validation method** |Select the method for verifying domain ownership. Options:<br><br><br>* **DNS validation**: This method requires you to log in to the DNS service provider's system and create a DNS TXT/CNAME record for the domain. The CA checks regularly if the specified record exists. DNS validation will end when the CA confirms that the specified record exists.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use BytePlus DNS Suite as your domain's DNS service provider, DNS validation will be automatically completed. You do not need to manually create DNS records.   </div><br>   <br><br>* **File validation**: This method requires you to add the specified validation file to a specific path on the web server. The CA checks regularly if the specified file can be accessed. File validation will end when the CA confirms that the specified file can be accessed.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <strong>File validation</strong> method only appears when the <strong>Domain type</strong> of the certificate instance is <strong>Single domain (FQDN)</strong>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before selecting this method, you must ensure that the address (domain name or IP) of the web server can be accessed via the Internet.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The CA only supports sending validation requests to ports 80 and 443. Before selecting this method, please ensure that your web server has opened ports 80 and 443.   </div><br>    |


<span id="next-steps"></span>
## Next steps

After submitting the certificate request, you need to cooperate with the CA to complete the certificate information validation. You can click on the ID of the certificate instance to enter the certificate details page. The **Order progress** area on the right side of the certificate details page will display the progress of the certificate request.


* Please complete the domain validation as soon as possible according to the requirements. For related operations, please refer to [Demonstrating control over domain](https://docs.byteplus.com/byteplus-certificate-center/docs/conducting-domain-validation).

* If you request an OV/EV certificate, the CA also needs to perform organization validation. During the validation process, please pay attention to answering phone calls. For more information, please refer to [Organization validation](https://docs.byteplus.com/en/byteplus-certificate-center/docs/understanding-the-review-process-for-certificate-requests#organization-validation).
