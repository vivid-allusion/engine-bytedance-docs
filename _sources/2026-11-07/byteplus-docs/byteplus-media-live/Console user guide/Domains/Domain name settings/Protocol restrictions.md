---
title: "Protocol restrictions"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-protocol-restrictions"
---

This page introduces how to limit requests to pull live streams of specific protocols in the BytePlus MediaLive console.

<span id="4cb190c7"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Find the domain name that you want to configure, and click **Settings** in the **Actions** column.

4. Click the **Access control** tab.

5. Click **Edit** to the right of the **Protocol restrictions** toggle.

6. In the **Edit protocol restrictions** dialog box that appears, you can disable specific protocols based on your requirements:

   * **Disable RTMP protocol**: This will block any requests to pull from an address that starts with `rtmp://`.

   * **Disable HLS protocol**: This will block any requests to pull from an address that ends with `.m3u8`.

   * **Disable FLV protocol**: This will block any requests to pull from an address that ends with `.flv`.

   * **Disable WebRTC protocol**: This will block any requests to pull from an address that ends with `.sdp`.

7. Click **Confirm**.
