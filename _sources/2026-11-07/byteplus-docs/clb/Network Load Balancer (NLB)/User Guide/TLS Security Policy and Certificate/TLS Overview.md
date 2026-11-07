---
title: "TLS Overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-TLS-Overview"
---

## Introduction​

TLS (Transport Layer Security) establishes secure connections between clients and servers over TCP by leveraging certificates and TLS security policies, encrypting and authenticating data in transit. You can use the feature by creating a TLS listener.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_321cac232151d1ec186427b30c577bd8.png)

> **tip**

> Dual\-stack instances do not support TLS listener creation at this time.

## Certificate

A certificate serves as an identity proof for network communication.

An SSL certificate is used to verify the legitimacy of a server and is trusted globally on the internet.

* Default certificate: A mandatory server certificate bound to the TLS listener. This certificate can only be replaced and cannot be deleted.

* Additional certificate: Server certificates bound to a TLS listener beyond the default certificate, enabling support for multi\-domain and multi\-certificate requirements.

* CA certificate: A certificate used by the NLB to authenticate client identities.

### Expiration

Expired certificates cannot be renewed; they can only be replaced.

For information related to SSL certificate expiration, refer to Certificate message.

For information related to CA certificate expiration, refer to Creating a private root CA.

### Limitations

* A single TLS listener must be bound to exactly one default certificate.

* A single TLS listener supports up to 25 additional certificates by default. If the default quota does not meet requirements, you can go to Quota Center to apply for an increase.

* A single listener only supports one CA certificate.

* Each certificate bound to a listener can associate with a maximum of 64 domain names, with the total length of domain names (Common Name + Subject Alternative Names) not exceeding 16,384 bytes.

## **Security Policy**

Security policies consist of TLS versions and cipher suites. The supported cipher suites vary by the version of TLS protocol. Higher TLS protocol versions offer stronger security at the cost of increased client compatibility requirements.

Some services support broader TLS versions and cipher suites to ensure compatibility with diverse clients, while others enforce stricter configurations by restricting TLS protocol versions and cipher suites for enhanced security. We have pre\-configured some security policies based on common scenarios for you. If the system pre\-configured policies are insufficient for your needs, you can also customize security policies.

**System Default Policy**

|**System Default Policy Name** |**Included TLS protocol version** |**Included Cipher Suites** |
|---|---|---|
|tls_cipher_policy_1_0<br><br> |TLSv1.0<br><br>TLSv1.1<br><br>TLSv1.2 |* ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-AES256\-SHA384<br><br>* ECDHE\-ECDSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* AES256\-GCM\-SHA384<br><br>* AES128\-GCM\-SHA256<br><br>* AES256\-SHA256<br><br>* AES128\-SHA256<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* AES256\-SHA<br><br>* AES128\-SHA<br><br>* DES\-CBC3\-SHA |
|tls_cipher_policy_1_1<br><br> |TLSv1.1<br><br>TLSv1.2 ||
|tls_cipher_policy_1_2 |TLSv1.2 ||
|tls_cipher_policy_1_2_strict |TLSv1.2 |* ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-AES256\-SHA384<br><br>* ECDHE\-ECDSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA |
|tls_cipher_policy_1_2_strict_with_1_3 |TLSv1.2<br><br>TLSv1.3 |* TLS_CHACHA20_POLY1305_SHA256<br><br>* TLS_AES_256_GCM_SHA384<br><br>* TLS_AES_128_GCM_SHA256<br><br>* TLS_AES_128_CCM_8_SHA256<br><br>* TLS_AES_128_CCM_SHA256<br><br>* ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-AES256\-SHA384<br><br>* ECDHE\-ECDSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA |

**Custom Security Policy**

|**TLS Versions** |**Optional Cipher Suite** |
|---|---|
|TLSv1.0<br><br> |* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* AES128\-SHA<br><br>* AES256\-SHA<br><br>* DES\-CBC3\-SHA |
|TLSv1.1 ||
|TLSv1.2 |* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* AES128\-SHA<br><br>* AES256\-SHA<br><br>* DES\-CBC3\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-AES128\-SHA256<br><br>* ECDHE\-ECDSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* AES128\-GCM\-SHA256<br><br>* AES256\-GCM\-SHA384<br><br>* AES128\-SHA256<br><br>* AES256\-SHA256 |
|TLSv1.3 |* TLS_CHACHA20_POLY1305_SHA256<br><br>* TLS_AES_256_GCM_SHA384<br><br>* TLS_AES_128_GCM_SHA256<br><br>* TLS_AES_128_CCM_8_SHA256<br><br>* TLS_AES_128_CCM_SHA256<br><br>* TLS_SM4_GCM_SM3 (SM)<br><br>* TLS_SM4_CCM_SM3 (SM)<br><br><br>> **tip**<br><br><br>> TLS_SM4_GCM_SM3 and TLS_SM4_CCM_SM3 are in Beta. For trial requests, contact your account manager.<br> |

## Matching process

SNI (Server Name Indication): When a single IP hosts multiple domains, this allows the client to specify the target domain to the NLB during the TLS handshake. The NLB then selects the corresponding certificate based on this information.

The NLB matches certificates first using exact SNI matching, the longest suffix principle. If multiple certificates match: Priority is given to Chinese cryptographic algorithm certificates (SM certificates). Otherwise, additional certificates are selected based on their upload sequence. If no match is found, the default certificate is used.
