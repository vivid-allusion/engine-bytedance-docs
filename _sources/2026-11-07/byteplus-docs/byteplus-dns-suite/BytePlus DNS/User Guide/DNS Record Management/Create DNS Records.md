---
title: "Create DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records"
---

This document describes how to create DNS records in BytePlus DNS.

BytePlus DNS uses record sets (RRSets) to manage one or more DNS records with the same domain, line, and type. You can set weights for multiple records in a record set to achieve DNS\-based load balancing. See [RFC 7719](https://www.rfc-editor.org/rfc/rfc7719.html) for more information.

<span id="steps"></span>
## Steps

Complete the following steps to create DNS records.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns/publiczone).

2. On the **Domain management** page, click your domain in the **Domain** column.

3. On the **Record management** tab, click **Create record set**.

4. On the **Create record set** page, configure the parameters according to the instructions in the following table.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Record type** |Record type. See [Supported DNS record types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types) for more information. |
   |**Domain** |Subdomain.<br><br><br>* If you want user requests to `www.example.com` to be routed, set the **Domain prefix** to `www`.<br><br>* If you want user requests to `example.com` to be routed, set the **Domain prefix** to `@`.<br><br>* If you want user requests to all single\-level subdomains of `example.com`, such as `abc.example.com`, to be routed, set the **Domain prefix** to `*`.<br><br><br>The requirements for the domain prefix are as follows:<br><br><br>* Supports English letters (a\-z, A\-Z), numbers (0\-9), hyphens (\-), and periods (.).<br><br>* Supports Internationalized Domain Names (IDNs), such as `example.中文网`, `example.닷컴`.<br><br>* Cannot start with a hyphen.<br><br>* Cannot use two consecutive periods.<br><br>* Cannot exceed 63 characters.<br><br>* Supports wildcard (\*) and `@`:<br><br>   * `@` can only represent an empty domain prefix and cannot coexist with other characters in the domain prefix.<br><br>   * `*` can only be used in wildcard domains:<br><br>      * `*` can only replace the leftmost label. For example, `*.example.com` is valid, but `example.*.com` and `abc*.example.com` are not valid.<br><br>      * Wildcard domains can only match domains with the same level. For example, `*.example.com` will match all single\-level subdomains of `example.com`, including domains like `abc.example.com`, but it will not match `example.com` or `abc.def.example.com`.<br><br>      * Specific domains have higher priority than wildcard domains. For example, if a DNS query matches both `*.example.com` and `www.example.com`, and records for both domains exist, BytePlus DNS will return the record for `www.example.com`.<br><br>* There are limitations on the number of subdomain levels. See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) for details.<br><br><br>The number of subdomain levels represents the domain levels of the domain prefix. For example, the number of subdomain levels for `www.example.com` is 1, and the number of subdomain levels for `www.xyz.example.com` is 2. |
   |**TTL** |Expiration time for the record. The default value is 10 minutes. The shorter the TTL, the faster DNS changes propagate. If your DNS records do not change frequently, you can set a longer expiration time. See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) for TTL limitations. |
   |**Line** |Select a line for the record set. If the record set applies to all geolocations and ISPs, set this parameter to **Default line**. By setting the line, you can implement [DNS-based Routing With Lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-intelligent-dns-based-routing) for your domain. |
   |**Load balancing** |Specify whether to enable DNS\-based load balancing among record values.<br><br><br>* **Disable**: Indicates that load balancing is not enabled among record values. BytePlus DNS returns all record values when receiving DNS queries.<br><br>* **Enable**: Indicates that load balancing is enabled among record values. BytePlus DNS returns an appropriate record value based on the load balancing algorithm when receiving DNS queries.<br><br><br>For A, AAAA, and CNAME record types, you can disable load balancing. When load balancing is disabled, BytePlus DNS returns all record values. For other record types, load balancing is enabled by default and cannot be disabled. |
   |**Record value** |Click **Add record value** and set a record value. Each record value represents a DNS record in the record set. You can add multiple record values, which means adding multiple DNS records to a record set. See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) for limitations on the number of record values. See [Supported DNS record types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types) to learn how to add record values for different record types. |
   |**Weight** |Weight of the record value. See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) for weight limitations. |
   |**Enabled** |Whether this record value is enabled.<br><br><br>* **Enabled**: The record value is included in DNS responses.<br><br>* **Disabled**: The record value is not included in DNS responses.<br><br><br>After you disable a record value, some users may still be able to send requests to the record value while others cannot. This is mainly because the expiration time of the cache on different local DNS servers is different. If the cache has not expired, users can still obtain the record value from the cache. If the cache has expired, users will not be able to obtain the record value.<br><br>If you enable a disabled record value, you may encounter similar issues. |
   |**Remark** |The remark for the record value. Supports UTF\-8 encoding. The length should not exceed 16 characters. |
   

5. After configuring the settings, click **Submit**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When creating DNS records, you need to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-avoiding-conflicts-in-dns-records">avoid conflicts in DNS records</a>.</div>
