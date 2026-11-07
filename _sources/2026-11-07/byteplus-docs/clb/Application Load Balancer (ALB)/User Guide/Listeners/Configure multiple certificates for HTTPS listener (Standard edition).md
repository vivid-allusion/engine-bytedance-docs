---
title: "Configure multiple certificates for HTTPS listener (Standard edition)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-SNI-for-an-HTTPS-listener_Standard-edition"
---

This article explains how to configure additional certificates for an HTTPS listener in the ALB console. Additional certificates apply to scenarios where multiple sites are deployed on the same server, each associated with its own certificate.

<span id="5f7aacc8"></span>
## Background

<span id="58f5a980"></span>
### SNI overview

Server Name Indication (SNI) is an extension of the TLS protocol. In scenarios where multiple sites are deployed on the same server and each has its own certificate, SNI resolves the following issue:


* When a client establishes a connection using HTTPS, the server cannot determine which site's certificate to send to the client.


If the client connects via HTTP, the server identifies the target site through the Host header in the client's request. However, when the client connects using HTTPS, a TLS handshake occurs before data transmission. During this process, the client has not yet sent the Host header to the server, so the server cannot determine which certificate to send to the client. In this case, the client can use the SNI extension to inform the server of the site it wants to access. This allows the server to send the corresponding certificate to the client during the TLS handshake phase.

<span id="f9eead0d"></span>
### ALB support for SNI

ALB supports SNI. During the TLS handshake phase, when ALB receives a message from the client containing the SNI extension, it first obtains the target domain name the client wants to access from the SNI extension. Then, ALB matches the target domain name with the certificate and sends the corresponding certificate to the client.

To implement this feature, you need to configure the certificate for the target domain on the listener. This process is called configuring "additional certificates." You can configure up to 40 additional certificates for one HTTPS listener.

<span id="9358ab04"></span>
### Smart certificate selection

The standard edition ALB instance supports the "smart certificate selection" feature. You only need to configure certificates for the listener. When the client establishes a connection with the ALB, the ALB automatically selects the best matching certificate based on the target domain the client wants to access. For detailed procedures, see [certificate matching](https://docs.byteplus.com/docs/clb/Configuring-SNI-for-an-HTTPS-listener_Standard-edition#858f0bd3).

<span id="486c8b73"></span>
## Before you begin


* You have already created an HTTPS listener.

* You have purchased a certificate from the [Certificate Center](https://console.byteplus.com/certificate-center/ssl/overview) or uploaded your certificate to the Certificate Center.


<span id="d5791c13"></span>
## Procedure


1. Log in to the [Application Load Balancer console](https://console.byteplus.com/alb).

2. On the **Instance management** page, locate the ALB instance to configure, and click **Listener** in the **Actions** column.

3. On the **Listener** tab, find the HTTPS listener that requires additional certificates, click the **More** icon in the **Actions** column, then select **Additional certificates**.

4. On the **Additional certificates** page, click **Edit** in the upper\-right corner.

5. On the **Edit extended certificate** page, click **Add certificate** to the right of **Additional certificates**.

   1. Select the source of the certificate. For more information about certificate sources, see [Certificate source](https://docs.byteplus.com/docs/clb/Configuring-SNI-for-an-HTTPS-listener_Standard-edition#d54a71a3) below.

   2. Select a certificate from the dropdown list.

      To add more certificates, continue clicking **Add certificate**.

6. After adding certificates, click **Confirmed**.


<span id="f19ca33c"></span>
## Related information

<span id="d54a71a3"></span>
### Certificate source

For Standard edition ALB instances, you can only configure certificates from the Certificate Center for listeners. You can purchase certificates in the [Certificate Center](https://console.byteplus.com/certificate-center/ssl/overview) or upload your certificates to the Certificate Center.

For detailed instructions on using certificates from the Certificate Center, refer to [Using Certificate Center Certificates with ALB](https://docs.byteplus.com/docs/clb/Using-certificates-from-BytePlus-Certificate-Center).

<span id="858f0bd3"></span>
### Certificate matching

<span id="9e49c480"></span>
#### Related concepts

Before understanding the certificate matching process, please familiarize yourself with the following concepts:


* Exact domain name

   An exact domain name refers to a specific domain that complies with domain name standards. This domain name is unique and used to accurately locate a particular website or network service. e.g., www.example.com is an exact domain name. This domain does not contain any wildcards and points to a specific website.

* wildcard domain

   A wildcard domain uses a wildcard (\*) to represent one or more characters. A wildcard domain can match multiple domains. However, a wildcard domain can only match domains at the same level and cannot match domains at different levels.

   For example, the wildcard domain \*.example.com can match domains at the same level such as mail.example.com, blog.example.com, and product1.example.com, but cannot match different\-level domains such as example.com and a.mail.example.com.

* Exact match

   An exact match occurs when the client’s target domain matches the exact domain associated with the certificate. For example, if the target domain is www.example.com and the certificate is associated with www.example.com, the exact match is successful.

* wildcard domain matching

   Wildcard domain matching occurs when the target domain accessed by the client matches the wildcard domain associated with the certificate. For example, if the target domain is www.example.com and the certificate is associated with \*.example.com, the wildcard domain match is successful.

* Default certificate

   When configuring additional certificates, you will see a default certificate on the **Additional Certificates** page. This certificate defaults to the one you selected when you created the listener, and you can replace the default certificate. If the target domain accessed by the client does not match any additional certificate, the listener returns the default certificate to the client. In this case, client\-side identity verification may fail due to a domain mismatch between the certificate and the target domain.


<span id="416c030c"></span>
#### Certificate matching process

The listener supports exact match and wildcard domain matching. Exact match has higher priority than wildcard domain match. When the client establishes a connection with the listener, the listener matches the target domain name requested by the client with the domain name associated with the certificate following the steps below and returns the corresponding certificate:


1. Match the target domain name with the exact domain name associated with the certificate.

   * If the exact match succeeds, the listener returns the certificate for the exact domain name to the client.

   * If the exact match fails, the listener tries to match the wildcard domain (go to step 2).

2. Match the target domain name with the wildcard domain associated with the certificate.

   * If the wildcard domain match succeeds, the listener returns the certificate for the wildcard domain to the client.

   * If the wildcard domain match fails, the listener returns the Default certificate to the client.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the target domain matches multiple certificates simultaneously, the listener determines which certificate to return based on the following priority:</div>



1. <div data-tips="true" data-tips-type="tip">Key algorithm:</div>


   <div data-tips="true" data-tips-type="tip"> ECC certificates have higher priority than RSA certificates.   </div>
   

   <div data-tips="true" data-tips-type="tip">Assuming the target domain matches  ECC, and RSA certificates simultaneously:   </div>
   

   * <div data-tips="true" data-tips-type="tip">If the client  supports ECC, the listener returns the ECC certificate.</div>


   * <div data-tips="true" data-tips-type="tip">If the client  ECC, the listener returns the RSA certificate.</div>


2. <div data-tips="true" data-tips-type="tip">Remaining validity period</div>


   <div data-tips="true" data-tips-type="tip">If the certificate key algorithms are the same, the listener returns the certificate with the longest remaining validity period.   </div>
   


<span id="71a2b14b"></span>
#### Certificate matching example

Suppose you add 2 extended certificates to a listener: cert\-1 and cert\-2 The domain name associated with cert\-1 is \*.example.com, and cert\-2 is associated with www.example.com


|**Domain name accessed by the client** |**Matched certificate** |**Listener actions** |
|---|---|---|
|www.example.com |cert\-2 |Return cert\-2 to the client |
|a.example.com |cert\-1 |Return cert\-1 back to the client |
|a.b.example.com |none |Return the Default certificate back to the client |
|example.com |none |Return the default certificate to the client |
