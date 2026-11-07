---
title: "Type-C"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-type-c"
---

<span id="characteristics"></span>
## Characteristics

Type C places the signature and a hexadecimal Unix timestamp before the original path, in that order. Use it when authentication information must be carried in the path and the timestamp must use a hexadecimal Unix timestamp.

<span id="rollout-recommendation"></span>
## Rollout recommendation

First, use a separate test file or directory to validate the client or signing server and the CDN configuration. Then add protected production\-resource extensions to the applicable scope to avoid affecting all resources.

<span id="configure-targets"></span>
## Configure Targets

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828094112-1187386092569.png) </span>

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828094124-44088582038.png) </span>

Enable **URL Authentication**, select **Type C**, and configure **Targets**. Only matching requests require authentication.


|Item |Behavior |
|---|---|
|Default rule |The default **Path Directory** rule for `/` cannot be deleted. |
|Supported match types |You can retain **Path Directory**, whose value is fixed as `/`, or change the rule to **Path Extension**. |
|Additional rules |Not supported. |
|Match value |For **Path Extension**, enter one or more extensions separated by semicolons (`;`) without periods. For example, `png;txt`. The combined length of matching values cannot exceed 1,024 characters or contain `//`, spaces, `$`, or `?`. |


<span id="configure-url-authentication"></span>
## Configure URL Authentication

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260917095502-635288463032.png) </span>

On the **Auth Configuration** tab, configure the following parameters.

<span id="basic-parameters"></span>
### Basic parameters


|Setting |Description |
|---|---|
|Primary Key |Required; 1–120 characters. It supports English letters, digits, and ASCII half\-width symbols only; spaces, Chinese characters, and full\-width characters are not supported. The client or signing server generates signatures with it, and CDN recalculates and compares them. |
|Backup Key |Optional. If validation with the Primary Key fails, CDN validates again with the Backup Key. It has the same input requirements and supports smooth Key rotation. |
|Signature Validity Period (Seconds) |Seconds; default `1800`; range 0–315,360,000. A URL expires when `timestamp + validity period < time when the request is received`. |
|Signing Algorithm |MD5 or SHA256; default MD5. The client or signing server must use the configured algorithm. |


<span id="signature-fields"></span>
### Signature fields


|Setting |Description |
|---|---|
|Timestamp Format |Fixed as a hexadecimal Unix timestamp in seconds. `timestamp` in both the URL and signature formula must use this format. |


<span id="hls-manifest-signing"></span>
## HLS Manifest Signing

Type C supports **HLS Manifest Signing**. When enabled, CDN uses Type C signing to add signatures to playlist resource URIs for HLS playback; only the `.m3u8` request needs to be signed by the client or signing server.

<span id="rewrite-conditions"></span>
### Rewrite conditions

HLS Manifest Signing takes effect only when both of the following conditions are met:


* **Path Extension** includes `m3u8` and the extensions of all protected playlist resources. For example, configure `m3u8;ts;mp4` for `.ts` and `.mp4` resources. CDN authenticates a playlist resource URI whenever its file extension matches.

* The origin response for `.m3u8` does not include `Content-Encoding`, and the `.m3u8` request does not match the scope configured for **File Compression**. CDN does not rewrite compressed M3U8 files.


Resource URIs can be complete URLs, absolute paths, or relative paths. CDN resolves a relative URI relative to the playlist directory, then inserts the signature and timestamp at the beginning of the path. For example, `segment-1.ts` in `/c-type-m3u8-rewrite-test/playlist.m3u8` becomes `/<SIGNATURE>/<timestamp>/c-type-m3u8-rewrite-test/segment-1.ts`.

<span id="configure-rewrite-parameters"></span>
### Configure rewrite parameters


|Setting |Description |
|---|---|
|Query Parameters in Segment URIs |Retains or removes existing query parameters in playlist resource URIs. |
|Inherit M3U8 Non\-Auth Params |Adds `.m3u8` request query parameters other than signature and timestamp parameters to playlist resource URIs. |
|Rewrite Custom Tags |CDN always rewrites resource URIs associated with `EXTINF`. When enabled, you can specify additional tags whose child resource URIs are also rewritten. The playlist must contain `EXTINF`, otherwise resources below additional tags are not rewritten. A maximum of 20 custom tags is allowed; each is 1–100 characters and cannot contain `#` or `:`. |


For `/video.ts?version=1`, removing original parameters and enabling inheritance with `q_m3u8=cool` produces `/<SIGNATURE>/<timestamp>/video.ts?q_m3u8=cool`; retaining them produces `/<SIGNATURE>/<timestamp>/video.ts?version=1&q_m3u8=cool`.

<span id="build-a-signed-url"></span>
## Build a signed URL

<span id="url-format"></span>
### URL format

```text
scheme://host/<SIGNATURE>/<timestamp><uri>[?query_params]
```


`uri` starts with `/`; `timestamp` is a hexadecimal Unix timestamp.

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
|`key` |Primary Key or Backup Key; used only in signature calculation. |
|`uri` |Original request path, beginning with `/` and excluding domain and query parameters; use the encoded path actually sent for Chinese characters. |
|`timestamp` |Hexadecimal Unix timestamp in seconds. |
|`SIGNATURE` |Hash of the string to be signed. |


```text
https://www.example.com/b1725c0a6120092863001cd8004c4adb/6093AF7D/product/cdn?query1=value1
```


<span id="cache-and-origin-requests"></span>
## Cache and origin requests

CDN excludes the Type C timestamp and signature from the cache key and removes them before forwarding the request to the origin. This behavior is not configurable.

<span id="verification"></span>
## Verification


1. After saving, use **Authentication Calculator** to select **Type C** and enter a complete, unsigned original URL under the current domain that matches the applicable scope.

2. In **Authentication Calculator**, enter **Auth Key**, **Start Time**, **Validity Period**, and **Signing Algorithm** to generate an unexpired URL. **Start Time** is used to generate `timestamp`. If a Backup Key is configured, also validate a URL generated with the Backup Key.

3. Generate the same URL with the client or signing server and compare it with the calculator result. `uri`, `timestamp`, Key, and algorithm must match the calculator settings; the validity period is not part of signature calculation.

4. Confirm the test file is accessible; tampered `SIGNATURE` requests and expired URLs must return 403.

5. Confirm origin requests exclude the path timestamp and signature.

6. For HLS, confirm playlist resource URIs are signed and accessible.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828092456-121916094412.png) </span>

<span id="cdn-validation-rules"></span>
## CDN validation rules


* CDN compares lowercase versions of its calculated signature and `SIGNATURE`.

* A missing or malformed signature, a mismatched signature, or an expired signature returns 403.


<span id="rollout-and-rollback"></span>
## Rollout and rollback

For the first rollout, add only the test\-file extension to the applicable scope. Validate the client or signing server, CDN configuration, time synchronization, and HLS playback before gradually expanding the extension scope.

To rotate a Key, configure the new Key as the Backup Key, validate signatures generated with it, then promote it to the primary Key and retain the old Key as the Backup Key until old URLs expire. If many unexpected 403 responses occur, immediately narrow the scope. If necessary, disable URL authentication and save the configuration to restore unsigned access.
