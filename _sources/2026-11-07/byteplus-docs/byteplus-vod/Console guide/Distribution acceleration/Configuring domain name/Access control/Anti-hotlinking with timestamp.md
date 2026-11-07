---
title: "Anti-hotlinking with timestamp"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-timestamp-"
---

To prevent unauthorized hotlinking of your video content, you can configure timestamp anti\-hotlinking in the BytePlus VOD console. This feature protects your content by setting a validity duration for the playback URLs obtained via the [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) API. This guide provides step\-by\-step instructions for enabling and configuring this setting for your playback domain names.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The timestamp anti\-hotlinking feature applies to <strong>Playback domain</strong> <strong>name</strong>.</div>


<span id="00317037"></span>
## Configuring the timestamp


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration** \> **Domain names** on the left navigation bar.

3. Click the **Playback domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. In the **Anti\-hotlinking with timestamp** section, switch the **Status** toggle and set the validity duration according to your business requirements. The default value is 60 minutes. The validity duration can range from 0 to 5,256,000 minutes (10 years).

8. Click **Save**.
