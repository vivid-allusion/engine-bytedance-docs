---
title: "Configuring multiple certificates for an HTTPS listener (Basic Edition)"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-SNI-for-an-HTTPS-listener"
---

This topic describes how to configure extended certificates for HTTPS listeners in the Application Load Balancer (ALB) console. Extended certificates are suitable for the following scenario: When multiple sites are deployed on the same server, each site is associated with its own certificate.

## Background

### SNI overview

Server Name Indication (SNI) is an extension of the TLS protocol. In scenarios where multiple sites are deployed on the same server with their respective certificates, SNI addresses the following issue: when a client uses the HTTPS protocol to establish a connection with the server, the server cannot determine which site's certificate to send to the client.

If the client uses HTTP, the server identifies the target site from the Host header in the client request. However, if HTTPS is used, a TLS handshake occurs before data transmission. During this process, the client has not yet sent the Host header, so the server cannot decide which certificate to send. In this case, the client can use the SNI extension to inform the server of the target site it intends to access. This allows the server to send the corresponding certificate during the TLS handshake phase.

### ALB support for SNI

ALB supports SNI. During the TLS handshake, when ALB receives a client message containing the SNI extension, it first extracts the target domain name the client wants to access from the SNI extension. ALB then performs certificate matching and sends the corresponding certificate to the client.

To achieve this functionality, you need to configure certificates for the target domain names on the listener. This process is called configuring extended certificates. You can configure up to 20 extended certificates for one HTTPS listener.

### Certificate matching

ALB selects the certificate based on the mapping you configure between the domain name, forwarding rules, and certificates. For detailed procedures, see [Certificate matching](https://docs.byteplus.com/docs/clb/Configuring-SNI-for-an-HTTPS-listener#e531cddf).

## Prerequisites

You have created an HTTPS listener.

## Precautions

When configuring extended certificates for a Basic Edition ALB instance, you need to simultaneously specify the domain name associated with that certificate.

Additionally, you must configure a forwarding rule for that domain name under the listener. Only then will the corresponding certificate configuration take effect. For example, if you configure an extended certificate for example.com, you must also configure a forwarding rule for example.com. The domain name configured in the forwarding rule must be exactly the same as the domain name associated with the extended certificate.

## Procedures

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. On the **Instance Management** page, find the ALB instance to configure and click **Listener** in the **Actions** column.

3. On the **Listener** tab, find the HTTPS listener that requires extended certificates and click **Manage certificate** in the **Actions** column.

4. On the **Extended certificate** page, click **Edit** in the upper right corner.

5. On the **Edit extended certificate** page, click **Add certificate** under **Extended certificate**.

   1. Select the source of the certificate. Certificates used by Basic Edition ALB instances can be either certificates existing on the ALB side or certificates from the Certificate Center. For more information about the certificate source, see the [Certificate source](https://docs.byteplus.com/docs/clb/Configuring-SNI-for-an-HTTPS-listener#f5bb4e95) below.

   2. Select a certificate. You need to input the domain name and then select the certificate associated with that domain. If you input a wildcard domain name, the selected certificate must also be one associated with that wildcard domain.

      When inputting the domain name, please note the following restrictions:

      * The domain name can only contain lowercase letters, numbers, and the special characters ., \-, \*.

      * Domain names must contain at least one half\-width period (.), but cannot begin or end with a half\-width period (.).

      * Domain names configured under the same listener cannot be duplicated.

         You can click **Add certificate** to add more certificates. However, note that the domain names associated with the certificates you input must not be repeated.

6. After adding the certificate, click **Save**.

## Related information

### Certificate source

Basic Edition ALB instances support certificates from the following sources:

* Certificates from the ALB side.

* Certificates from the Certificate Center.

To use certificates on the ALB side, you need to previously:

* Upload your certificate to the ALB console. ALB only allows uploading certificates in PEM format. Certificates in other formats must be converted to PEM format before they can be uploaded. For related operations, see [Adding/Deleting a certificate](https://docs.byteplus.com/docs/clb/Adding-and-deleting-a-certificate) and [Converting the certificate format](https://docs.byteplus.com/docs/clb/Converting-certificate-formats).

To use certificates from the Certificate Center, you need to previously:

* Purchase a certificate from Certificate Center or upload your certificate to Certificate Center.

For detailed instructions on using certificates from Certificate Center, see [ALB using certificates from Certificate Center](https://docs.byteplus.com/docs/clb/Using-certificates-from-BytePlus-Certificate-Center).

We recommend using certificates from the Certificate Center. In the [Certificate Center console](https://console.byteplus.com/certificate-center/ssl/overview), you have a one\-stop shop for purchasing, uploading, and managing certificates.

### Certificate matching

#### Related terms

Before understanding the certificate matching process, please familiarize yourself with the following concepts:

* Exact domain name

   An exact domain name refers to a specific domain name that conforms to domain name standards. This domain is unique and used to precisely locate a specific website or network service. For example, www.example.com is an exact domain name. It does not contain any wildcards and points to a particular website.

* Wildcard domain

   A wildcard domain refers to a domain name that uses an asterisk (\*) to represent one or more characters. A wildcard domain name can match multiple domain names. However, a wildcard domain can only match domain names at the same level, not domain names at different levels.

   For example, the wildcard \*.example.com can match domain names at the same level, such as mail.example.com, blog.example.com, and product1.example.com. However, it cannot match domain names at different levels, such as example.com (a higher level) or a.mail.example.com (a lower level).

* Exact match

   An exact match occurs when the target domain name the client wants to access matches an exact domain name associated with a certificate. For example, if the target domain is www.example.com and the certificate is associated with www.example.com, then the exact match is successful.

* Wildcard domain matching

   Wildcard match occurs when the target domain name the client wants to access matches a wildcard domain name associated with a certificate. For example, if the target domain is www.example.com and the certificate is associated with \*.example.com, then the wildcard match is successful.

* Default certificate

   When configuring extended certificates, you will see a default certificate on the **Extended certificate** page. This certificate is, by default, the one you selected when creating the listener. You can replace the default certificate. When the client's target domain name cannot match any extended certificate, the listener returns this default certificate to the client. In this case, identity verification on the client side may fail due to a mismatch between the domain associated with the certificate and the target domain.

#### Certificate matching process

For Basic Edition ALB instances, when configuring extended certificates, you need to manually specify the domain name associated with the certificate and configure forwarding rules for these domain names. These operations effectively establish the association between the domain name, forwarding rules, and the certificate.

When a client establishes a connection with the listener, the listener follows the workflow below to match and send the appropriate certificate to the client:

* Checks if the domain name requested by the client matches any forwarding rule.

   * If a matching forwarding rule is found, the listener checks whether that rule is associated with a certificate:

      * If the forwarding rule is associated with a certificate, the listener sends that certificate to the client.

      * If the forwarding rule is not associated with a certificate, the listener sends the default certificate to the client.

   * If no forwarding rule matches the domain, the listener sends the default certificate to the client.

> **tip**

> When matching forwarding rules, the listener supports both exact matching and wildcard matching. If the client's requested domain matches both a wildcard domain rule and an exact domain rule, the listener selects the exact domain rule and sends its associated certificate to the client.

#### Certificate matching example

Assume you add two extended certificates to a listener: cert\-1 and cert\-2. cert\-1 is associated with the wildcard domain \*.example.com; cert\-2 is associated with the exact domain www.example.com. You have configured \*.example.comin forwarding rule rule\-1 and www.example.comin forwarding rule rule\-2.

|**Client\-accessed domain name** |**Matched forwarding rules** |**Matched certificate** |**Listener behavior** |
|---|---|---|---|
|www.example.com |rule\-2 |cert\-2 |Return cert\-2 to the client |
|a.example.com |rule\-1 |cert\-1 |Return cert\-1 to the client |
|a.b.example.com |None |None |Return the default certificate to the client |
|example.com |none |None |Return the default certificate to the client |

## What to do next

Create forwarding rules. The forwarding rule must include the domain name specified when you configured the extended certificate. For relevant operations, see [Creating a forwarding rule (Basic edition)](https://docs.byteplus.com/docs/clb/Creating-a-forwarding-rule).
