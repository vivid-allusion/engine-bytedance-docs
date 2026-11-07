---
title: "Type-A"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-type-a"
---

<span id="characteristics"></span>
## Characteristics

Type A combines the timestamp, random string, and signature into the value of one query parameter. Use it when all authentication information must be carried in a single query parameter.

<span id="rollout-recommendation"></span>
## Rollout recommendation

Plan a separate test file or directory first. Validate the client or signing server and CDN configuration before configuring the applicable scope for production resources that require authentication. This reduces the risk that a configuration error affects access to all resources.

<span id="configure-targets"></span>
## Configure Targets

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828091419-99985263775.png) </span>

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828091144-1401132106815.png) </span>

Enable **URL Authentication**, select **Type A**, and configure the **Targets** tab. The default **Path Directory** rule for `/` cannot be deleted. You can change its type and content, or add rules, with a maximum of 10 rules. Combine multiple rules with **OR** (the default; any condition matches) or **AND** (all conditions match). Only matching requests require authentication.


|Match Type |Match Value / Pattern |
|---|---|
|Path Extension |One or more extensions separated by semicolons (`;`), without periods. For example, `png;txt`. |
|Path Directory |One or more directories separated by semicolons; each item starts and ends with `/`. For example, `/video/;/image/`. |
|Full Path |One or more paths separated by semicolons (`;`); each item starts with `/`. You can use `*` to match one or more characters, including `/`. For example, `/video/*;/image/logo.png`. |
|Full Path Regex |One or more regular expressions separated by semicolons. [Submit a ticket](https://console.byteplus.com/workorder/create) to enable this feature before use. |


Non\-regular\-expression rules are case\-insensitive, while full\-path regular expressions are case\-sensitive. The combined length of matching values in a single condition cannot exceed 1,024 characters and cannot contain `//`, spaces, `$`, or `?`.

<span id="configure-url-authentication"></span>
## Configure URL Authentication

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260917094313-976414087785.png) </span>

Configure the following parameters on the **Auth Configuration** tab.

<span id="basic-parameters"></span>
### Basic parameters


|Setting |Description |
|---|---|
|Primary Key |Required. It must be 1–120 characters long and can contain only English letters, digits, and ASCII half\-width symbols. Spaces, Chinese characters, and full\-width characters are not supported. The client or signing server uses it to generate signatures; CDN calculates a signature by the same rules and compares it with the request signature. |
|Backup Key |Optional. If the signature calculated with the primary Key does not match the request signature, CDN calculates and compares it again with the Backup Key using the same rules. It has the same input requirements as the primary Key. Use it for smooth Key rotation. |
|Signature Validity Period (Seconds) |In seconds. The default is `1800`; the range is 0–315,360,000. CDN considers a URL expired when `timestamp + validity period < time when the request is received`. |
|Signing Algorithm |MD5 or SHA256. The default is MD5. The client or signing server must use the same algorithm as the CDN configuration. |


<span id="signature-fields"></span>
### Signature fields

`rand` and `uid` are not configured in the console. The client or signing server includes them in the signature parameter value, and CDN parses them when validating the signature.


|Setting |Description |
|---|---|
|Signature Parameter Name |Specifies the query parameter that carries the complete authentication value. The default name is `sign`. The name is case\-sensitive, must be 1–100 characters long, may contain letters, digits, `_`, `-`, `.`, `,`, and `!`, and must include at least one letter. |
|Timestamp Format |Specifies a decimal Unix timestamp in seconds. |


<span id="hls-manifest-signing"></span>
## HLS Manifest Signing

Type A supports **HLS Manifest Signing**. When enabled, CDN adds signatures to resource URIs in a playlist using Type A signing, enabling HLS playback. The client or signing server needs to generate a signature only for the `.m3u8` request.

<span id="rewrite-conditions"></span>
### Rewrite conditions

After HLS Manifest Signing is enabled, CDN rewrites resource URIs only when all of the following conditions are met:


* **Path Extension** in the **Targets** includes `m3u8` and the extensions of resources in the playlist that need URL authentication. For example, if a playlist references `.ts` segments and `.mp4` files, set **Path Extension** to `m3u8;ts;mp4`. CDN performs URL authentication whenever a playlist resource URI has a matching file extension, even if it does not match other target conditions.

* The origin response for `.m3u8` does not include `Content-Encoding`, and the `.m3u8` request does not match the scope configured for **File Compression**, because CDN does not rewrite compressed M3U8 files.


Playlist resource URIs can be complete URLs, paths beginning with `/`, or relative paths. A relative resource URI remains relative after rewriting.

For example, if the playlist path is `/a-type-m3u8-rewrite-test/playlist.m3u8` and a resource URI is `segment-1.ts`, it is rewritten as `segment-1.ts?<signature parameter name>=<timestamp>-<rand>-0-<SIGNATURE>`.

<span id="configure-rewrite-parameters"></span>
### Configure rewrite parameters


|Setting |Description |
|---|---|
|Query Parameters in Segment URIs |Controls whether existing query parameters in playlist resource URIs are retained. |
|Inherit M3U8 Non\-Auth Params |Controls whether query parameters other than the signature parameter from the `.m3u8` request URL are added to playlist resource URIs. |
|Rewrite Custom Tags |CDN always rewrites resource URIs associated with the `EXTINF` tag. When enabled, you can specify additional tags whose child resource URIs are also rewritten. The playlist must include the `EXTINF` tag; otherwise, CDN does not rewrite resources under the specified additional tags. You can specify up to 20 custom tags. Each tag must be 1–100 characters long and cannot contain `#` or `:`. |


**Query Parameters in Segment URIs** and **Inherit M3U8 Non\-Auth Params** together determine the query parameters in rewritten resource URIs. For example, with resource URI `/video.ts?version=1`, if you remove the original parameters and enable inheritance, and the `.m3u8` request URL contains `q_m3u8=cool`, the rewritten URI is `/video.ts?q_m3u8=cool&<signature parameter name>=<timestamp>-<rand>-0-<SIGNATURE>`. If you retain original parameters, it is `/video.ts?version=1&q_m3u8=cool&<signature parameter name>=<timestamp>-<rand>-0-<SIGNATURE>`.

<span id="build-a-signed-url"></span>
## Build a signed URL

<span id="url-format"></span>
### URL format

```text
scheme://host<uri>?<signature parameter name>=<timestamp>-<rand>-<uid>-<SIGNATURE>
```


If the original URL already has query parameters, append the signature parameter with `&`:

```text
scheme://host<uri>?version=1&<signature parameter name>=<timestamp>-<rand>-<uid>-<SIGNATURE>
```


The `-` characters between `timestamp`, `rand`, `uid`, and `SIGNATURE` are literal characters.

<span id="signature-formula"></span>
### Signature formula

```text
MD5:    md5(uri-timestamp-rand-uid-key)
SHA256: sha256(uri-timestamp-rand-uid-key)
```


<span id="parameters"></span>
### Parameters


|Parameter |Description |
|---|---|
|`uri` |Request path beginning with `/`, excluding the scheme, domain, and query parameters. If the path contains Chinese characters, use the encoded path that the client actually sends. |
|`timestamp` |Decimal Unix timestamp in seconds. Together with the signature validity period, it determines whether the signature is expired. |
|`rand` |A 1–100\-character random string containing only letters or digits. |
|`uid` |Must be `0`. |
|`key` |The primary Key or Backup Key. It is used only in signature calculation. |
|`SIGNATURE` |The hash of the string to be signed. |


Example:

```text
https://www.example.com/img/image.png?sign=1644406401-2e1ca42a1bb248408fc9cf435e5af744-0-54959c1ec3448bf8e992554476248fab
```


<span id="cache-and-origin-requests"></span>
## Cache and origin requests

CDN excludes the Type A signature parameter from the cache key and removes it before forwarding the request to the origin. This behavior is not configurable.

<span id="verification"></span>
## Verification


1. After saving, use **Authentication Calculator** to select Type A and enter a complete, unsigned original URL under the current domain that matches the applicable scope.

2. In **Authentication Calculator**, enter **Auth Key**, **Signature Parameter**, `rand`, **Start Time**, **Validity Period**, and **Signing Algorithm** to generate an unexpired URL. **Start Time** is used to generate `timestamp`. If a Backup Key is configured, also validate a URL generated with the Backup Key.

3. Generate the same URL with the client or signing server and compare it with the calculator result. `uri`, `timestamp`, `rand`, `uid`, Key, and algorithm must match the calculator settings; the validity period is not part of signature calculation.

4. Request the test file and confirm that it is accessible. Requests with a tampered `SIGNATURE` and requests that use an expired URL must both return 403.

5. Confirm that origin requests do not include the signature parameter.

6. When using HLS, confirm that playlist resource URIs are signed and that the related resources are accessible.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828092101-1572984087547.png) </span>

<span id="cdn-validation-rules"></span>
## CDN validation rules


* When comparing signatures, CDN converts both its calculated result and `SIGNATURE` in the request to lowercase.

* A missing or malformed signature, a mismatched signature, or an expired signature returns 403.


<span id="rollout-and-rollback"></span>
## Rollout and rollback

For the first rollout, set the applicable scope to test files or directories only. Validate the client or signing server, CDN configuration, and HLS playback, then gradually expand the scope.

To rotate a Key, first configure the new Key as the Backup Key and validate signatures generated by the client or signing server with that Key. Then promote the new Key to the primary Key, retain the old Key temporarily as the Backup Key, and remove it after all old URLs expire. If many unexpected 403 responses occur, immediately narrow or delete the applicable scope. If necessary, disable URL authentication and save the configuration to restore access to unsigned requests.
