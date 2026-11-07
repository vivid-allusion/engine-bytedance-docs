---
title: "What is an Alias Record"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/What_is_an_Alias_Record"
---

An Alias record points a domain name to a BytePlus cloud resource domain name. An Alias record is a special type of record provided by BytePlus DNS and is not defined in any RFC.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can only create Alias records for domain names with professional or higher editions.</div>


* <div data-tips="true" data-tips-type="tip">Currently, Alias records only support one type of BytePlus cloud resource domain name: the CNAME of BytePlus CDN. If an Alias record points to a CNAME of BytePlus CDN, when BytePlus DNS receives a DNS query matching that Alias record, it will return the IP address of an edge node assigned by CDN.</div>


* <div data-tips="true" data-tips-type="tip">Alias records are included in exported DNS records and backup DNS records, but you cannot import Alias records.</div>



<span id="47f3a94d"></span>
## Differences between Alias records and CNAME records

Alias records and CNAME records have similar functionalities. However, there are the following differences between Alias records and CNAME records.


|Difference\Record type |CNAME record |Alias record |
|---|---|---|
|Functionality |Maps a domain name to any domain name |Maps a domain name to a BytePlus cloud resource domain name |
|DNS record type conflict |* When the domain prefix is @, the DNS record types that conflict with CNAME records under the same domain name and same line are: A, AAAA, SRV, CAA.<br><br>* When the domain prefix is not @, the DNS record types that conflict with CNAME records under the same domain name, same line, and same domain prefix are: NS, A, MX, TXT, AAAA, SRV, CAA. |If the Alias record is added based on A or AAAA records, then:<br><br><br>* When the domain prefix is @, the DNS record type that conflicts with A or AAAA records under the same domain name and same line is: CNAME.<br><br>* When the domain prefix is not @, the DNS record types that conflict with A or AAAA records under the same domain name and same line are: NS, CNAME. |
|Record type specified in DNS query |The record type specified in the DNS query can be any type |* If the Alias record is added based on an A record, then the record type specified in the DNS query must be A.<br><br>* If the Alias record is added based on an AAAA record, then the record type specified in the DNS query must be AAAA. |
|DNS response |The DNS response will show the record type corresponding to the domain name as CNAME |* If the Alias record is added based on an A record, then the DNS response will show the record type corresponding to the domain name as A.<br><br>* If the Alias record is added based on an AAAA record, then the DNS response will show the record type corresponding to the domain name as AAAA. |
