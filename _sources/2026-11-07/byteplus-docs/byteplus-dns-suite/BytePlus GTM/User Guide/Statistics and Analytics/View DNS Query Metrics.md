---
title: "View DNS Query Metrics"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/GeqPrU"
---

This document describes how to view DNS query statistics in BytePlus GTM.

<span id="how-byteplus-gtm-collects-dns-query-data"></span>
## How BytePlus GTM collects DNS query data

You can use **CNAME** or **Domain from BytePlus DNS** to connect a GTM instance to your domain. For different connection methods, BytePlus GTM collects DNS query data differently. Suppose your domain is `example.com`.


* CNAME: You need to use an authoritative DNS service, such as AWS Route53, to resolve `example.com` as a CNAME record to the routing domain `example.com.byteplus.com`. BytePlus GTM resolves the routing domain `example.com.byteplus.com` to the target address you set. Therefore, BytePlus GTM can only collect DNS query data for `example.com.byteplus.com`, not for `example.com`.

* Domain from BytePlus DNS: You enable DNS service for `example.com` in BytePlus DNS and set `example.com` as the domain of the GTM instance in BytePlus GTM. BytePlus GTM replaces BytePlus DNS to resolve `example.com` to the target address you set. Therefore, DNS query data for `example.com` is collected in BytePlus GTM.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In BytePlus DNS, you cannot create A, AAAA, or CNAME records under <code>example.com</code>. However, you can still create other types of records under <code>example.com</code>, such as MX records or TXT records. DNS query data for these records will be collected in BytePlus GTM and billed accordingly.   </div>
   

Refer to [Create a GTM Instance](https://docs.byteplus.com/docs/byteplus-dns-suite/k_FIn3) to learn about different connection methods for BytePlus GTM.

<span id="view-dns-query-statistics-on-the-dns-query-metrics-page"></span>
## View DNS query statistics on the DNS query metrics page

Follow these steps to view DNS query statistics on the **DNS query metrics** page.


1. Open the [DNS query metrics](https://console.byteplus.com/dns-suite/gtm/statistics) page of BytePlus GTM.

2. The **DNS query metrics** page displays statistics for all DNS queries. You can group the statistics by status, type, ISP, and geolocation.

   * **Status**: Statistics of DNS queries categorized by status. The status is indicated by DNS response codes. Refer to IANA's [DNS RCODEs](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6).

   * **Type**: Statistics of DNS queries categorized by type. Refer to [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types).

   * **ISP**: Statistics of DNS queries categorized by ISP. Refer to [Supported lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines). **OTHER** indicates that the ISP is not in the [Supported lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines).

   * **Geolocation**: Statistics of DNS queries categorized by geolocation. Refer to [Supported lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines).


<span id="viewing-dns-query-statistics-on-the-overview-page"></span>
## Viewing DNS query statistics on the overview page

Follow these steps to view DNS query statistics on the **Overview** page.


1. Open the [Overview](https://console.byteplus.com/dns-suite/gtm/overview) page of BytePlus GTM.

2. In the **Data Statistics** section, you can see the following statistics:

   * **Number of instances**: The total number of GTM instances created by the current account.

   * **Number of health check tasks**: The number of health check tasks for all GTM instances.

   * **Number of pools**: The total number of address pools for all GTM instances.

   * **Healthy/Unhealthy addresses**: The number of addresses with health check results indicating availability and unavailability.

   * **Number of billed DNS queries this month**: The number of DNS queries for all GTM instances. BytePlus GTM calculates fees based on the number of DNS queries. Refer to [Billing](https://docs.byteplus.com/docs/byteplus-dns-suite/R4Anoj).

3. In the **Trend of total number of DNS queries** section, select the time range and the domain of the GTM instance. You can see the number of DNS queries for each GTM instance within the selected time range.
