---
title: "View DNS Query Metrics"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-viewing-dns-query-metrics"
---

You can use BytePlus DNS to track the number of DNS queries sent by recursive DNS servers to BytePlus DNS authoritative servers. You can track the query metrics for each domain individually.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The available DNS query metrics for your domain depend on the edition of your domain. Please refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions">Editions</a>.</div>


<span id="steps"></span>
## Steps

Follow the steps below to view DNS query metrics.


1. Open the [DNS query metrics](https://console.byteplus.com/dns-suite/dns/publiczone/statistics) in the BytePlus DNS Console.

2. On the **DNS query metrics** page, set a query time period.

3. Find the domain name you want to view, and click **Details** in the **Actions** column. You can see the following information:

   * Total number of DNS queries for the domain name.

   * DNS queries categorized by geolocation. Refer to [Supported Lines](https://docs.byteplus.com/docs-supported-lines).

   * DNS queries categorized by DNS response. The DNS response is indicated by DNS response codes. Refer to IANA's [DNS RCODEs](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6).

   * DNS queries categorized by record type. Refer to [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types).

   * DNS queries categorized by ISP (including cloud providers). Refer to [Supported Lines](https://docs.byteplus.com/docs-supported-lines).

   * DNS queries categorized by **ISP (including cloud vendors) + geolocation**. Refer to [Supported Lines](https://docs.byteplus.com/docs-supported-lines).
