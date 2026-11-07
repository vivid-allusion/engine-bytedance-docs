---
title: "Referer"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-referer"
---

You can configure a referer blocklist or allowlist to control access to your content and protect it from unauthorized access.

Follow the instructions below to configure a referer blocklist or allowlist in the BytePlus MediaLive console.


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Find the domain name that you want to check out, and click **Settings** in the **Actions** column.

4. Click the **Access control** tab.

5. Click **Edit** to the right of the **Referer** toggle.

6. In the **Edit** **referer** dialog box that appears, **Referer** is turned on automatically. Configure the following parameters.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_676d7c240bb772dff671d1d148cfb24b.png) </span>



|Parameter |Description |
|---|---|
|Referer type |Select **Blocklist** or **Allowlist**. If you select **Blocklist**, requests from the domain names or wildcard domain names in the blocklist cannot access resources. If you select **Allowlist**, only requests from the domain names or wildcard domain names in the allowlist are allowed to access resources. |
|Referer rules |Supports adding a complete domain name or wildcard domain name as a rule. Currently, a maximum of 100 rules can be configured. The configuration examples are as follows (taking the configuration of the domain name www.example.com as an example).<br><br><br>* When configuring `www.example.com`, only `www.example.com` can be matched. `http(s)://www.example.com`, `www.example.com/`, and `http(s)://www.example.com/path` cannot be matched.<br><br>* When configuring `*.example.com`, `http(s)://www.example.com` can be matched, but `http(s)://www.example.com/` cannot be matched.<br><br>* When configuring `*.example.*`, `www.example.com`, `http(s)://www.example.com`, `www.example.com/`, and `http(s)://www.example.com/path` can be matched.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to configure more than 100 rules, please <a href="https://www.byteplus.com/en/support">contact support</a>.</div><br> |



7. Click **Confirm**.
