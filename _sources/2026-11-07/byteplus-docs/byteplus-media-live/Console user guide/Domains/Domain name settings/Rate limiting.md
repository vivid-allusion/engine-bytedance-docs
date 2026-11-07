---
title: "Rate limiting"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rate-limiting"
---

You can configure the frequency limit for pull streaming requests associated with a specific domain name. You can use **Rate limiting** to mitigate the risk of Challenge Collapsar (CC) attacks.

Exercise caution when using this feature, as setting the rate limit too low may result in legitimate requests being unintentionally blocked. Therefore, it is recommended to carefully consider and test the appropriate rate limit to strike a balance between security and accessibility.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The frequency limit is applied per edge cluster, rather than across the entire network. To illustrate, consider a scenario where the frequency limit for requests sent from a particular IP address is set at 50 per second. If both cluster A and cluster B receive 50 requests from an IP address within a second, no errors will occur. However, if cluster A receives 101 requests while cluster B still receives 50 requests within the same second, any subsequent requests sent from that IP address and received by cluster A will be blocked during the rejection period. Cluster B, on the other hand, will remain unaffected.</div>


<span id="04013d7d"></span>
## Procedure

Follow the instructions below to configure a frequency limit for a domain name in the BytePlus MediaLive console:


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Find the domain name that you want to configure, and click **Settings** in the **Actions** column.

4. Click the **Access control** tab.

5. Click **Edit** to the right of the **Rate limiting** toggle.

6. In the **Edit rate limiting** dialog box that appears, configure the following parameters.

   * **Restriction type**:

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Options including <strong>Request rate to a URL</strong>, <strong>Request rate to URLs with a specified query</strong>, and <strong>Request rate to a URL from an IP address</strong> are hidden by default. Contact your <a href="https://www.byteplus.com/en/support">technical support</a> to enable the display of this option.      </div>
      

      * **Request rate from an IP address**: Limit the frequency of requests sent from an individual IP address.

      * **Request rate to a URL**: Limit the frequency of requests sent to an individual URL.

      * **Request rate to URLs with a specified query**: Limit the frequency of requests sent to URLs containing a specified query parameter.

      * **Request rate to a URL from an IP address**: Limit the frequency of requests sent to the same URL from an individual IP address.

   * **Limit**: The maximum number of requests allowed within a second or a minute.

7. Click **Confirm**.
