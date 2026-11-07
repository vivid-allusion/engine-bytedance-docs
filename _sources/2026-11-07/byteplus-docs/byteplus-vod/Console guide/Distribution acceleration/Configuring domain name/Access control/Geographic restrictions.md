---
title: "Geographic restrictions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-geographic-restrictions"
---

To control access to your video content based on user location, you can configure geographic restrictions for your **custom\-origin domain names**.

<span id="ef583104"></span>
## Configuring geographic restrictions


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Geographic restrictions**, switch the **Status** toggle and configure geographic restrictions.

   
   |**Configuration** |**Description** |
   |---|---|
   |Type |The options for this configuration are as follows:<br><br><br>* **Allowlist**: Indicates that only requests from specified regions are allowed to access your domain name.<br><br>* **Blocklist**: Indicates that requests from specified regions are prohibited from accessing your domain name.<br><br><br>If a request matches a blocklist rule or does not match an allowlist rule, BytePlus VOD will reject the request and return a 403 response status code. |
   |Country and region |Specify one or more countries and regions. |
   |Allowing requests from unidentified regions |Specifies whether to allow requests from IP addresses that cannot be resolved to a region. |
   

8. Click **Save**.
