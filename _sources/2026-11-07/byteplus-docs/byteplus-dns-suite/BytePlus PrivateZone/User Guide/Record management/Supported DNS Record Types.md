---
title: "Supported DNS Record Types"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/prQAdU"
---

This document introduces the types of DNS records supported by BytePlus PrivateZone.

<span id="a-record"></span>
## A record

An A record specifies the IPv4 address corresponding to a domain name.

This type is defined in [RFC 1035](https://docs.byteplus.com/docs/6758/162499).

<span id="add-a-record"></span>
### Create an A record

For example, you need to add the following A record for `example.com`. In this A record, you specify the IPv4 address corresponding to the domain name `example.com` as `10.0.0.1`.

```Plain
@.example.com.           600           IN    A       10.0.0.1
```


<span id="steps"></span>
#### Steps

You need to use the following parameters to create an A record.


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the A record, i.e., `@.example.com`. |
|Record type |You need to set it to **A**. |
|Record value |The IPv4 address corresponding to the domain name `example.com`, i.e., `10.0.0.1`. |



* Refer to [Create DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/tmjP7G) to learn how to create a DNS record in the BytePlus PrivateZone console.

* Refer to [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/QSN6xl) to learn how to create a DNS record with OpenAPI.


<span id="aaaa-record"></span>
## AAAA record

An AAAA record specifies the IPv6 address corresponding to a domain name.

This type is defined in [RFC 3596](https://docs.byteplus.com/docs/6758/162499).

<span id="add-aaaa-record"></span>
### Create an AAAA record

For example, you need to create the following AAAA record for `example.com`. In this AAAA record, you specify the IPv6 address corresponding to the domain name `example.com` as `5e0d:6c48:6bb7:df07:ce44:5f55:5337:1901`.

```Plain
@.example.com.           600           IN    AAAA        5e0d:6c48:6bb7:df07:ce44:5f55:5337:1901
```


<span id="steps"></span>
#### Steps

You need to use the following parameters to add an AAAA record.


|**Parameter** |**Description** |
|---|---|
|Domain |The domain name corresponding to the AAAA record, i.e., `@.example.com`. |
|Record type |You need to set it to **AAAA**. |
|Record value |The IPv6 address corresponding to the `example.com` domain, i.e., `5e0d:6c48:6bb7:df07:ce44:5f55:5337:1901`. |



* Refer to [Create DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/tmjP7G) to learn how to create a DNS record in the BytePlus PrivateZone console.

* Refer to [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/QSN6xl) to learn how to create a DNS record with OpenAPI.


<span id="cname-record"></span>
## CNAME record

A CNAME record points one domain name to another domain name. Traffic can be routed to a system or service through a CNAME record. This type is defined in [RFC 1035](https://docs.byteplus.com/docs/6758/162499).

<span id="add-cname-record"></span>
### Create an CNAME record

For example, you need to add the following CNAME record for `example.com`. In this CNAME record, the domain name `example.com` points to `example.service.com`.

```Plain
@.example.com.    600           IN    CNAME    example.service.com. 
```


<span id="steps"></span>
#### Steps

You need to use the following parameters to create a CNAME record.


|**Parameter** |**Description** |
|---|---|
|Domain |The domain name corresponding to the CNAME record, i.e., `@.example.com`. |
|Record type |You need to set it to **CNAME**. |
|Record value |The domain name that `example.com` points to, i.e., `example.service.com`. |



* Refer to [Create DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/tmjP7G) to learn how to create a DNS record in the BytePlus PrivateZone console.

* Refer to [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/QSN6xl) to learn how to create a DNS record with OpenAPI.


<span id="mx-record"></span>
## MX record

An MX record points to an email server. When a user sends an email, the Mail Transfer Agent (MTA) sends a domain query request based on the domain name in the recipient's email address suffix (e.g., `example.com` in `abc@example.com`). Based on the returned MX record, the MTA can obtain the domain name of the email server and establish an SMTP connection with the email server.

The format of the MX record value is `priority domain`. You can enter the priority and the domain name of the email server, for example, `10 mail.service.com`. The smaller the number, the higher the priority.

In BytePlus PrivateZone, the priority range is 1 to 99.

In the following example, `mail01.service.com` has a higher priority than `mail02.service.com`. The MTA will first establish an SMTP connection with `mail01.service.com`. Only if `mail01.service.com` fails to send the email will the MTA establish an SMTP connection with `mail02.service.com`. In this case, `mail01.service.com` is the primary email server, and `mail02.service.com` is the backup email server.

```Plain
10 mail01.service.com
20 mail02.service.com
```


If you want to achieve load balancing between email servers, you can set the same priority for both domain names.

```Plain
10 mail01.service.com
10 mail02.service.com
```


<span id="create-an-mx-record"></span>
### Create an MX record

For example, you need to add the following MX record for `example.com`. In this MX record, the domain name `example.com` points to the email server domain name `mail.example.com`.

```Plain
@.example.com.   600    IN    MX    10    mail.example.com. 
```


<span id="steps"></span>
#### Steps

You need to use the following parameters to create an MX record.


|**Parameter** |**Description** |
|---|---|
|Domain |The domain name corresponding to the MX record, i.e., `@.example.com`. |
|Record type |You need to set it to **MX**. |
|Record value |The format of the record value is `priority domain`, i.e., `10 mail.example.com`. |



* Refer to [Create DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/tmjP7G) to learn how to create a DNS record in the BytePlus PrivateZone console.

* Refer to [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/QSN6xl) to learn how to create a DNS record with OpenAPI.


<span id="txt-record"></span>
## TXT record

A TXT record is a description set for a domain name. TXT is commonly used in the following scenarios:


* Verifying the owner of a domain name. For example, you create an NS record with domain registrar A, pointing a subdomain to domain registrar B for resolution. When you configure the record for this subdomain with domain registrar B, domain registrar B will provide you with a TXT record to confirm that you are the owner of this subdomain. You need to create this TXT record with domain registrar A. This way, domain registrar B can verify your identity.

* Implementing anti\-spam functionality based on SPF technology. For example, `v=spf1 a mx ~all`. This record value indicates that only the IP addresses configured in the A record and MX record under the domain name are authorized to use this domain name to send emails.


This type is defined in [RFC 1035](https://docs.byteplus.com/docs/6758/162499).

In BytePlus PrivateZone, the length of the TXT record value cannot exceed 512 characters. Additionally, the record value only supports ASCII characters except for double quotes (") and single quotes (').

<span id="create-a-txt-record"></span>
### Create a TXT record

For example, you need to add the following TXT record for `example.com`. This TXT record specifies that only the IP addresses configured in the A record and MX record under the domain name are authorized to use this domain name to send emails.

```Plain
@.example.com.     600    IN    TXT      v=spf1 a mx ~all 
```


<span id="Steps"></span>
#### Steps

You need to use the following parameters to add a TXT record.


|**Parameter** |**Description** |
|---|---|
|Domain |The domain name corresponding to the TXT record, i.e., `@.example.com`. |
|Record type |You need to set it to **TXT**. |
|Record value |You need to set it to `v=spf1 a mx ~all`. |



* Refer to [Create DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/tmjP7G) to learn how to create a DNS record in the BytePlus PrivateZone console.

* Refer to [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/QSN6xl) to learn how to create a DNS record with OpenAPI.


<span id="ptr-record"></span>
## PTR record

A PTR record resolves an IP address to a domain name. PTR records can be used for reverse DNS lookups. This type is defined in [RFC 1035](https://docs.byteplus.com/docs/6758/162499).

<span id="add-ptr-record"></span>
### Create a PTR record

Suppose in a VPC named `vpc01`, you need to configure reverse DNS resolution for an ECS with an IP address of `10.0.2.128`. This allows the IP address to be resolved to a domain name in reverse, facilitating network issue troubleshooting. The reverse\-resolved domain name is `example.internal.com`.

You need to add the corresponding reverse\-resolved domain name. The reverse\-resolved domain name is `2.0.10.in-addr.arpa`. You need to add a PTR record within the `2.0.10.in-addr.arpa` domain. This record points from the `128.2.0.10.in-addr.arpa` subdomain to the `test.internal.com` domain.

<span id="0b2ee319"></span>
#### Steps

You can refer to the following steps to create a PTR record:


1. Create a domain and set the **Domain** to `2.0.10.in-addr.arpa`. See [Create a Domain](https://docs.byteplus.com/en/docs/36/(/docs/byteplus-dns-suite/PU6MMV)).

2. In this domain, [create a record](https://docs.byteplus.com/docs/byteplus-dns-suite/tmjP7G) with the following configuration:

   
   |**Parameter** |**Description** |
   |---|---|
   |Domain |You need to set it to `128.2.0.10.in-addr.arpa`. |
   |Record type |You need to set it to **PTR**. |
   |Record value |You need to set it to `example.internal.com`. |
   


After the record is created, in the VPC associated with the domain name, BytePlus PrivateZone will resolve `128.2.0.10.in-addr.arpa` to `example.internal.com`.

You can use the `dig ptr 128.2.0.10.in-addr.arpa` command to verify whether the reverse DNS resolution is effective.
