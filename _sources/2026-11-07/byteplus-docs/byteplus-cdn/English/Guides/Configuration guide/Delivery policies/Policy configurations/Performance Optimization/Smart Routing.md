---
title: "Smart Routing"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/smart-routing_en-us"
---

Smart Routing optimizes the path between BytePlus CDN edge servers and your origin to reduce origin latency and improve connection reliability for cross\-region traffic.

When a request is not served from the cache, the CDN retrieves content from your origin. Dynamic requests cannot be cached, so each client request triggers an origin request. Non\-cacheable content and content with short cache TTLs also generally result in more origin requests. By default, the CDN uses its standard network path to retrieve content from the origin. In cross\-region or multi\-provider network environments, this path can be affected by changes in public Internet routing quality.

When Smart Routing is enabled, the CDN dynamically selects an available network path with better performance before sending a request to the origin.

<span id="how-smart-routing-works"></span>
## How Smart Routing Works

Smart Routing optimizes only the network path from CDN edge servers to the origin. It does not change how clients connect to the CDN, your existing origin configuration, or origin selection behavior.

When enabled, CDN edge servers run lightweight network probes to the origin. For each domain, the aggregate bandwidth used by all CDN edge servers for probes to the origin is typically less than `100 KB/s`. Based on the probe data, the system evaluates the latency, stability, and path length (hop count) of available routes and selects a better network path for subsequent origin requests.

For example, if your origin is in Europe and users access your service from Asia Pacific, Europe, and the Americas, edge servers in those regions may need to retrieve content from the origin. Smart Routing selects network paths based on real\-time network conditions between each edge server and the origin, helping reduce latency and connection instability caused by fluctuations in public Internet routing quality.

Smart Routing can improve the following metrics:


* Client time to first byte (TTFB).

* Client download speed.

* Origin request success rate.


Overall client\-perceived performance also depends on factors such as cache hit ratio and network quality between clients and CDN edge servers. The benefits of Smart Routing are generally more noticeable when a larger share of requests reaches the origin.

<span id="use-cases"></span>
## Use Cases

Smart Routing is well suited to services with a relatively fixed origin location and geographically distributed users, especially when origin requests from some regions traverse cross\-region or multi\-provider networks.

The following workloads are more likely to benefit from Smart Routing:


* SaaS applications or web APIs served from a centralized origin.

* Global applications that deliver a mix of dynamic and static content.

* File download services that deliver non\-cacheable, short\-lived, or frequently updated content.

* Services that are sensitive to client TTFB, client download speed, or origin request success rate.


For content that can remain cached for long periods, most requests can be served from the CDN cache. Because fewer requests reach the origin, Smart Routing typically provides less benefit.

<span id="considerations"></span>
## Considerations


* Smart Routing applies only when the CDN sends a request to the origin. It does not apply to requests served from the CDN cache.

* Smart Routing selects network paths based on real\-time network probe data. Actual results vary depending on origin location, client access region, and network conditions.


<span id="pricing"></span>
## Pricing

Smart Routing is currently available at no additional charge for a limited time.

<span id="steps"></span>
## Steps


1. Open the **Smart Routing** configuration page. For the steps, see [Domain Management](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to Enabled.


After the configuration takes effect, CDN edge servers use real\-time network probe data to select an available network path with better performance for origin requests.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260814035523-1578476726847.png) </span>
