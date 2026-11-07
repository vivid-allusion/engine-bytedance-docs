---
title: "Type-D"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-type-d"
---

<span id="characteristics"></span>
## Characteristics

Type D sends the signature and timestamp in two separate query parameters and calculates the signature in a fixed order. Use it when the fixed calculation order `key + uri + timestamp` is sufficient.

<span id="rollout-recommendation"></span>
## Rollout recommendation

Plan and validate against a separate test file or directory before applying authentication to production resources, so configuration errors do not affect access to all resources.

<span id="configure-targets"></span>
## Configure Targets

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828094308-1694247308674.png) </span>

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828094326-1542148186642.png) </span>

Enable **URL Authentication**, select **Type D**, and configure **Targets**. The default **Path Directory** rule for `/` cannot be deleted. You can change its type and content, add up to 10 rules in total, and combine them using **OR** (default; any condition matches) or **AND** (all conditions match). Only matching requests require authentication.


|Match Type |Match Value / Pattern |
|---|---|
|Path Extension |Extensions separated by `;`, without periods; for example, `png;txt`. |
|Path Directory |Directories separated by `;`; every item begins and ends with `/`, for example `/video/;/image/`. |
|Full Path |Paths separated by `;`, each beginning with `/`. `*` matches one or more characters, including `/`; for example, `/video/*;/image/logo.png`. |
|Full Path Regex |Regular expressions separated by `;`. [Submit a ticket](https://console.byteplus.com/workorder/create) before using this feature. |


Non\-regex rules are case\-insensitive; full\-path regular expressions are case\-sensitive. The combined length of the matching values in a condition must not exceed 1,024 characters. The values cannot contain `//`, spaces, `$`, or `?`.

<span id="configure-url-authentication"></span>
## Configure URL Authentication

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260917095547-1535829088572.png) </span>

On the **Auth Configuration** tab, configure the following parameters.

<span id="basic-parameters"></span>
### Basic parameters


|Setting |Description |
|---|---|
|Primary Key |Required; 1–120 characters; English letters, digits, and ASCII half\-width symbols only. Spaces, Chinese characters, and full\-width characters are not supported. It is used by the client or signing server and CDN to generate signatures using the same rules. |
|Backup Key |Optional. CDN retries validation with the Backup Key if validation with the Primary Key fails. It has the same input requirements and supports smooth Key rotation. |
|Signature Validity Period (Seconds) |Seconds; default `1800`; range 0–315,360,000. The URL expires when `timestamp + validity period < time when the request is received`. |
|Signing Algorithm |MD5 or SHA256; default MD5. The client or signing server must use the same algorithm. |


<span id="signature-fields"></span>
### Signature fields


|Setting |Description |
|---|---|
|Signature Parameter Name |Specifies the query parameter that carries the signature. The default name is `sign`. The name is case\-sensitive, must be 1–100 characters long, may contain letters, digits, `_`, `-`, `.`, `,`, and `!`, and must include at least one letter. |
|Timestamp Parameter Name |Specifies the query parameter that carries the timestamp. The default name is `t`. The name is case\-sensitive, must be 1–100 characters long and may contain letters, digits, `_`, `-`, `.`, `,`, and `!`. |
|Parameter\-name relationship |The **Signature Parameter Name** and **Timestamp Parameter Name** cannot be the same. |
|Timestamp Format |Decimal or hexadecimal Unix timestamp, in seconds. The client or signing server must use the configured timestamp format. |


<span id="hls-manifest-signing"></span>
## HLS Manifest Signing

Type D supports **HLS Manifest Signing**. When enabled, CDN signs playlist resource URIs using Type D to support HLS; only the `.m3u8` request needs to be signed by the client or signing server.

<span id="rewrite-conditions"></span>
### Rewrite conditions

HLS Manifest Signing takes effect only when all of the following conditions are met:


* **Path Extension** in **Targets** includes `m3u8` and the extensions of all protected playlist resources. For example, configure `m3u8;ts;mp4` for `.ts` segments and `.mp4` files. CDN authenticates a resource URI with a matching extension even if it does not match **Path Directory**, **Full Path**, or **Full Path Regex** conditions.

* The origin response for `.m3u8` does not include `Content-Encoding`, and the `.m3u8` request does not match the scope configured for **File Compression**. CDN does not rewrite compressed M3U8 files.


Resource URIs can be complete URLs, absolute paths, or relative paths. A relative resource URI remains relative after rewriting. For example, `segment-1.ts` in `/d-type-m3u8-rewrite-test/playlist.m3u8` becomes `segment-1.ts?<signature parameter name>=<SIGNATURE>&<timestamp parameter name>=<timestamp>`.

<span id="configure-rewrite-parameters"></span>
### Configure rewrite parameters


|Setting |Description |
|---|---|
|Query Parameters in Segment URIs |Controls whether existing query parameters in playlist resource URIs are retained. |
|Inherit M3U8 Non\-Auth Params |Controls whether query parameters other than the signature and timestamp parameters from the `.m3u8` request URL are added to playlist resource URIs. |
|Rewrite Custom Tags |CDN always rewrites resource URIs associated with the `EXTINF` tag. When enabled, you can specify additional tags whose child resource URIs are also rewritten. The playlist must include `EXTINF`; otherwise, CDN does not rewrite resources associated with the additional tags. You can specify up to 20 custom tags, each 1–100 characters long and without `#` or `:`. |


**Query Parameters in Segment URIs** and **Inherit M3U8 Non\-Auth Params** together determine the query parameters in rewritten resource URIs. For example, with resource URI `/video.ts?version=1`, if you remove the original parameters and enable inheritance, and the `.m3u8` request URL contains `q_m3u8=cool`, the rewritten URI is `/video.ts?q_m3u8=cool&<signature parameter name>=<SIGNATURE>&<timestamp parameter name>=<timestamp>`. If you retain the original parameters, it is `/video.ts?version=1&q_m3u8=cool&<signature parameter name>=<SIGNATURE>&<timestamp parameter name>=<timestamp>`.

<span id="build-a-signed-url"></span>
## Build a signed URL

<span id="url-format"></span>
### URL format

```text
scheme://host<uri>?<signature parameter name>=<SIGNATURE>&<timestamp parameter name>=<timestamp>[&...]
```


`sign` and `t` are default names. If you change either name, use the new name in the URL.

<span id="signature-formula"></span>
### Signature formula

```text
MD5:    md5(key + uri + timestamp)
SHA256: sha256(key + uri + timestamp)
```


`+` means direct concatenation, not a literal character.

<span id="parameters"></span>
### Parameters


|Parameter |Description |
|---|---|
|`key` |Primary Key or Backup Key; used only for signature calculation. |
|`uri` |Request path beginning with `/`, excluding domain and query parameters; use the encoded path actually sent for Chinese characters. |
|`timestamp` |Decimal or hexadecimal Unix timestamp in the configured format. |
|`SIGNATURE` |Hash of the string to be signed. |


```text
https://www.example.com/product/cdn?sign=e954e253c33634b510443af72406600f&t=1620291453&query1=value1
```


<span id="cache-and-origin-requests"></span>
## Cache and origin requests

CDN excludes the Type D signature and timestamp parameters from the cache key and removes them before forwarding the request to the origin. This behavior is not configurable.

<span id="verification"></span>
## Verification


1. After saving, use **Authentication Calculator** to select **Type D** and enter a complete, unsigned original URL under the current domain that matches the applicable scope.

2. In **Authentication Calculator**, enter **Auth Key**, **Signature Parameter**, **Timestamp Parameter**, **Start Time**, **Validity Period**, **Timestamp Format**, and **Signing Algorithm** to generate an unexpired URL. **Start Time** is used to generate `timestamp`. If a Backup Key is configured, also validate a URL generated with the Backup Key.

3. Generate the same URL with the client or signing server and compare it with the calculator result. `uri`, `timestamp`, Key, and algorithm must match the calculator settings; the validity period is not part of signature calculation.

4. Confirm that the test file is accessible. Requests with a tampered `SIGNATURE` and requests that use an expired URL must both return 403.

5. Confirm that origin requests do not include the signature and time parameters.

6. When using HLS, confirm that playlist resource URIs are signed and the related resources are accessible.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828092536-1100347190249.png) </span>

<span id="cdn-validation-rules"></span>
## CDN validation rules


* CDN compares lowercase versions of its calculated signature and `SIGNATURE`.

* A missing or malformed signature, a mismatched signature, or an expired signature returns 403.


<span id="rollout-and-rollback"></span>
## Rollout and rollback

For the first rollout, limit the applicable scope to test files or directories. Validate the client or signing server, CDN configuration, time synchronization, origin behavior, and HLS playback before gradually expanding the scope.

To rotate a Key, configure the new Key as the Backup Key, validate signatures generated with it, then promote it to the primary Key and retain the old Key as the Backup Key until old URLs expire. If many unexpected 403 responses occur, immediately narrow or delete the scope. If necessary, disable URL authentication and save the configuration to restore unsigned access.
