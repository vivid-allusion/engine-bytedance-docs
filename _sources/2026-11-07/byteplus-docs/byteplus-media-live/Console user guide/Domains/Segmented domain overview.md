---
title: "Segmented domain overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/segmented_domain_overview"
---

Segmented domains are intended for live streaming playback over protocols such as `HLS`, `DASH`, `LL-HLS`, and `LL-DASH`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">If you cannot find this feature in the console, contact <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">technical support</a> to enable it.</div>


 &nbsp;

<span id="how-to-choose-a-domain-name-for-stream-pulling"></span>
## How to choose a domain name for stream pulling

You can choose to add a segmented domain or a streaming domain based on your business requirements.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb67beb3049c488e8e834218551b38e7~tplv-goo7wpa0wc-topic.webp) </span>


* If you need pull stream addresses for protocols such as `HLS`, `DASH`, `LL-HLS`, and `LL-DASH` to watch live streams, select a segmented domain.

* If you need pull stream addresses for protocols such as `RTM`, `FLV`, and `RTMP` to watch live streams, select a streaming domain.

* If both types of protocols are required, add both a segmented domain and a streaming domain separately.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">If you are already using pull stream addresses for protocols such as <code>HLS</code>, <code>DASH</code>, <code>LL-HLS</code>, and <code>LL-DASH</code> through a streaming domain, you can continue using the existing addresses. However, to add new pull stream addresses for these protocols in the future, it is recommended to use a segmented domain.</div>


* <div data-tips="true" data-tips-type="tip">To use the adaptive bitrate (ABR) feature, it is recommended to use a segmented domain.</div>



 &nbsp;

<span id="segmented-domain-configuration-page"></span>
## Segmented domain configuration page

You can configure HTTPS, access control, caching, origins, and advanced settings for a segmented domain. The following figures show the configuration pages for segmented domains in the console, helping you quickly understand the configuration scope. For specific configuration methods, see the corresponding documentation.


<Tabs>
<Tab zoneid="fqXUplJsqi" title="HTTPS">
<TabTitle>HTTPS</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23ca2c2f9a27468d865e246bbd8151a8~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
<Tab zoneid="siWZL24O5Q" title="Access control">
<TabTitle>Access control</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ff3cb4544d440f5b011cbdd30aeff66~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
<Tab zoneid="GeB9MDTB5R" title="Caching">
<TabTitle>Caching</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a665256eaef54574aedbcb4642d433f4~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
<Tab zoneid="fKMT8mciYT" title="Origins">
<TabTitle>Origins</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a35611edf5854d1b834e6a04c58751d9~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
<Tab zoneid="bPb7s83gXD" title="Advanced settings">
<TabTitle>Advanced settings</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f90423dd4354712be6317ec6763d0ac~tplv-goo7wpa0wc-topic.webp) </span>


</Tab>
</Tabs>


 &nbsp;

<span id="feature-differences-between-segmented-domains-and-streaming-domains"></span>
## Feature differences between segmented domains and streaming domains

There are differences in the features supported by segmented domains and streaming domains. Even if the supported features are the same, the specific configuration methods may differ. See the corresponding documentation for details.

&nbsp;


|Feature |Description |Segmented domain |Streaming domain |
|---|---|---|---|
|Certificate |Add an SSL certificate to enable HTTPS encryption. |Supported |Supported |
|HTTP/2 protocol |When using an HTTPS pull stream address, the pull stream request is sent over HTTP/2. |Supported |Supported |
|QUIC protocol |When using an HTTPS pull stream address, the pull stream request is sent over QUIC. |Supported |Not supported |
|Forced redirect |Force HTTP pull stream requests to be redirected to HTTPS, or force HTTPS pull stream requests to be redirected to HTTP. |Supported |Not supported |
|OCSP stapling |Return certificate status information directly for HTTPS pull stream requests. |Supported |Not supported |
|HSTS |Instruct browsers to prioritize HTTPS for subsequent pull stream requests. |Supported |Not supported |
|TLS version range |Specify the range of TLS versions that can be used when establishing HTTPS connections. |Supported |Supported |
|IPv6 |Send pull stream requests using IPv6 addresses. |Supported |Not supported |
|Disable HTTP method |Disable pull stream requests using specific HTTP methods. |Supported |Not supported |
|WebSocket |Establish a WebSocket connection between browsers and servers to support bidirectional communication. |Supported |Not supported |
|Proxy protocol |Transmit information, such as the viewer's real IP address, in proxy forwarding scenarios. |Supported |Not supported |
|URL authentication |Set URL signing rules to allow or deny pull stream requests. |Supported |Supported |
|Geographic restrictions |Allow or deny pull stream requests based on the geographic location of the viewer's public IP address. |Supported |Supported |
|IP restrictions |Allow or deny pull stream requests based on IP allowlist or blocklist. |Supported |Supported |
|UA restrictions |Allow or deny pull stream requests based on UA allowlist or blocklist. |Supported |Supported |
|Referer |Allow or deny pull stream requests based on Referer allowlist or blocklist. |Supported |Supported |
|Origin restrictions |Allow or deny pull stream requests based on Origin allowlist or blocklist. |Supported |Not supported |
|Remote authentication |Forward pull stream requests to your authentication server for validation. |Supported |Supported |
|HTTP response headers |Customize the returned HTTP response headers. |Supported |Supported |
|Custom error page |Customize the error page returned when access errors occur. |Supported |Not supported |
|URL normalization |Normalize pull stream request URLs according to rules. |Supported |Not supported |
|Rate limiting |Limit the frequency of pull stream requests. |Not supported |Supported |
|Protocol restrictions |Disable pull stream requests by protocol. |Not supported |Supported |
|Cache rules |Set node cache rules. |Supported |Not supported |
|Cache key |Set whether query parameters are included in the cache key. |Supported |Not supported |
|Status code cache rule |Set error status code cache rules. |Supported |Not supported |
|Browser cache rule |Set browser cache rules. |Supported |Not supported |
|Origin list |Set primary and backup origin servers. |Supported |Not supported |
|Origin protocol |Set the protocol used for requests to the origin. |Supported |Not supported |
|IPv6 Origin |Set whether IPv4 or IPv6 addresses are preferred for requests to an origin configured with a domain name. |Supported |Not supported |
|Origin host |Set the Host header value in requests to the origin. |Supported |Not supported |
|Origin time\-out |Set the timeout for establishing connections to the origin and waiting for content from the origin. |Supported |Not supported |
|HTTP request headers |Set the HTTP request headers for requests to the origin. |Supported |Supported |
|Origin range get |When the origin server supports Range, retrieve content from the origin in segments. |Supported |Not supported |
|Origin redirect follow |Set whether redirects are followed when the origin server returns a 301 or 302 status code. |Supported |Not supported |
|Origin parameter |Set the parameters included in requests to the origin. |Supported |Not supported |
|Origin SNI |Set the SNI domain name used for HTTPS requests to the origin. |Supported |Not supported |
|Origin address rewrite |Rewrite the request path for requests to the origin according to rules. |Not supported |Supported |
|Gop cache |Set the Group of Pictures (GOP) cache duration to balance latency and resilience to network fluctuations. |Not supported |Supported |
|Bandwidth limit |Set the bandwidth limit for pulling streams. |Not supported |Supported |
|HLS/LL\-HLS |Set the segment and low\-latency settings for HLS and LL\-HLS streams. |Supported |Not supported |
|DASH/LL\-DASH |Set the segment and low\-latency settings for DASH and LL\-DASH streams. |Supported |Not supported |
|Address generator |Generate pull stream addresses for corresponding protocols. |Only supports generating HLS, DASH, LL\-HLS, and LL\-DASH pull stream addresses. |Only supports generating RTMP, FLV, and RTM pull stream addresses.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If your streaming domain was created before segmented domains became available, you can still use the address generator to generate HLS, DASH, LL\-HLS, and LL\-DASH pull stream addresses.</div><br> |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Segmented domains and streaming domains use different origin configuration methods. By default, both can be used directly for live streaming playback.</div>


<div data-tips="true" data-tips-type="tip">For custom origin configuration:</div>



* <div data-tips="true" data-tips-type="tip">For segmented domains, origin configuration is based on the domain name.</div>


* <div data-tips="true" data-tips-type="tip">For streaming domains, origin configuration is performed at the stream level, including by specific stream (<code>AppName</code> + <code>StreamName</code>) and by streaming protocol (<code>AppName</code> + streaming protocol). Both on\-demand and scheduled modes are supported.</div>
