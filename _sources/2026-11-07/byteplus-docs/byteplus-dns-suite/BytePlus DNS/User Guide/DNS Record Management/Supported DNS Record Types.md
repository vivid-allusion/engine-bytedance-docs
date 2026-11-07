---
title: "Supported DNS Record Types"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-supported-dns-record-types"
---

This document introduces the types of DNS records supported by BytePlus DNS and the methods to create each type of DNS record.

Different types of DNS records may conflict with each other. When multiple types of DNS records coexist, some DNS records may not take effect. For more information, see [Avoid Conflicts in DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-avoiding-conflicts-in-dns-records).

<span id="56e9ffc9"></span>
## A record

An A record specifies the IPv4 address corresponding to a domain name.

This record type is defined in [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/).

<span id="a7c3790f"></span>
### Create an A record

For example, you need to add the following A record for example.com. In this A record, you specify the IPv4 address `203.0.113.0` corresponding to the domain name example.com.

```Plain
@.example.com.           600           IN    A        203.0.113.0
```


<span id="7822301c"></span>
#### Steps

You need to create an A record with the following parameters.


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the A record, such as `@.example.com`. |
|Record type |Set this parameter to **A**. |
|Record value |The IPv4 address corresponding to the domain name example.com, for example, `203.0.113.0`. |



* See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for how to create a DNS record in the BytePlus DNS console.

* See [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createrecord) for how to create a DNS record using the BytePlus DNS OpenAPI.


<span id="2860f19e"></span>
## AAAA record

An AAAA record specifies the IPv6 address corresponding to a domain name.

This record type is defined in [RFC 3596](https://datatracker.ietf.org/doc/rfc3596/).

<span id="3bd67582"></span>
### Create an AAAA record

For example, you need to add the following AAAA record for example.com. In this AAAA record, you specify the IPv6 address `2001:db8::` corresponding to the domain name `example.com`.

```Plain
@.example.com.           600           IN    AAAA        2001:db8::
```


<span id="0a85b714"></span>
#### Steps

You need to add an AAAA record with the following parameters.


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the AAAA record, for example, `@.example.com`. |
|Record type |Set this parameter to **AAAA**. |
|Record value |The IPv6 address corresponding to the domain name example.com, for example, `2001:db8::`. |



* See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for how to create a DNS record in the BytePlus DNS console.

* See [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createrecord) for how to create a DNS record using the BytePlus DNS OpenAPI.


<span id="5fcc5807"></span>
## CNAME record

A CNAME record points one domain name to another domain name. Traffic can be routed to a system or service through a CNAME record.

This record type is defined in [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/).

<span id="c701f7e2"></span>
### Create a CNAME record

For example, you need to add the following CNAME record for `example.com`. In this CNAME record, the domain name `example.com` points to the domain name `example.service.com`.

```Plain
@.example.com.    600           IN    CNAME    example.service.com.
```


<span id="297987ad"></span>
#### Steps

You need to create a CNAME record with the following parameters.


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the CNAME record, such as `@.example.com`. |
|Record type |Set this parameter to **CNAME**. |
|Record value |The domain name that `example.com` points to, such as `example.service.com`. |



* See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for how to create a DNS record in the BytePlus DNS console.

* See [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createrecord) for how to create a DNS record using the BytePlus DNS OpenAPI.


<span id="alias-record"></span>
## Alias record

An Alias record points a domain name to a BytePlus cloud resource domain name. An Alias record is a special type of record provided by BytePlus DNS and is not defined in any RFC.

See [What is an Alias Record](https://docs.byteplus.com/docs/byteplus-dns-suite/What_is_an_Alias_Record).

<span id="58a6b983"></span>
## MX record

MX records point to an email server. When a user sends an email, the Mail Transfer Agent (MTA) sends a domain query request based on the domain name in the recipient's email address suffix (e.g., `example.com` in `abc@example.com`). With the returned MX records, the MTA can obtain the domain name of the email server and establish an SMTP connection with it.

The format of the MX record value is `<priority> <domain>`. You can input the priority value and the domain name of the mail server, for example, `10 mail.service.com`. The lower the priority value, the higher the priority.

In BytePlus DNS, the priority value for MX records ranges from 1 to 99.

In the following example, `mail01.service.com` has a higher priority than `mail02.service.com`. The MTA will establish an SMTP connection with `mail01.service.com` first. Only when sending emails fails with `mail01.service.com`, will the MTA establish an SMTP connection with `mail02.service.com`. In this case, `mail01.service.com` is the primary email server, and `mail02.service.com` is the backup email server.

```Plain
10 mail01.service.com
20 mail02.service.com
```


If you want to achieve load balancing between email servers, you can set the same priority value for both domains.

```Plain
10 mail01.service.com
10 mail02.service.com
```


This record type is defined in [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/).

<span id="734431b2"></span>
### Create an MX record

For example, if you need to add the following MX record for `example.com`, where the domain name `example.com` points to the mail server with the domain name `mail.example.com`.

```Plain
@.example.com.   600    IN    MX    10    mail.example.com.
```


<span id="9dd7a5b0"></span>
#### Steps

You need to create an MX record with the following parameters:


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the MX record, such as `@.example.com`. |
|Record type |Set this parameter to **MX**. |
|Record value |The format of the record value is `priority domain`, such as `10 mail.example.com`. |



* See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for how to create a DNS record in the BytePlus DNS console.

* See [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createrecord) for how to create a DNS record using the BytePlus DNS OpenAPI.


<span id="e71c6642"></span>
## NS record

NS records specify the authoritative DNS servers for a domain name.

This record type is defined in [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/).

<span id="788b4aa2"></span>
### Create an NS record

For example, if you need to add the following NS record for `example.com`, where `example.com` uses the domain name `ns1.example.com` as the authoritative DNS server for domain name resolution.

```Plain
@.example.com.       600           IN    NS       ns1.example.com.
```


<span id="c10366ef"></span>
#### Steps

You need to create an NS record with the following parameters:


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the NS record, such as `@.example.com`. |
|Record type |Set this parameter to **NS**. |
|Record value |The DNS server used to resolve the `example.com` domain name, i.e., `ns1.example.com`. |



* See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for how to create a DNS record in the BytePlus DNS console.

* See [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createrecord) for how to create a DNS record using the BytePlus DNS OpenAPI.


<span id="8c71f2d9"></span>
## TXT record

TXT records provide additional information about a domain name. TXT records are commonly used in the following scenarios:


* Verifying the domain name ownership. For example, when you create an NS record at domain service provider A to point a subdomain to domain service provider B for resolution, domain service provider B will provide you with a TXT record to confirm your ownership of the subdomain. You need to create this TXT record at domain service provider A to verify your identity.

* Implementing anti\-spam functionality based on SPF technology. For example, `v=spf1 a mx ~all`. This record value indicates that only the IP addresses configured in the A records and MX records under the domain name have permission to send emails using this domain name.


This record type is defined in [RFC 1035](https://datatracker.ietf.org/doc/rfc1035/).

In BytePlus DNS, the length of the record value for TXT records cannot exceed 255 characters. Additionally, the record value cannot contain `"` or `'`.

<span id="91b20091"></span>
### Create a TXT record

For example, if you need to add the following TXT record for `example.com`, which specifies that only the IP addresses configured in the A records and MX records under the domain name have permission to send emails using this domain name.

```Plain
@.example.com.     600    IN    TXT      v=spf1 a mx ~all
```


<span id="55842669"></span>
#### Steps

You need to create a TXT record with the following parameters:


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the TXT record, such as `@.example.com`. |
|Record type |Set this parameter to **TXT**. |
|Record value |Set this parameter to `v=spf1 a mx ~all`. |



* See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for how to create a DNS record in the BytePlus DNS console.

* See [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createrecord) for how to create a DNS record using the BytePlus DNS OpenAPI.


<span id="b2ad3c2b"></span>
## SRV record

SRV records indicate specific servers used by specific services. For example, for Microsoft Active Directory, you can specify domain controllers using SRV records to ensure proper operation for Active Directory users.

The format of the SRV record value is `priority weight port domain`. For example, `0 3 3000 sipserver.example.com`.

This record type is defined in [RFC 2782](https://datatracker.ietf.org/doc/rfc2782/).

<span id="2cae0cd7"></span>
### Create an SRV record

You need to add the following SRV records for example.com. These SRV records specify domain controllers.

```Plain
@.example.com.  600  IN  SRV  0  3  3000  sipserver.example.com.
```


<span id="da8c7cea"></span>
#### Steps

You need to add an SRV record with the following parameters.


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the SRV record, such as @.example.com. |
|Record type |Set this parameter to **SRV**. |
|Record value |`0 3 3000 sipserver.example.com`. |



* See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for how to create a DNS record in the BytePlus DNS console.

* See [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createrecord) for how to create a DNS record using the BytePlus DNS OpenAPI.


<span id="06d300fb"></span>
## CAA record

CAA records are used to specify the certificate authorities (CAs) allowed to issue certificates for a domain.

The format of the CAA record value is `[flag] [tag] [value]`. This format includes the following parameters:


* [flag]: Indicates how the CA processes the record value. In most cases, the parameter value is 0. 0 means that if the CA cannot recognize the meaning of the tag parameter value in the record value, the CA will ignore the record value. For more information on the meaning of the [flag] parameter, refer to [RFC 6844](https://datatracker.ietf.org/doc/rfc6844/). In BytePlus DNS, the [flag] parameter ranges from 0 to 255.

* [tag]: This parameter can have the following values:

   * issue: Represents a CA. Only this CA can issue certificates for the specified domain.

   * issuewild: Represents a CA. Only this CA can issue wildcard certificates for the specified domain.

   * iodef: Represents a URL. If a CA receives a certificate request that is not in the list of specified CAs, the CA can send the violation record to this URL.

* [value]: If the [tag] parameter is `issue` or `issuewild`, this parameter represents the specified CA. If the [tag] parameter is `iodef`, this parameter represents the specified URL.


This record type is defined in [RFC 6844](https://datatracker.ietf.org/doc/rfc6844/).

<span id="d0f0bd28"></span>
### Create a CAA record

For example, you need to add the following CAA records for example.com. In these CAA records, you specify two CA organizations, DigiCert and Let's Encrypt, for example.com. Additionally, you specify an iodef record.

```Plain
@.example.com.     600      IN    CAA      0 issue "letsencrypt.org" 
@.example.com.     600      IN    CAA      0 issue "digicert.com" 
@.example.com.     600      IN    CAA      0 iodef "mailto:admin@dns-example.com"
```


When you apply for a certificate for example.com:


* If you apply for a certificate from DigiCert or Let's Encrypt, DigiCert or Let's Encrypt will issue the certificate.

* If you apply for a certificate from GeoTrust, GeoTrust will not issue the certificate. Additionally, GeoTrust can send the violation record to the admin@dns\-example.com email address.


<span id="eaad2325"></span>
#### Steps

You need to add a CAA record with the following parameters.


|**Parameter** |**Description** |
|---|---|
|Domain name |The domain name corresponding to the CAA record, such as example.com. |
|Record type |Set this parameter to **CAA**. |
|Line |Set this parameter to **Default**. Otherwise, some CA organizations may fail to authenticate. |
|Record value |The attributes of the CAA record, including issue, issuewild, or iodef. Each record value contains one attribute. You can add one or more record values. The domain name in the record value should be enclosed in double quotation marks (""). Set the record value as shown in the screenshot below.<br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_650c5a8e3a626d03206c91bfbd4ecfac.jpeg) </span> |



* See [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) for how to create a DNS record in the BytePlus DNS console.

* See [CreateRecord API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createrecord) for how to create a DNS record using the BytePlus DNS OpenAPI.


<span id="ptr-record"></span>
## PTR Record

A PTR (Pointer) record is used to perform a Reverse DNS Lookup, which maps an IP address back to its corresponding domain name. Reverse DNS lookups are commonly applied in the following scenarios:


* Anti\-Spam Filtering (Email Validation):

   When a user sends an email, the Mail Transfer Agent (MTA) typically performs a standard DNS query on the recipient's domain (e.g., `example.com` in `abc@example.com`) to find the associated IP address. In addition, some email service providers' MTAs perform a Reverse DNS Lookup on the sender's IP address. This is done to verify that the domain name retrieved from the reverse lookup matches the sender's actual domain name. If the names do not match, or if the sending IP address lacks a valid PTR record, the verification fails, and the email may be rejected as potential spam.

* Log\-Based Troubleshooting:

   System logs generally record IP addresses rather than domain names. A Reverse DNS Lookup allows administrators to quickly resolve these IP addresses to their corresponding domain names, which significantly aids in troubleshooting and security analysis.


PTR records are defined in [RFC 1035](https://www.rfc-editor.org/rfc/rfc1035) and [RFC 8501](https://www.rfc-editor.org/rfc/rfc8501).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus DNS currently supports PTR records for IPv4 addresses only. Support for IPv6 PTR records is not available at this time.</div>


<span id="create-a-ptr-record"></span>
### Create a PTR Record

For instructions, see [Purchase a PTR record](https://docs.byteplus.com/docs/byteplus-dns-suite/purchase_a_ptr_record).
