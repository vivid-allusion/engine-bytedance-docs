---
title: "Origin Retry Mechanism"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-retry-logic_en-us"
---

When an origin request to the selected origin server fails, CDN retries the origin request according to the configured retry rules.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN retries an origin request only when the client request method is <code>POST</code>, <code>HEAD</code>, or <code>GET</code>, and the request meets the <a href="https://docs.byteplus.com/en/docs/18/118660#origin-request-failure-criteria">origin request failure criteria</a>.</div>


<span id="origin-retry-process"></span>
## Origin retry process

For each origin request, CDN selects a primary origin server based on its weight.

If the first origin request fails, CDN retries the request once among the primary origin servers:


* If the current primary origin server is a domain name that resolves to multiple IP addresses, CDN selects another available IP address returned by the domain name through round\-robin scheduling.

* In other cases, CDN selects another primary origin server based on the weights of the primary origin servers.


If the retry among primary origin servers also fails and a backup origin server is configured, CDN retries the request once using a backup origin server. If this request also fails, CDN does not initiate further origin retries.

<span id="origin-ip-address-availability-detection"></span>
### Origin IP address availability detection

If CDN cannot establish a TCP connection with an origin IP address for 10 consecutive attempts, CDN marks the IP address as unavailable.

During origin selection, if the selected origin IP address is marked as unavailable, CDN selects another origin server and probes the unavailable IP address asynchronously. If the probe successfully establishes a TCP connection, CDN marks the IP address as available again.

<span id="origin-request-failure-criteria"></span>
### Origin request failure criteria

CDN considers an origin request to have failed in any of the following cases:


* The TCP connection times out or fails.

* The HTTP First Byte Timeout or HTTP Read Timeout is exceeded.

* The origin server returns a 5xx status code or a status code that you specify in [Origin Retry Settings](https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-en).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TCP Timeout, HTTP First Byte Timeout, and HTTP Read Timeout can all cause an origin request to fail. For information about configuring timeouts, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-request-time-out">Origin Fetch Timeouts</a>.</div>
