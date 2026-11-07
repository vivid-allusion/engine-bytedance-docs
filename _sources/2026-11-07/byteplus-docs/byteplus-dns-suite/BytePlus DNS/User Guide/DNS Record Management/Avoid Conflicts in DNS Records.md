---
title: "Avoid Conflicts in DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-avoiding-conflicts-in-dns-records"
---

This document introduces how different types DNS records conflict with each other in BytePlus DNS.

In the same domain, if the DNS record you create conflicts with an existing DNS record, you cannot create that DNS record.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only DNS records with the same domain prefix can potentially conflict. DNS records with different domain prefixes will not conflict.</div>


* <div data-tips="true" data-tips-type="tip">DNS record conflicts can only occur in the same line. DNS records in different lines will not conflict.</div>


* <div data-tips="true" data-tips-type="tip">✅ indicates no conflict. Non\-conflicting DNS records with the same line in the same domain can coexist. For example, A records with the domain prefix "@" can coexist with NS records with the domain prefix "@" in the domain example.com.</div>


* <div data-tips="true" data-tips-type="tip">❌ indicates conflict. Conflicting DNS records with the same line in the same domain cannot coexist. For example, CNAME records with the domain prefix "@" cannot coexist with A records with the domain prefix "@" in the domain example.com.</div>


* <div data-tips="true" data-tips-type="tip">↔️ indicates duplicable. Duplicable DNS records belong to the same record set.</div>



<span id="57b06e42"></span>
## When the domain prefix is "@"

When the domain prefix is "@", the conflict situations of DNS records with the same line in the same domain are as follows:


|**Record Type** |**NS** |**CNAME** |**A** |**MX** |**TXT** |**AAAA** |**SRV** |**CAA** |
|---|---|---|---|---|---|---|---|---|
|NS |↔️ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |
|CNAME |✅ |↔️ |❌ |✅ |✅ |❌ |❌ |❌ |
|A |✅ |❌ |↔️ |✅ |✅ |✅ |✅ |✅ |
|MX |✅ |✅ |✅ |↔️ |✅ |✅ |✅ |✅ |
|TXT |✅ |✅ |✅ |✅ |↔️ |✅ |✅ |✅ |
|AAAA |✅ |❌ |✅ |✅ |✅ |↔️ |✅ |✅ |
|SRV |✅ |❌ |✅ |✅ |✅ |✅ |↔️ |✅ |
|CAA |✅ |❌ |✅ |✅ |✅ |✅ |✅ |↔️ |


<span id="b3517792"></span>
## When the domain prefix is not "@"

When the domain prefix is not "@", the conflict situations of DNS records with the same line and the same domain prefix in the same domain are as follows:


|**Record Type** |**NS** |**CNAME** |**A** |**MX** |**TXT** |**AAAA** |**SRV** |**CAA** |
|---|---|---|---|---|---|---|---|---|
|NS |↔️ |❌ |❌ |❌ |❌ |❌ |❌ |❌ |
|CNAME |❌ |↔️ |❌ |❌ |❌ |❌ |❌ |❌ |
|A |❌ |❌ |↔️ |✅ |✅ |✅ |✅ |✅ |
|MX |❌ |❌ |✅ |↔️ |✅ |✅ |✅ |✅ |
|TXT |❌ |❌ |✅ |✅ |↔️ |✅ |✅ |✅ |
|AAAA |❌ |❌ |✅ |✅ |✅ |↔️ |✅ |✅ |
|SRV |❌ |❌ |✅ |✅ |✅ |✅ |↔️ |✅ |
|CAA |❌ |❌ |✅ |✅ |✅ |✅ |✅ |↔️ |


<span id="scenarios-in-which-conflicting-records-in-rfc-1912-can-coexist"></span>
## Scenarios in which conflicting records in RFC 1912 can coexist

<span id="31db227c"></span>
### When the domain prefix is @, CNAME records and NS records can coexist

According to [RFC 1912](https://datatracker.ietf.org/doc/html/rfc1912), CNAME records cannot coexist with other DNS records. However, some websites may have DNS records set for second\-level and third\-level domains. For example, a website has the domain names `www.example.com` and `example.com`. Both domain names are configured with DNS resolution and CDN services. To configure DNS servers and CDN services for `example.com` at the same time, the website administrator needs to create the following DNS records for `example.com`:


* A CNAME record pointing to the CNAME provided by the CDN service.

* An NS record pointing to a third\-party DNS server outside of BytePlus DNS.


To support this scenario, in BytePlus DNS, when the domain prefix is "@" and the same line, CNAME records with the same domain prefix and NS records can coexist. You can use the `dig NS` command to obtain the NS records for domain names that have both CNAME records and NS records.

For example, you have created the following records for the domain name example.com:

```Plain
@.example.com      600           IN    CNAME    abc.example.com.
@.example.com      600           IN    NS       ns1.example.com.
```


You can use the following command to obtain the NS records:

```Shell
dig example.com NS
```


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">BytePlus DNS does not recommend creating CNAME records and NS records at the same time in the same line of the same domain, as CNAME records cannot coexist with other DNS records according to <a href="https://datatracker.ietf.org/doc/html/rfc1912">RFC 1912</a>. If your practice violates RFC 1912, your domain resolution may not work in certain cases.</div>


For example, you have created the following records for the domain name example.com:

```Plain
@.example.com      600           IN    CNAME    abc.example.com.
@.example.com      600           IN    NS       ns1.example.com.
```


You can use the following command to obtain the NS records:

```Plain
dig example.com NS
```


<span id="when-the-domain-prefix-is-cname-records-and-mx-records-can-coexist"></span>
### When the domain prefix is @, CNAME records and MX records can coexist

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">BytePlus does not recommend creating CNAME records and MX records simultaneously in the same line under the same domain name, because according to <a href="https://datatracker.ietf.org/doc/html/rfc1912">RFC 1912</a>, CNAME records cannot coexist with other resolution records. If your practice violates RFC 1912, your domain name resolution may not work in some cases.</div>


<div data-tips="true" data-tips-type="danger">For example, if the Local DNS server used by the email server returns the CNAME record first, email reception may fail.</div>


According to [RFC 1912](https://datatracker.ietf.org/doc/html/rfc1912), CNAME records cannot coexist with other DNS records. However, some websites may configure both CDN services and email services for subdomains. To configure both CDN services and email services for `example.com`, the website administrator needs to create the following DNS records for `example.com`:


* A CNAME record pointing to the CNAME provided by the CDN service.

* One or more MX records pointing to the email server.


To support this scenario, in BytePlus DNS, when the domain prefix is @, CNAME records and MX records can coexist in the same line under the same domain name. For domain names with both CNAME records and MX records, you can use the `dig MX` command to obtain MX records.

For example, you create the following records for the domain name `example.com`:

```plain
@.example.com      600           IN    CNAME    abc.example.com.
@.example.com      600           IN    MX   10   mx1.example.com.
@.example.com      600           IN    MX   10   mx2.example.com.
```


You can use the following command to obtain MX records.

```shell
dig example.com MX
```


<span id="when-the-domain-prefix-is-cname-records-and-txt-records-can-coexist"></span>
### When the domain prefix is @, CNAME records and TXT records can coexist

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">BytePlus does not recommend creating CNAME records and TXT records simultaneously in the same line under the same domain name, because according to RFC 1912, CNAME records cannot coexist with other resolution records. If your practice violates RFC 1912, your domain name resolution may not work in some cases.</div>


<div data-tips="true" data-tips-type="danger">For example:</div>



* <div data-tips="true" data-tips-type="danger">If the TXT record you added is used as an SPF record, the email corresponding to the domain name may not receive emails or the sent emails may be rejected.</div>


* <div data-tips="true" data-tips-type="danger">If the TXT record you added is used to verify domain ownership, the verification may fail.</div>



According to RFC 1912, CNAME records cannot coexist with other resolution records. However, some websites may need to add TXT records as SPF records or to verify domain ownership while configuring CDN services for subdomains. To support this scenario, in BytePlus DNS, when the domain prefix is @, CNAME records and TXT records can coexist in the same line under the same domain name.

<span id="24dc9fee"></span>
## NS records in the same line of the same domain can cause other records to be inactive

If you add an NS record in BytePlus DNS that points to a DNS server of another DNS service provider, this NS record will cause other records to become inactive.

For example, you have created the following records for the domain name example.com:

```Plain
www.test.example.com      600           IN    A        1.1.1.1
shop.test.example.com      600           IN    A        2.2.2.2
forum.test.example.com      600           IN    A        3.3.3.3
test.example.com            600           IN    NS       ns1.example.com.
```


test.example.com is an NS record pointing to a DNS server outside of BytePlus DNS. The resolution records for `www.test.example.com`, `shop.test.example.com`, and `forum.test.example.com` will not take effect.

If you use the following command to query the A records of the domain, you will not get any A records:

```Shell
dig a example.com
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus DNS automatically creates NS records and SOA records for each domain. The NS records contain all the DNS servers of BytePlus DNS. In general, you do not need to change these two records. Therefore, these two records are not displayed in the BytePlus DNS console. If you export the DNS records to a <code>.zone</code> file, you will see the NS records in the <code>.zone</code> file.</div>
