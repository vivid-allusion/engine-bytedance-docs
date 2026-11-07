---
title: "CDN Traffic Theft Risk"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/high-bill_en-us"
---

To prevent malicious CDN traffic theft that can cause unexpectedly high bills and service interruptions, you can implement a multi\-layered defense strategy. This guide provides comprehensive preventive measures, including how to monitor usage with alerts, analyze traffic patterns using logs, and configure various access control features like URL authentication, IP restrictions, and referer restrictions to effectively block unauthorized requests.

<span id="main-risks"></span>
## Main Risks

**High Bills**

CDN billing is based on the volume of data transmitted to users from cache nodes, or the corresponding bandwidth usage. Once your domain is subjected to malicious attacks or theft, the data volume transmitted through your domain via CDN will sharply increase, leading to additional bandwidth consumption. You are responsible for the resulting traffic or bandwidth costs.

**Service Suspension**

If malicious attacks or theft result in an unexpectedly high bill, your account may become overdue, leading to service suspension.

<span id="preventive-measures"></span>
## Preventive Measures

To reduce the risk of your domain being attacked or subjected to traffic theft, we recommend you take the following preventive measures:

<span id="monitor-usage"></span>
### Monitor Usage

You can use BytePlus Cloud Monitor to monitor CDN usage in real time to promptly detect abnormal traffic and bandwidth. Additionally, setting up billing alerts in the Cost Center can effectively reduce losses during attacks or theft. If you have purchased resource packages, you can also set up balance alerts.


|**Alert Capability** |**Description** |
|---|---|
|[Cloud Monitor](https://console.byteplus.com/cloud-monitor) |Monitor traffic and bandwidth and set usage alerts. |
|[Cost Alerts](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2) |On the [Account Overview](https://console.byteplus.com/finance/overview) page, you can set billing amount alerts to help you promptly detect billing anomalies.<br><br><br>* Billing Amount Alert: Set a threshold for your cumulative daily pay\-as\-you\-go bill. You will receive a notification if this threshold is exceeded. |
|Resource Package Remaining Quota Alert |If you have purchased resource packages, you can click **Remaining quota alert** in the upper right corner of the [Resource package](https://console.byteplus.com/finance/resource-package) page, and then set resource package balance alerts to be promptly notified of usage anomalies. |


<span id="traffic-analysis"></span>
### Traffic Analysis

Enable [Log streaming](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-overview_en-us) and [Configure Log Index](https://docs.byteplus.com/en/docs/byteplus-cdn/log-query-examples_en-us).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Real\-time log delivery will incur additional costs. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-pricing#billing-details-pay-as-you-go">Pricing</a>.</div>


When you detect abnormal traffic and bandwidth, you can query the logs to determine the cause to identify the characteristics of the malicious attack or theft event. For example, the source country or region of malicious requests, the time period of the attack, and the IP address range initiating the attack.

<span id="enable-access-control"></span>
### Enable Access Control

Based on the identified characteristics of malicious requests, you can configure features under access control to intercept such requests. These features do not incur additional costs but can effectively reduce risks.


|**Feature** |**Description** |
|---|---|
|[Referer Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-referer-restrictions) |Filter requests based on the Referer header, allowing only requests from specific pages. |
|[Origin Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-restrictions) |Filter requests based on the Origin header, allowing only requests from specific domains. |
|[User-Agent Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ua-restrictions) |Filter requests based on the User\-Agent header, allowing only requests with specific User\-Agent headers. |
|[IP Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ip-restrictions) |Filter requests based on IP addresses, allowing only requests from specific IP addresses. |
|[URL Authentication](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview) |Add a signature to the request URL when the client initiates a request. CDN authenticates the request upon receipt, allowing only authenticated requests. |
|[Remote Authentication](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-remote-authentication_1) |If you have a dedicated authentication server to authenticate user requests, you can configure remote authentication in CDN. |
|[Geographic Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-geographical-restrictions) |Filter requests based on the geographic location of the client's IP address, allowing only requests from specific regions. |
|[Disabled HTTP Methods](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-disallowed-http-method) |Configure disabled HTTP methods in CDN. If CDN receives a user request using a disabled method, it will reject the request and respond with a 405 status code. |
|[Data Rate Throttling](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-data-rate-throttling) |Configure an upper limit on the data transfer speed for requests. You can also specify the time period for enabling this feature. |
|[Custom Restrictions](https://docs.byteplus.com/en/docs/byteplus-cdn/custom-restrictions_en) |Filter requests based on request path, query parameters, and client IP address, allowing only requests that meet the specified conditions. |
