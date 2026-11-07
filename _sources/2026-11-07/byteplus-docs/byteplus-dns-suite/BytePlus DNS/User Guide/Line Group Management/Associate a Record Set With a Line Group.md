---
title: "Associate a Record Set With a Line Group"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/V7FRGD"
---

This document introduces how to associate a line group with a DNS record set.

<span id="steps"></span>
## Steps

When creating or updating a DNS record set, you set the **Line** parameter of the record set to **Line group** and select the line group you created.

Refer to [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records) and [Update DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/JzsSrJ).

<span id="supported-domain-names-for-line-groups"></span>
## Supported domain names for line groups

When you associate a line group with a DNS record set for a domain name, the line types included in the line group must be supported by the current edition of the domain name. Otherwise, you cannot associate the line group with the DNS record set for that domain name.

For example, if a line group includes China Mobile and China Dr. Peng, and the edition of your domain name is professional edition, then the DNS record set under that domain name cannot be associated with the line group. However, if the edition of your domain name is ultimate edition, then the DNS record set under that domain name can be associated with the line group.

<span id="priority-of-line-groups"></span>
## Priority of line groups

The priority of a line group depends on the priority of the lines included in the line group. Refer to [Priority in DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-priority-in-dns-records).
