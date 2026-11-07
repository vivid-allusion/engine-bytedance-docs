---
title: "Type A signing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-type-a"
---

URL signing protects your origin servers from unauthorized downloads and access by adding a cryptographic signature to resource URLs. This guide explains the working principle of Type A signing, its configuration, and provides a detailed signing example to help you implement it.

## How it works

The working principle of type A signing is as follows:

* How a URL is signed based on type A signing

   ```HTTP
   scheme://host/uri?auth_key=timestamp-rand-uid-md5(uri-timestamp-rand-uid-key)(&...)
   ```

* Signed URL example:

   ```HTTP
   https://www.example.com/img/byteplus.png?auth_key=1644406401-2e1ca42a1bb248408fc9cf435e5af744-0-54959c1ec3448bf8e992554476248fab
   ```

* Signing parameters in a signed URL

   |Parameter |Description |
   |---|---|
   |uri |The requested file path. The path starts with a slash (`/`) and does not include the domain name. For example, if the complete path is `https://www.example.com/image.png`, the value of uri is `/image.png`. If the path contains Chinese characters, you need to encode the path. |
   |timestamp |The time when the signed URL is generated. The timestamp follows the UNIX time format. The timestamp and the validity duration you specified in the BytePlus VOD console determine the time when a signed URL expires. The expiration time of the signed URL is timestamp + valid duration. Example: `1644406401`. |
   |rand |A random string. The length is 1\-100 characters and can contain letters and numbers. Example: `2e1ca42a1bb248408****f435e5af744`. |
   |uid |The user ID. Set this field to 0. |
   |key |The key you specified in the BytePlus VOD console. You can use the primary key or the backup key. |

* Signing process:

   1. After receiving a request from the client, the CDN node calculates the signature based on the `md5(uri-timestamp-rand-uid-key)` formula using the MD5 algorithm. The MD5 value is converted to lowercase for comparison, and it consists of 32 characters.

   2. The CDN node performs the following verifications:

      1. Checks whether the calculated signature matches the signature in the client's request.

      2. Checks whether the signature has expired. The CDN node compares "timestamp + the valid duration you specified in the BytePlus VOD console" with the current time. If the expiration time of the signature is earlier than the current time, the VOD service determines that the signature has expired; otherwise, the signature is considered valid.

   3. Based on the verification result, the CDN node returns the requested resource or an HTTP 403 error.

## Console configuration

For Type A signing, you can configure the following parameters in the BytePlus VOD console:

|Parameter |Description |
|---|---|
|Rule |Specifies which requests require authentication. You need to add at least one rule and can add up to 10 rules.<br><br>You can specify the relationship between multiple rules:<br><br><br>* **Any** means that any request that matches any rule will be authenticated.<br><br>* **All** means that only requests that match all rules will be authenticated.<br><br><br>Each rule includes the following configurations:<br><br><br>* **Rule type**: Supports the following options:<br><br>   * **File directory**: The rule applies to all files in a specific directory.<br><br>   * **File suffix**: The rule applies to all files with specific suffixes.<br><br>   * **File full path**: The rule applies to specific files.<br><br>* **Match type**: Can be set to **Match** or **Mismatch**.<br><br>* **Rule**: Enter the content of the rule based on the **Rule type**. The length cannot exceed 1,024 characters. The following characters are not allowed: consecutive slashes (`//`), spaces, dollar signs (`$`), question marks (`?`), and Delete (ASCII code 127). The specific requirements for different rule types are as follows:<br><br>   * If the rule type is **File suffix**, the rule content must be one or more file suffixes separated by semicolons (`;`). The file suffix does not need to start with a period (`.`). Example: `png;txt`.<br><br>   * If the rule type is **File directory**, the rule content must be one or more directories separated by semicolons (;). The directory must start and end with a slash (/). Example: /chs/foods/;/us/birds/.<br><br>   * If the rule type is **File full path**, the rule content must be one or more file paths separated by semicolons (`;`). The file path must start with a slash (`/`) and can contain an asterisk (`*`) to represent one or more characters. Example: `/chs/foods/local*sets;/us/birds/chickadee`. |
|Primary key |The primary key. The length must be 6\-40 characters and can only contain printable ASCII characters, except for Delete (ASCII code 127). Pure whitespace characters are not supported. |
|Backup key |The backup key. The length must be 6\-40 characters and can only contain printable ASCII characters, except for Delete (ASCII code 127). Pure whitespace characters are not supported.<br><br>> **Note**<br><br><br>> When updating URL signing for an online domain name, use a backup key during the transition period to avoid disruptions to your online business.<br> |
|Support preview |Enables video preview for a playback domain. To obtain a preview URL, call [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) with `NeedPreview=true`. For supported formats and playback limitations, see [Video preview](https://docs.byteplus.com/docs/byteplus-vod/docs-video-preview). |
|Preview duration |The preview duration in seconds, required when **Support preview** is enabled. Enter a positive integer of at least 5 seconds. The console advises that the duration should not exceed the video's total duration. Choose a shorter duration to provide a partial preview. For HLS, playback ends at a TS segment boundary and can be shorter than the configured duration; follow the [HLS preview duration requirements](https://docs.byteplus.com/docs/byteplus-vod/docs-video-preview#requirements-and-limits). |
|Signature parameter |The signature parameter name is set to `auth_key`. |
|Validity duration |The valid duration of the signature. This parameter is used in conjunction with the timestamp parameter in the client request to calculate the expiration time of the signature. The expiration time of the signature is timestamp + valid duration. You can specify a time unit and enter a value. The default valid duration is 30 minutes. The maximum valid duration you can specify is 10 years, which is 315,360,000 seconds. The specific instructions are as follows:<br><br><br>* If you specify the time unit as **seconds**, the maximum value you can enter is `315360000`.<br><br>* If you specify the time unit as **minutes**, the maximum value you can enter is `5256000`. |
|Time format |Fixed as **Decimal (Unix timestamp)** . |
|M3U8 rewrite |Specifies whether to add the signature parameter to the URL of each segment file in the response to a .m3u8 file request. The signature of each segment URL is calculated based on the rewritten segment URL using the signature rule. After enabling this configuration, you can also configure the following:<br><br><br>* **Whether to retain original parameters in segment URLs**: Whether to retain the original parameters in the segment URL when rewriting the segment URL.<br><br>* **Whether to inherit non\-signing parameters in M3U8 file URLs**: Whether to add non\-signing query parameters from the M3U8 file URL to the segment URLs.<br><br>* **Rewrite tag selection**: Specify which HLS tags in the M3U8 manifest should have their URIs rewritten with a signature. You can select the following tags:<br><br>   * `#EXT-X-MAP`<br><br>   * `#EXT-X-MEDIA`<br><br><br>> **Warning**<br><br><br><br>* > The **M3U8 rewrite** feature is only available for playback domain names.<br><br><br>* > The **Rewrite tag selection** feature is only applicable to domains created after **October 20, 2025 (UTC+8)**. For domains created before this date, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) to our technical support team for assistance.<br> |

## Signing **example**

To better understand the logic of Type A signing, let's walk through an example scenario.

### Example conditions

In this example, assume that the signed request URL is:

```HTTP
https://www.example.com/img/byteplus.png?auth_key=1644406401-2e1ca42a1bb248408fc9cf435e5af744-0-54959c1ec3448bf8e992554476248fab
```

Based on the above URL, the values of each signing parameter are as follows:

* The value of `uri` is `/img/byteplus.png`.

* The value of `timestamp` is `1644406401`, which indicates that the URL was generated at 2022\-02\-09 11:33:21 GMT.

* The value of `rand` is `2e1ca42a1bb248408fc9cf435e5af744`.

* The value of `uid` is `0`.

Assume that the key you specified in the BytePlus VOD console is `abc123def456`, and the valid duration is 1800 seconds.

### Signing **process**

The signing process in this example is as follows:

1. Upon receiving the signed request, the BytePlus CDN node uses the MD5 algorithm to calculate the signature value using the formula `md5(uri-timestamp-rand-uid-key)`. In this case, the signature calculation is: `md5(/img/byteplus.png-1644406401-2e1ca42a1bb248408fc9cf435e5af744-0-abc123def456)`

2. The CDN then validates the request by comparing the calculated signature with the one provided in the request URL.

   ```Plain
   https://www.example.com/img/byteplus.png?auth_key=1644406401-2e1ca42a1bb248408fc9cf435e5af744-0-54959c1ec3448bf8e992554476248fab
   ```

3. The CDN node validates the request:

   * Verifies that the calculated signature matches the signature in the client's request.

   * Checks for expiration. The signature is considered valid if the current time is before the URL's expiration time.

## Signature generation tool

For easy implementation of Type A URL signing, BytePlus VOD offers a signature generation tool. For details, see [Signature generation](https://docs.byteplus.com/docs/byteplus-vod/docs-signature-generation).
