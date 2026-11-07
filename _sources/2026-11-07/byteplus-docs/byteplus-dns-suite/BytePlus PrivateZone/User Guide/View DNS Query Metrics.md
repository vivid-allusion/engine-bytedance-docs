---
title: "View DNS Query Metrics"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/C2hmpr"
---

This document introduces how to view and count the number of DNS queries received by the authoritative DNS server of BytePlus PrivateZone in the console.

<span id="steps"></span>
## Steps

Refer to the following steps to view the DNS query metrics in the console.


1. Open the [DNS Query Metrics](https://console.byteplus.com/dns-suite/privatezone/statistics) page of the BytePlus PrivateZone console.

2. On the **DNS Query Metrics** page, set a query time period.

3. Find the domain name you want to view, and click **Details** in the **Actions** column. You can see the following information:

   * Total DNS query statistics for the domain name.

   * DNS query request statistics grouped by resolution status. The resolution status is indicated by DNS response codes. Refer to [IANA's DNS RCODEs](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6).

   * DNS query request statistics grouped by record type. Refer to [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/prQAdU?type=preview).

4. You can also select VPC ID and subdomain in the dropdown box at the top right. BytePlus PrivateZone filters the DNS query statistics based on the VPC ID and subdomain you select.
