---
title: "Create DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/tmjP7G"
---

This document describes how to create DNS records for your domain in BytePlus PrivateZone.

Multiple records with the same domain name, line, and type will be merged into a single record set (Record set, RRSet). Within a record set, you can set weights for each DNS record to achieve DNS\-based load balancing. See RRSet in [RFC 7719](https://www.rfc-editor.org/rfc/rfc7719.html).

<span id="prerequisites"></span>
## Prerequisites

You have created a domain. See [Create Domain](https://docs.byteplus.com/docs/byteplus-dns-suite/PU6MMV).

<span id="add-dns-record"></span>
## Create a record set

Follow the steps below to create a record set for your domain. Within a record set, you can add one or multiple DNS records.


1. Open the [BytePlus PrivateZone console](https://console.byteplus.com/dns-suite/dns/privatezone/zones).

2. On the **Domain management** page, select the **Domain management** tab and find your domain. In the **Action** column, click **Manage**.

3. On the **Record management** page, select the **DNS records** tab. Then click **Create record set**.

4. On the **Create record set** page, configure the following parameters.



|Parameter |Description |
|---|---|
|Record type |The type of DNS record included in the record set. See [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/prQAdU). |
|Domain |The domain prefix of the subdomain.<br><br><br>* To route user requests for `www.example.com`, set the domain prefix to `www`.<br><br>* To route user requests for `example.com`, set the domain prefix to `@`.<br><br>* To route user requests for all subdomains of `example.com`, set the domain prefix to `*`.<br><br><br>The rules for the domain are as follows:<br><br><br>* Supports English letters (a\-z, A\-Z), numbers (0\-9), hyphens (\-), underscores (_), periods (.), wildcards (\*), @, and Chinese characters.<br><br>* `-` cannot be used at the beginning or end of a label.<br><br>* Multiple `.` cannot be used consecutively.<br><br>* `@` can only represent an empty domain prefix and cannot coexist with other characters in the domain prefix.<br><br>* `*` can only be used in wildcard domains:<br><br>   * `*` can only replace the leftmost label. For example, `*.example.com` is valid, but `example.*.com` and `abc*.example.com` are not.<br><br>   * Wildcard domains can match domains with the same level and their subdomains. For example, `*.example.com` will match all subdomains of `example.com`, including domains like `abc.example.com` or `abc.def.example.com`, but it will not match `example.com`.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Specific domains affect how wildcard domains match multi\-level subdomains. For example, if both <code>*.example.com</code> and <code>www.example.com</code> exist in the Private Zone:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">DNS queries for domains ending with <code>www.example.com</code> (such as <code>123.www.example.com</code> or <code>abc.www.example.com</code>) will fail to match.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">DNS queries for domains ending with <code>example.com</code> but not <code>www.example.com</code> (such as <code>123.abc.example.com</code>) will match <code>*.example.com</code>.      </div><br>      <br><br>   * Specific domains take precedence over wildcard domains. For example, if a DNS query matches both `*.example.com` and `www.example.com`, and records for both exist, BytePlus PrivateZone will return the record for `www.example.com`.<br><br>* The length of a label should not exceed 63 characters. Under the FQDN format, the total length of the domain should not exceed 254 characters. |
|TTL |The time\-to\-live for the DNS record, with a default value of 10 minutes. The smaller the TTL, the faster the DNS record will take effect after updates. See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/0K0WyX) for TTL limitations. |
|Line |Select a line for the record set. If the record set applies to all subnets of the associated VPC, set this parameter to **Default line**. **Intelligent DNS** must be enabled for this domain when you set this parameter. See [Implement Intelligent DNS](https://docs.byteplus.com/docs/byteplus-dns-suite/-Gvd2s). |
|Load balancing |Whether to enable DNS\-level load balancing for the record set. You must have enabled **Load balancing** when adding the domain to set this parameter. See [Implement Load Balancing](https://docs.byteplus.com/docs/byteplus-dns-suite/s3g1J3).<br><br><br>* **Enabled**: Activates DNS\-level load balancing. If a record set contains multiple record values, each with a weight, then BytePlus PrivateZone will calculate the sum of all weights in the record set and determine the proportion of weight each record value holds. Based on the proportion of weight each record value holds, BytePlus PrivateZone will return that record value in the corresponding proportion of DNS responses.<br><br>   For example, if there is a record set under `www.example.com` containing two record values `10.0.0.1` and `10.0.0.2` with weights of 1 and 3 respectively, and BytePlus PrivateZone receives 100 DNS queries matching this record set, 25 responses will contain `10.0.0.1` and 75 will contain `10.0.0.2`.<br><br>* **Disabled**: Deactivates DNS\-level load balancing. For any DNS query, BytePlus PrivateZone will return all record values in the record set. The order of record values is random. |
|Record value |The record values in the record set. Each record value represents a DNS record. Click **Create record value** to set a record value. You can add multiple record values. See [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/prQAdU) to learn how to add record values for different record types. |
|Weight |The weight of the record value. This parameter is displayed only when **Load balancing** is set to **Enabled**. See [Implement Load Balancing](https://docs.byteplus.com/docs/byteplus-dns-suite/s3g1J3). See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/0K0WyX) for weight limitations. |
|Enabled |Whether this record value is enabled.<br><br><br>* **Enabled**: The record value is included in DNS responses.<br><br>* **Disabled**: The record value is not included in DNS responses. |
|Remark |A remark for the record value. Supports UTF\-8 encoding, with a length not exceeding 16 characters. |



4. After configuring the parameters, click **Submit**. You can view the created DNS records on the **Record management** page.


<span id="next-steps"></span>
## Next Steps

After adding DNS records, you can:


* [Update Record](https://docs.byteplus.com/docs/byteplus-dns-suite/pkPnV9)

* [Delete Record](https://docs.byteplus.com/docs/byteplus-dns-suite/FJHwQW)
