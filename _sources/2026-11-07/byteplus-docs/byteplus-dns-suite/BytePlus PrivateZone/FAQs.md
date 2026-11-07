---
title: "FAQs"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/mb-xVa"
---

This document includes the frquently asked questions of BytePlus PrivateZone.

<span id="failed-to-import-dns-records-to-byteplus-privatezone"></span>
## Failed to import DNS records to BytePlus PrivateZone

For each failed DNS record import, the console will display the reason for the failure. You can refer to the following troubleshooting steps based on the failure reason.

<span id="issue-domain-name-is-invalid"></span>
### Issue: Domain name is invalid

You need to check if the complete domain name meets the following rules:


* Only English letters (a\-z, A\-Z), numbers (0\-9), hyphens (\-), underscores (_), periods (.), asterisks (\*), @, and simplified Chinese characters are supported.

* Hyphens cannot be used at the beginning or end of a label, and periods cannot be used consecutively.

* @ can only be used alone to represent an empty value.

* Asterisks (\*) can only be used at the beginning of a label for wildcard resolution.

* The length of a label should not exceed 63 characters.

* The total length of the domain name should not exceed 255 characters.


Also, make sure that the subdomain in the DNS record matches the target domain for the record import. For example, if the target domain for the record import is example.com, and you have the following record in your file:

```text
test.sample.com   www   A   default   600   1.1.1.1   Yes
```


The console will return a "Domain name is invalid" error.

<span id="issue-the-record-duplicates-an-existing-record"></span>
### Issue: The record duplicates an existing record

You need to check if the following issues exist:


* The DNS records in the file are duplicates of the records in the console.

* There are duplicate DNS records in the file.


<span id="why-can-t-i-set-weights-for-record-values-in-the-console"></span>
## Why can't I set weights for record values in the console?

If you did not enable load balancing when creating the domain name, the console will not display weight\-related settings when creating resolution records under that domain name. Refer to [Implement Load Balancing](https://docs.byteplus.com/docs/byteplus-dns-suite/s3g1J3).

<span id="will-the-dns-records-of-a-domain-name-take-effect-in-a-vpc-that-is-not-associated-with-the-domain-name"></span>
## Will the DNS records of a domain name take effect in a VPC that is not associated with the domain name?

No. You must first associate the VPC with the domain name for the DNS records of the domain name to take effect in that VPC. Refer to [Create a Domain](https://docs.byteplus.com/docs/byteplus-dns-suite/9iX1X2) to learn how to associate a domain name with a VPC.

You can view the VPC currently associated with the domain name on the **Domain information** tab. Refer to [Update Domain Configuration](https://docs.byteplus.com/docs/byteplus-dns-suite/PU6MMV).

<span id="26d4007c"></span>
## Does BytePlus PrivateZone support EDNS?

EDNS is an extension mechanism of the DNS protocol used to address the issue of insufficient DNS message length affecting information transmission efficiency.

<span id="edns-versions-supported-by-byteplus-privatezone"></span>
### EDNS versions supported by BytePlus PrivateZone

BytePlus PrivateZone only supports `EDNS(0)`. Refer to [RFC 6891](https://www.rfc-editor.org/rfc/rfc6891.html). For other versions of EDNS, BytePlus PrivateZone will return the response code `BADVERS`.

<span id="edns-option-codes-supported-by-byteplus-privatezone"></span>
### EDNS Option Codes supported by BytePlus PrivateZone

BytePlus PrivateZone does not support the following EDNS Option Codes. If a DNS query request contains unsupported Option Codes, these Option Codes will be discarded.


* 8

* 18

* 65001 ~ 65534
