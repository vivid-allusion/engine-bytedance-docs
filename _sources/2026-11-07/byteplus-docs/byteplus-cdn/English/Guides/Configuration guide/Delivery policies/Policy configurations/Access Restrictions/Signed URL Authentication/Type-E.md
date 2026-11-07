---
title: "Type-E"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-type-e"
---

<span id="characteristics"></span>
## Characteristics

Type E sends the signature and timestamp in separate query parameters and lets you choose the fields and concatenation order used for signature calculation. Use it when Type D's fixed fields and calculation order are insufficient, and request parameters, request headers, client information, or a custom order must participate in signing.

<span id="rollout-recommendation"></span>
## Rollout recommendation

Validate first with a separate test file or directory before protecting production resources.

<span id="configure-targets"></span>
## Configure Targets

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828094716-54560621441.png) </span>

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828094731-313535356977.png) </span>

Enable **URL Authentication**, select **Type E**, and configure **Targets**. The default **Path Directory** rule for `/` cannot be deleted. You can change its type and content, add up to 10 rules, and combine rules with **OR** (default) or **AND**. Only matching requests require authentication.


|Match Type |Match Value / Pattern |
|---|---|
|Path Extension |Extensions separated by `;`, with no periods, for example `png;txt`. |
|Path Directory |Directories separated by `;`, each beginning and ending with `/`, for example `/video/;/image/`. |
|Full Path |Paths separated by `;`, each beginning with `/`; `*` matches one or more characters, including `/`, for example `/video/*;/image/logo.png`. |
|Full Path Regex |Regular expressions separated by `;`; [submit a ticket](https://console.byteplus.com/workorder/create) before use. |


Non\-regex rules are case\-insensitive; full\-path regexes are case\-sensitive. The combined length of the matching values in a condition must not exceed 1,024 characters. The values cannot contain `//`, spaces, `$`, or `?`.

<span id="configure-url-authentication"></span>
## Configure URL Authentication

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260917095758-100381670161.png) </span>

On the **Auth Configuration** tab, configure the following parameters.

<span id="basic-parameters"></span>
### Basic parameters


|Setting |Description |
|---|---|
|Primary Key |Required. It must be 1–120 characters long and can contain only English letters, digits, and ASCII half\-width symbols. Spaces, Chinese characters, and full\-width characters are not supported. The client or signing server uses it to generate signatures; CDN calculates a signature by the same rules and compares it with the request signature. |
|Backup Key |Optional; CDN retries validation with the Backup Key if validation with the Primary Key fails. It has the same input requirements and supports Key rotation. |
|Signature Validity Period (Seconds) |Seconds; default `1800`; range 0–315,360,000. The URL expires when `timestamp + validity period < time when the request is received`. |
|Signing Algorithm |MD5 or SHA256; default MD5. The client or signing server must use the same signing algorithm as CDN. |


<span id="signature-fields"></span>
### Signature fields


|Setting |Description |
|---|---|
|Signature Parameter Name |Specifies the query parameter that carries the signature. The default name is `sign`. The name is case\-sensitive, must be 1–100 characters long, cannot be the same as the Timestamp Parameter Name, may contain letters, digits, `_`, `-`, `.`, `,`, and `!`, and must include at least one letter. |
|Timestamp Parameter Name |Specifies the query parameter that carries the timestamp. The default name is `t`. The name is case\-sensitive, must be 1–100 characters long, cannot be the same as the Signature Parameter Name, and may contain letters, digits, `_`, `-`, `.`, `,`, and `!`. |
|Timestamp Format |Specifies whether the timestamp uses a decimal or hexadecimal Unix timestamp in seconds. |
|Signature Calculation Rule |Must include **Key**, **URI**, and **Timestamp Parameter**. You can add request parameters, request headers, client information, and custom variables, and adjust the order of all fields. |
|Additional Settings |Lets you configure up to 50 custom variables. Each variable is of the request\-parameter or request\-header type and uses exact\-match retrieval. A variable name can be up to 100 characters long. Request\-parameter names can contain letters, digits, `-`, `,`, `.`, and `!`; request\-header names cannot contain spaces, double quotation marks, or colons. |


Optional calculation fields are `Referer`, client domain, `Origin`, client IP, `User-Agent`, and custom variables. The client or signing server must use exactly the same field values and order. Before saving, you can enable **Exclude Auth Params from Cache Key & Origin Requests**.

<span id="hls-manifest-signing"></span>
## HLS Manifest Signing

Type E supports **HLS Manifest Signing**. CDN signs playlist resource URIs using Type E; only the `.m3u8` request needs to be signed by the client or signing server.

<span id="rewrite-conditions"></span>
### Rewrite conditions

HLS Manifest Signing takes effect only when all of the following conditions are met:


* **Path Extension** in **Targets** includes `m3u8` and the extensions of all protected playlist resources. For example, configure `m3u8;ts;mp4` for `.ts` segments and `.mp4` files. CDN authenticates a resource URI with a matching extension even if it does not match **Path Directory**, **Full Path**, or **Full Path Regex** conditions.

* The origin response for `.m3u8` does not include `Content-Encoding`, and the `.m3u8` request does not match the scope configured for **File Compression**. CDN does not rewrite compressed M3U8 files.

* If the **Signature Calculation Rule** includes request headers, every resource request must include the same header names and values as the `.m3u8` request. Otherwise, signature validation fails.


Resource URIs may be complete URLs, absolute paths, or relative paths; relative paths remain relative. For `segment-1.ts` in `/e-basic-m3u8-rewrite-test/playlist.m3u8`, the rewritten URI is `segment-1.ts?<signature parameter name>=<SIGNATURE>&<timestamp parameter name>=<timestamp>`.

<span id="configure-rewrite-parameters"></span>
### Configure rewrite parameters


|Setting |Description |
|---|---|
|Query Parameters in Segment URIs |Controls whether existing query parameters in playlist resource URIs are retained. |
|Inherit M3U8 Non\-Auth Params |Controls whether query parameters other than the signature and timestamp parameters from the `.m3u8` request URL are added to playlist resource URIs. If the **Signature Calculation Rule** includes request parameters, this setting remains enabled and cannot be disabled. |
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
MD5:    md5(<custom signature calculation rule>)
SHA256: sha256(<custom signature calculation rule>)
```


`<custom signature calculation rule>` concatenates actual field values in the configured order without an automatic separator. For example, the values of **Key**, **URI**, and **Timestamp Parameter** are concatenated as `key + uri + timestamp`. `+` is not a literal character. `uri` starts with `/`, excludes query parameters, and uses the encoded path actually sent for Chinese characters.

<span id="parameters"></span>
### Parameters


|Parameter |Description |
|---|---|
|`key` |Primary Key or Backup Key; used only in signature calculation. |
|`uri` |Request path excluding domain and query parameters. |
|`timestamp` |Configured decimal or hexadecimal Unix timestamp in the URL. |
|`SIGNATURE` |Hash of the custom calculation\-rule result: 32 hexadecimal characters for MD5 or 64 for SHA256. |


```text
https://www.example.com/product/cdn?sign=e954e253c33634b510443af72406600f&t=1620291453&query1=value1
```


The actual `SIGNATURE` depends on the configured signing rule.

<span id="cache-and-origin-requests"></span>
## Cache and origin requests

By default, CDN includes the Type E signature and timestamp parameters in both the cache key and the request forwarded to the origin. When **Exclude Auth Params from Cache Key & Origin Requests** is enabled, CDN excludes those parameters from the cache key and removes them before forwarding the request to the origin.

<span id="verification"></span>
## Verification


1. After saving, use **Authentication Calculator** to select **Type E** and enter a complete, unsigned original URL under the current domain that matches the applicable scope.

2. In **Authentication Calculator**, enter **Auth Key**, **Signature Parameter**, **Timestamp Parameter**, **Custom Variables**, **Computation Rule**, **Start Time**, **Validity Period**, **Timestamp Format**, and **Signing Algorithm** to generate an unexpired URL. **Start Time** is used to generate `timestamp`. If the signing rule includes custom request parameters, the original URL must not contain them. Enter each parameter name and value as a custom variable; the calculator appends the parameters to the generated URL. If a Backup Key is configured, also validate a URL generated with the Backup Key.

3. Generate the same URL with the client or signing server and compare it with the calculator result. The fields, field values, concatenation order, `uri`, `timestamp`, Key, and algorithm must match the calculator settings; the validity period is not part of signature calculation.

4. Confirm that the test file is accessible. A request with a tampered `SIGNATURE`, an expired URL, or a signature generated with field values or a concatenation order that differs from the CDN configuration must return 403.

5. With **Exclude Auth Params from Cache Key & Origin Requests** disabled, confirm that the signature and timestamp parameters are present in the cache key and in the request forwarded to the origin. Enable the setting, repeat the request, and confirm that both parameters are excluded from the cache key and removed from the origin request.

6. When using HLS, confirm that playlist resource URIs are signed and the related resources are accessible.

7. If the signing rule includes request headers, confirm that playlist and resource requests carry the same header values. If it includes custom request parameters, confirm that URLs generated by the calculator and rewritten resource URIs include the same parameter values.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260828092640-1773585774727.png) </span>

<span id="cdn-validation-rules"></span>
## CDN validation rules


* CDN compares lowercase versions of its calculated signature and `SIGNATURE`.

* A missing or malformed signature, a mismatched signature, or an expired signature returns 403.


<span id="rollout-and-rollback"></span>
## Rollout and rollback

For the first rollout, limit the applicable scope to test files or directories. Validate the client or signing server, CDN configuration, time synchronization, cache and origin\-request behavior, and HLS playback before gradually expanding the scope.

To rotate a Key, configure the new Key as the Backup Key, validate signatures generated with it, then promote it to the primary Key and retain the old Key as the Backup Key until old URLs expire. If many unexpected 403 responses occur, immediately narrow or delete the scope. If necessary, disable URL authentication and save the configuration to restore unsigned access.
