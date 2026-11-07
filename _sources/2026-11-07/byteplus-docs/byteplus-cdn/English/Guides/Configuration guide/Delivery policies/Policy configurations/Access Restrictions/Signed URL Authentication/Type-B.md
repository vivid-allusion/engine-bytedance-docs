---
title: "Type-B"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-type-b"
---

<span id="characteristics"></span>
## Characteristics

Type B places the timestamp and signature before the original path as path prefixes, in that order. Use it when authentication fields must be path prefixes and you need to choose `YYYYMMDDHHMM` (UTC+8), a decimal Unix timestamp, or a hexadecimal Unix timestamp.

<span id="rollout-recommendation"></span>
## Rollout recommendation

First plan a separate test file or directory, validate the client or signing server and CDN configuration, and then add extensions for protected production resources to the applicable scope. This prevents configuration errors from affecting all resources.

<span id="configure-targets"></span>
## Configure Targets

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828092753-655051290321.png) </span>

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828092814-686753610331.png) </span>

Enable **URL Authentication**, select **Type B**, and configure the **Targets** tab. Only matching requests require authentication.


|Item |Behavior |
|---|---|
|Default rule |The default **Path Directory** rule for `/` cannot be deleted. |
|Supported match types |You can retain **Path Directory**, whose value is fixed as `/`, or change the rule to **Path Extension**. |
|Additional rules |Not supported. |
|Match value |For **Path Extension**, enter one or more extensions separated by semicolons (`;`) without periods. For example, `png;txt`. The combined length of matching values cannot exceed 1,024 characters or contain `//`, spaces, `$`, or `?`. |


<span id="configure-url-authentication"></span>
## Configure URL Authentication

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260917094411-1230448252975.png) </span>

The preceding screenshot shows an example configuration with **HLS Manifest Signing** enabled.

On the **Auth Configuration** tab, configure the following parameters.

<span id="basic-parameters"></span>
### Basic parameters


|Setting |Description |
|---|---|
|Primary Key |Required. It must be 1–120 characters long and can contain only English letters, digits, and ASCII half\-width symbols. Spaces, Chinese characters, and full\-width characters are not supported. The client or signing server generates signatures with it; CDN recalculates and compares the signature by the same rules. |
|Backup Key |Optional. If validation with the primary Key fails, CDN calculates and compares the signature again with this Key. It has the same input requirements as the primary Key and supports smooth Key rotation. |
|Signature Validity Period (Seconds) |In seconds. Default: `1800`. Range: 0–315,360,000. CDN considers a URL expired when `timestamp + validity period < time when the request is received`. |
|Signing Algorithm |MD5 or SHA256. Default: MD5. The client or signing server must use the configured algorithm. |


<span id="signature-fields"></span>
### Signature fields


|Setting |Description |
|---|---|
|Timestamp Format |Default: `YYYYMMDDHHMM`. You can select `YYYYMMDDHHMM`, a decimal Unix timestamp, or a hexadecimal Unix timestamp. `YYYYMMDDHHMM` always uses UTC+8. |


When `YYYYMMDDHHMM` is selected, the client or signing server generates the timestamp in UTC+8, regardless of its local time zone. This format is accurate to the minute; during validation, CDN treats the seconds component as `00`. Both Unix timestamp formats are accurate to the second.

<span id="hls-manifest-signing"></span>
## HLS Manifest Signing

Type B supports **HLS Manifest Signing**, which is disabled by default. When enabled, CDN adds Type B signatures to resource URIs in a playlist for HLS playback. Only the `.m3u8` request needs to be signed by the client or signing server.

<span id="rewrite-conditions"></span>
### Rewrite conditions

HLS manifest signing takes effect only when all conditions below are met:


* **Path Extension** in the **Targets** includes `m3u8` and extensions for playlist resources requiring URL authentication. For example, for `.ts` segments and `.mp4` files, configure `m3u8;ts;mp4`.

* The origin response for `.m3u8` does not include `Content-Encoding`, and the `.m3u8` request does not match the scope configured for **File Compression**, because CDN does not rewrite compressed M3U8 files.


Resource URIs can be complete URLs, paths beginning with `/`, or relative paths. CDN resolves a relative URI against the playlist directory and inserts the Type B timestamp and signature at the beginning of the path. For example, `segment-1.ts` in `/b-type-m3u8-rewrite-test/playlist.m3u8` becomes `/<timestamp>/<SIGNATURE>/b-type-m3u8-rewrite-test/segment-1.ts`.

<span id="configure-rewrite-parameters"></span>
### Configure rewrite parameters


|Setting |Description |
|---|---|
|Query Parameters in Segment URIs |Controls whether existing query parameters in playlist resource URIs are retained. |
|Inherit M3U8 Non\-Auth Params |Controls whether query parameters other than signature and timestamp parameters from the `.m3u8` request URL are added to playlist resource URIs. |
|Rewrite Custom Tags |CDN always rewrites resource URIs associated with `EXTINF`. When enabled, you can specify additional tags whose child resource URIs are also rewritten. The playlist must include `EXTINF`; otherwise, CDN does not rewrite resources below the additional tags. You can specify up to 20 custom tags, each 1–100 characters long and without `#` or `:`. |


For `/video.ts?version=1`, if you remove original parameters and enable inheritance, and the `.m3u8` request contains `q_m3u8=cool`, the result is `/<timestamp>/<SIGNATURE>/video.ts?q_m3u8=cool`; if you retain original parameters, it is `/<timestamp>/<SIGNATURE>/video.ts?version=1&q_m3u8=cool`.

<span id="build-a-signed-url"></span>
## Build a signed URL

<span id="url-format"></span>
### URL format

```text
scheme://host/<timestamp>/<SIGNATURE><uri>[?query_params]
```


`uri` starts with `/`, and `timestamp` must use the configured format.

<span id="signature-formula"></span>
### Signature formula

```text
MD5:    md5(key + timestamp + uri)
SHA256: sha256(key + timestamp + uri)
```


`+` means direct concatenation, not a literal character.

<span id="parameters"></span>
### Parameters


|Parameter |Description |
|---|---|
|`key` |The primary Key or Backup Key, used only in signature calculation. |
|`timestamp` |The timestamp in the URL path, in the configured format. |
|`uri` |Original request path beginning with `/`, excluding the domain and query parameters. For Chinese characters, use the encoded path actually sent. |
|`SIGNATURE` |The hash of the string to be signed. |


```text
https://www.example.com/202105061700/2a76bb4719ab4beb77b4746b9c984a1d/product/cdn?query1=value1
```


<span id="cache-and-origin-requests"></span>
## Cache and origin requests

CDN excludes the Type B timestamp and signature from the cache key and removes them before forwarding the request to the origin. This behavior is not configurable.

<span id="verification"></span>
## Verification


1. After saving, select Type B in **Authentication Calculator** and enter a complete, unsigned original URL under the current domain that matches the applicable scope.

2. In **Authentication Calculator**, enter **Auth Key**, **Start Time**, **Validity Period**, **Timestamp Format**, and **Signing Algorithm** to generate an unexpired URL. **Start Time** is used to generate `timestamp`. If a Backup Key is configured, also validate a URL generated with it.

3. Generate the same URL with the client or signing server and compare it with the calculator result. `uri`, `timestamp`, Key, and algorithm must match the calculator settings. When using `YYYYMMDDHHMM`, confirm that the timestamp uses UTC+8. The validity period is not part of signature calculation.

4. Confirm the test file is accessible. Requests with a tampered `SIGNATURE` and requests that use an expired URL must both return 403.

5. Confirm that origin requests do not contain the timestamp and signature in the path.

6. When using HLS, confirm that playlist resource URIs are signed and the related resources are accessible.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828092131-993008417201.png) </span>

<span id="cdn-validation-rules"></span>
## CDN validation rules


* CDN compares lowercase versions of its calculated result and `SIGNATURE`.

* A missing or malformed signature, a mismatched signature, or an expired signature returns 403.


<span id="rollout-and-rollback"></span>
## Rollout and rollback


* For the first rollout, add only the test\-file extension to the applicable scope. Validate the client or signing server, CDN configuration, time synchronization, and HLS playback before gradually expanding the extension scope.

* To rotate a Key, configure the new Key as the Backup Key, validate signatures generated with it, then promote it to the primary Key and retain the old Key as the Backup Key until old URLs expire. If many unexpected 403 responses occur, immediately narrow the scope. If necessary, disable URL authentication and save to restore unsigned access.
