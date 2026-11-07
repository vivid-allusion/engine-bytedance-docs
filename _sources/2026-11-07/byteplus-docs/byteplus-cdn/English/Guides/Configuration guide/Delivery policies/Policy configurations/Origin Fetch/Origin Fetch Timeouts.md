---
title: "Origin Fetch Timeouts"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-request-time-out"
---

This topic describes how to configure origin fetch timeouts in BytePlus CDN. After you enable origin fetch timeout settings, you can configure timeouts for TCP connection establishment, receiving the first byte of an HTTP response, and reading the HTTP response body.

<span id="origin-fetch-timeouts"></span>
## Origin Fetch Timeouts

When a CDN point of presence (POP) sends a request to an origin server, it establishes a TCP connection, waits for the first byte of the response, and receives the response body. The default timeout values are as follows:


|Setting |Default value |Valid range |Description |
|---|---|---|---|
|TCP Timeout |2 seconds |2–60 seconds |The maximum time that a CDN POP waits to establish a TCP connection with the origin server. If the connection is not established within this period, the connection attempt times out. |
|HTTP Read Timeout |60 seconds |1–900 seconds |After a CDN POP receives the first byte of the origin response, the maximum time it waits without receiving subsequent response body data. The connection is closed when this period is exceeded. |
|HTTP First Byte Timeout |60 seconds |1–900 seconds |After a CDN POP sends an HTTP request to the origin server, the maximum time it waits for the first byte of the response. The connection is closed if the first byte is not received within this period. |


Configure the timeout values based on network conditions and the processing capabilities of your origin server. Note the following:


* A timeout that is too short can cause origin requests to fail frequently because of network fluctuations or long origin processing times.

* A timeout that is too long can keep connections to the origin server open for an extended period and affect its service capacity.

* `HTTP First Byte Timeout` is appropriate when the origin server takes a long time to process requests and cannot begin sending a response promptly.

* `HTTP Read Timeout` is appropriate when the origin server has started sending a response but there are long intervals during response body transmission.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The configured origin fetch timeout represents the theoretical maximum timeout when CDN POPs are operating normally. When conditions such as a sudden increase in origin connections occur for a domain, CDN limits the number of origin connections based on its security policies.</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An origin fetch timeout causes the current origin request to fail. Whether CDN retries the request, and the number of retries, depend on the origin retry configuration and whether the request meets the retry conditions. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/origin-retry-logic_en-us">Origin Retry Mechanism</a>.</div>


<span id="steps"></span>
## Steps


1. Open the **Origin Fetch Timeouts** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enabled**.

3. Configure each timeout in seconds.

   * Configure **TCP Timeout**. The valid range is 2–60.

   * Configure **HTTP Read Timeout**. The valid range is 1–900.

   * Configure **HTTP First Byte Timeout**. The valid range is 1–900.

4. Click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260903083031-965844638717.png) </span>
