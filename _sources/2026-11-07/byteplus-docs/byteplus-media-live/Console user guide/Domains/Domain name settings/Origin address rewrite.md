---
title: "Origin address rewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite"
---

When pulling a live stream from a third\-party origin server, as explained in [Configuring an origin-pull task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings), there might be instances where the origin address changes over time. To cater to this, you can use the origin address rewrite feature, which enables fetching the stream from a new address based on predefined matching rules.

<span id="8ae1c921"></span>
## Limitations

This feature is applicable to on\-demand origin pull tasks only. It supports streams that use the FLV, HLS, and RTMP protocols.

<span id="1ec9696b"></span>
## Procedure

Follow the instructions below to configure an origin address rewrite in the BytePlus MediaLive console:


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Find the domain name that you want to configure, and click **Settings** in the **Actions** column.

4. Click the **Origin pull** tab.

5. Click **Edit** to the right of the **Origin address rewrite** toggle.

6. In the **Origin address rewrite** dialog box that appears, configure the rewrite rules. You can configure a maximum of 50 rewrite rules. The order of the rewrite rules indicates the priority of the rule. If there are multiple rules, they are executed based on their priority. If one rule matches the user request, the remaining rules will not be executed.

   * **Existing path**: The original path. The path may include a maximum of five wildcards. However, do not use wildcards to represent query parameters.

   * **Target path**: The new path. You can use `${1}`, `${2}`, `${3}`, `${4}`, and `${5}` to represent the content matched by the first to the fifth wildcards respectively.

      The existing and target paths must also satisfy the following requirements:

   * The path must not contain the protocol and domain name, such as `http://example.domain.com`.

   * The path must start with `/`.

   * The path can contain a maximum of 1,024 characters.

   * The path cannot contain two consecutive asterisks like `**`.

   * The path cannot contain two consecutive instances like `${${`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To query origin pull data, use the existing path instead of the new path.</div>


<span id="cdb378e7"></span>
## Example

Suppose the existing path is set to `/app/*/*/playlist.m3u8` and the target path is set to `/abc/${1}/${2}.m3u8`, the original request `http://www.test.com/app/123/test/playlist.m3u8` will be rewritten as `http://www.test.com/abc/123/test.m3u8`.
