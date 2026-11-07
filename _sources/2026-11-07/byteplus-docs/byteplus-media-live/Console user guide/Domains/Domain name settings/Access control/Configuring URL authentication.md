---
title: "Configuring URL authentication"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication"
---

To protect live stream resources from unauthorized use, you can use the URL authentication feature to add the authentication information to the end of the original push or pull stream address. When a user initiates a push or pull stream request using a URL containing authentication information, the BytePlus MediaLive server validates the authentication parameters. Only requests that pass validation will be responded to. Requests that do not pass validation will be rejected. This topic describes how to configure URL authentication through the console.

<span id="4ef0cf9e"></span>
# Application scope

URL authentication applies to domain names for stream pushing and pulling.


* Configure URL authentication for domain names for stream pushing: Used to control which URLs can push streams, thereby preventing unauthorized users from pushing live streams to protect the source of live stream content. Currently, only Type B URL authentication can be configured for domain names for stream pushing.

* Configure URL authentication for domain names for stream pulling: Used to control which URLs can pull streams, ensuring that the audience can watch live streams only by using specific URLs. Type A, Type B, and Type C URL authentication can be configured for domain names for stream pulling.


<span id="882ce378"></span>
# Prerequisite

You have added a domain name. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

<span id="f9dd2d8d"></span>
# URL authentication process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebd6ea56ff424d2e8dc7334085832fd5~tplv-goo7wpa0wc-image.image) </span>


1. Your server generates authentication URLs and provides such URLs to users.

2. Users use authentication URLs to send push or pull stream requests to the BytePlus MediaLive server.

3. The BytePlus MediaLive server validates the authentication parameters in the authentication URL. Compare the authentication parameters in the authentication URL with the authentication parameters in the request to determine whether the request is valid.

   * Request is valid: The BytePlus MediaLive server responds to the request. Users can push or pull streams successfully.

   * Request is invalid: A 403 error is returned and the request is denied. Users cannot push or pull streams, thereby protecting live stream resources.


<span id="e7e3f739"></span>
# Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left navigation bar, click **Domains**.

3. On the **Domains** page, locate the domain name for stream pushing or pulling that needs to be configured, and click **Settings** in the **Action** column to enter the domain settings page.

4. Click the **Access control** tab.

5. Turn on the **URL authentication** switch, or click **Edit** in the **URL authentication** area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b89826da54b947279e3aa61e56ecab5e~tplv-goo7wpa0wc-image.image) </span>

6. In the **Edit URL authentication** dialog box that appears, select any of the following authentication types according to your business requirements, and complete the following configuration.

   * [Type A URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication#1747184f)

   * [Type B URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication#1c5d686d)

   * [Type C URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication#a4f520fc)

      All of the above\-mentioned authentication types use the MD5 encryption algorithm.

      About 5 minutes after completing the URL authentication configuration, users can only push or pull streams by using authentication URLs, while cannot push or pull streams by using original URLs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the URL authentication is enabled for domain names for stream pushing.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, domain names for stream pushing only support Type B URL authentication.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the above\-mentioned authentication types do not meet your business requirements, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">create a ticket</a> to contact technical support to complete the configuration for custom URL authentication.   </div>
   

7. Get the authentication URL.

   You can refer to [Type A URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication#1747184f), [Type B URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication#1c5d686d), or [Type C URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication#a4f520fc) and concatenate the authentication URL manually, or complete the following steps to get the authentication URL by using the address generator.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For domain names with custom URL authentication configuration, to get the authentication URL, you can concatenate the URL yourself according to your custom authentication rules or <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">create a ticket</a> to contact technical support.   </div>
   

   1. In the left navigation bar, click **Address generator**.

   2. Select **Push stream address** or **Pull stream address**.

   3. Select the domain name, and configure the **AppName**, **StreamName**, and expiration time. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

   4. Click **Generates Push stream address** or **Generates Pull stream address**.

   5. On the right side of the page, get the authentication URL.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b484ff0075ff494d885701d5665904fe~tplv-goo7wpa0wc-image.image) </span>


<span id="1747184f"></span>
## Type A URL authentication

<span id="8f01aaf5"></span>
### How it works

Authentication URL format:

```Plain
OriginalURL?auth_key={timestamp}-{rand}-{uid}-{md5hash}
```



|Field |Description |Example value |
|---|---|---|
|auth_key |The name of the signature parameter. You can configure the name in the **Edit URL authentication** dialog box of the console. |`auth_key` |
|timestamp |Unix timestamp, in seconds. Supports decimal or hexadecimal, and you must select the same time format in the **Edit URL authentication** dialog box of the console.<br><br>This field is used together with the valid period configured in the **Edit URL authentication** dialog box of the console to calculate the actual signature invalidation time. After the signature becomes invalid, users cannot pull streams through the authenticated URL.<br><br>The signature invalidation time = `timestamp` + valid period. For example, if the value of `timestamp` is `1758296819` (2025\-09\-19 23:46:59) and the valid period is 600 seconds, the signature invalidation time will be `1758297419` (2025\-09\-19 23:56:59). |`1758296819` |
|rand |A random number. You can use the UUID (Universally Unique Identifier) format and this field cannot contain hyphens (\-).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you generate the authentication URL using the address generator in the console, the value of this field is always set to <code>0</code>.</div><br> |`123e4567` |
|uid |User ID. A reserved parameter which is not in use currently. Set the value to `0`. |`0` |
|md5hash |A 32\-character lowercase string calculated using the MD5 encryption algorithm.<br><br>The calculation formula is as follows.<br><br>```Plain```<br>```sstring = "{URI}-{timestamp}-{rand}-{uid}-{Key}"```<br>```md5hash = md5sum(sstring)```<br><br><br>Among them,<br><br><br>* `URI`: The portion that begins immediately after the domain name and extends to the end of the path in the original URL. For example, if the original URL is `http://pull.example.com/live/test.flv`, the URI value is then `/live/test.flv`.<br><br>* `key`: Primary key or backup key, which can be configured in the **Edit URL authentication** dialog box of the console. For example, `123abc`.<br><br><br>In this example, the value of `{URI}-{timestamp}-{rand}-{uid}-{key}` is `/live/test.flv-1758296819-123e4567-0-123abc`. After generating the MD5 hash of this value, which produces a 32\-character lowercase string, the value of `md5hash` is `fbe5e26c0b7abe1431c3c897f7bdc278`. |`fbe5e26c0b7abe1431c3c897f7bdc278` |


Authentication URL example:

```Plain
http://pull.example.com/live/test.flv?auth_key=1758296819-123e4567-0-fbe5e26c0b7abe1431c3c897f7bdc278
```


<span id="7cb9e341"></span>
### Authentication process


1. After the BytePlus MediaLive server receives an authentication URL request from users, it performs MD5 hashing on the value of `{URI}-{timestamp}-{rand}-{uid}-{key}` to generate a 32\-character lowercase string. In the example of this topic, the final generated string is `fbe5e26c0b7abe1431c3c897f7bdc278`.

2. The BytePlus MediaLive server validates the authentication parameters in the authentication URL. The validation passes if both of the following checks are met.

   * Determine whether the signature value calculated by the server matches the signature value in the request. If matches, the validation passes. In the example of this topic, the signature value is `auth_key=1758296819-123e4567-0-fbe5e26c0b7abe1431c3c897f7bdc278`.

   * Determine whether the signature is valid. The server compares the current time with the signature invalidation time (`timestamp` + valid period). If the signature invalidation time is later than the current time, the signature is determined to be valid, and the validation passes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For protocols such as RTMP and FLV that are used to pull long\-duration streams, when a user initiates a pull stream request, the BytePlus MediaLive server validates the authentication parameters. Once the validation passes, users can continuously pull streams without being affected by the signature invalidation time. Therefore, as long as the request is initiated before the signature is invalid, stream pulling will not be interrupted due to invalid signature. Only newly initiated pull stream requests will fail due to invalid signature.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The HLS protocol is used for segmented video playback, and users continuously initiate new pull stream requests to get video segments. Each time a user initiates a pull stream request, the BytePlus MediaLive server validates the authentication parameters. Therefore, once the signature becomes invalid, requests will be rejected, resulting in playback interruption. Because new segments are frequently requested during live stream playback, we recommend that you set a longer signature invalidation time to prevent playback failures during the live stream.   </div>
   

3. Determine whether the request is valid based on the validation result.

   * Validation passes: The request is valid and the server responds to the request. Users can pull streams successfully.

   * Validation fails: The request is invalid. A 403 error is returned, and the request is denied. Users cannot pull streams, thus protecting live stream resources.


<span id="8ad6a89e"></span>
### Console configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a4aa801a7b64484abf8a13ece8afe6b~tplv-goo7wpa0wc-image.image) </span>


|Configuration item |Description |
|---|---|
|Primary key |Primary key.<br><br>The value must be 1\-100 characters in length and can contain digits (0–9), lowercase letters (a–z), and uppercase letters (A–Z).<br><br>You can also click the icon on the right of the text box to randomly generate a 24\-character key containing digits, lowercase and uppercase letters. |
|KEY |A backup key, which is used for smooth change of the primary key.<br><br>The value must be 1\-100 characters in length and can contain digits (0–9), lowercase letters (a–z), and uppercase letters (A–Z).<br><br>You can also click the icon on the right of the text box to randomly generate a 24\-character key containing digits, lowercase and uppercase letters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To prevent online service interruptions when changing the primary key, you can use the backup key to generate the authentication URL and achieve a smooth transition. During the transition period, you can replace the authentication URL with the version generated by the backup key. After the primary key changes, gradually replace the authentication URL with that generated by the new primary key.</div><br> |
|signature parameter |The name of the signature parameter. The default value is `auth_key`.<br><br>The value must be 1\-100 characters in length and can contain:<br><br><br>* Digits (0\-9)<br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Underscore (_)<br><br>* Hyphen (\-)<br><br>* Dot (.)<br><br>* Comma (,)<br><br>* Exclamation mark (!)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value must contain at least one letter.</div><br> |
|Valid period |The valid period of the signature. Unit: seconds. The default value is `600`. Value range: [0, 2592000].<br><br>This parameter is used together with the `timestamp` parameter in the authentication URL and can be used to calculate the actual signature invalidation time. After the signature becomes invalid, users cannot pull streams through the authenticated URL.<br><br>The signature invalidation time = `timestamp` + valid period. For example, if the value of `timestamp` is `1758296819` (2025\-09\-19 23:46:59) and the valid period is 600 seconds, the signature invalidation time will be `1758297419` (2025\-09\-19 23:56:59). |
|time format |Time format of `timestamp`. The default value is **Decimal**. Valid values:<br><br><br>* **Decimal**<br><br>* **Hexadecimal** |


<span id="1c5d686d"></span>
## Type B URL authentication

<span id="28f7c6dd"></span>
### How it works

Authentication URL format:

```Plain
OriginalURL?sign=md5(/{AppName}/{StreamName}{key}{timestamp})&expire=timestamp
```



|Field |Description |Example value |
|---|---|---|
|sign |The name of the signature parameter. You can configure the name in the **Edit URL authentication** dialog box of the console. |`sign` |
|AppName |The value of the `AppName` field in the live stream address.<br><br>The value must be 1\-30 characters in length and can contain:<br><br><br>* Digits (0\-9)<br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Underscore (_)<br><br>* Hyphen (\-)<br><br>* Dot (.)<br><br><br>For example, if the original URL is `http://pull.example.com/live/test.flv`, then the value of `AppName` is `live`. |`live` |
|StreamName |The value of the `StreamName` field in the live stream address.<br><br>The value must be 1\-100 characters in length and can contain:<br><br><br>* Digits (0\-9)<br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Underscore (_)<br><br>* Hyphen (\-)<br><br><br>For example, if the original URL is `http://pull.example.com/live/test.flv`, then the value of `StreamName` is `test`. |`test` |
|key |Primary key or backup key, which can be configured in the **Edit URL authentication** dialog box of the console. |`123abc` |
|timestamp |Unix timestamp, in seconds. Supports decimal or hexadecimal, and you must select the same time format in the **Edit URL authentication** dialog box of the console.<br><br>This field is used together with the valid period configured in the **Edit URL authentication** dialog box of the console to calculate the actual signature invalidation time. After the signature becomes invalid, users cannot push or pull streams through the authenticated URL.<br><br>The signature invalidation time = `timestamp` + valid period. For example, if the value of `timestamp` is `1758296819` (2025\-09\-19 23:46:59) and the valid period is 600 seconds, the signature invalidation time will be `1758297419` (2025\-09\-19 23:56:59). |`1758296819` |
|expire |The name of the timestamp parameter. You can configure the name in the **Edit URL authentication** dialog box of the console. |`expire` |


Calculate the signature value based on `md5(/{AppName}/{StreamName}{key}{timestamp})`. In the example of this topic, the value of `/{AppName}/{StreamName}{key}{timestamp}` is `/live/test123abc1758296819`. Perform MD5 hashing on this value to generate a 32\-character lowercase string, resulting in `1e2ea5d60de5adcf5e4b7688ccd76915`.

Authentication URL example:

```Plain
http://pull.example.com/live/test.flv?sign=1e2ea5d60de5adcf5e4b7688ccd76915&expire=1758296819
```


<span id="a83c35b7"></span>
### Authentication process


1. After the BytePlus MediaLive server receives an authentication URL request from users, it performs MD5 hashing on the value of `/{AppName}/{StreamName}{key}{timestamp}` to generate a 32\-character lowercase string. In the example of this topic, the final generated string is `1e2ea5d60de5adcf5e4b7688ccd76915`.

2. The BytePlus MediaLive server validates the authentication parameters in the authentication URL. The validation passes if both of the following checks are met.

   * Determine whether the signature value calculated by the server matches the signature value in the request. If matches, the validation passes. In the example of this topic, the signature value is `sign=1e2ea5d60de5adcf5e4b7688ccd76915&expire=1758296819`.

   * Determine whether the signature is valid. The server compares the current time with the signature invalidation time (`timestamp` + valid period). If the signature invalidation time is later than the current time, the signature is determined to be valid, and the validation passes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For protocols such as RTMP and FLV that are used to push or pull long\-duration streams, when a user initiates a push or pull stream request, the BytePlus MediaLive server validates the authentication parameters. Once the validation passes, users can continuously push or pull streams without being affected by the signature invalidation time. Therefore, as long as the request is initiated before the signature is invalid, stream pushing or pulling will not be interrupted due to invalid signature. Only newly initiated push or pull stream requests will fail due to invalid signature.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The HLS protocol is used for segmented video playback, and users continuously initiate new pull stream requests to get video segments. Each time a user initiates a pull stream request, the BytePlus MediaLive server validates the authentication parameters. Therefore, once the signature becomes invalid, requests will be rejected, resulting in playback interruption. Because new segments are frequently requested during live stream playback, we recommend that you set a longer signature invalidation time to prevent playback failures during the live stream.   </div>
   

3. Determine whether the request is valid based on the validation result.

   * Validation passes: The request is valid and the server responds to the request. Users can push or pull streams successfully.

   * Validation fails: The request is invalid. A 403 error is returned, and the request is denied. Users cannot push or pull streams, thus protecting live stream resources.


<span id="3f8e2d6e"></span>
### Console configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a54a8bd8454b47e39579257ac5fe6aa9~tplv-goo7wpa0wc-image.image) </span>


|Configuration item |Description |
|---|---|
|Primary key |Primary key.<br><br>The value must be 1\-100 characters in length and can contain digits (0–9), lowercase letters (a–z), and uppercase letters (A–Z).<br><br>You can also click the icon on the right of the text box to randomly generate a 24\-character key containing digits, lowercase and uppercase letters. |
|KEY |A backup key, which is used for smooth change of the primary key.<br><br>The value must be 1\-100 characters in length and can contain digits (0–9), lowercase letters (a–z), and uppercase letters (A–Z).<br><br>You can also click the icon on the right of the text box to randomly generate a 24\-character key containing digits, lowercase and uppercase letters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To prevent online service interruptions when changing the primary key, you can use the backup key to generate the authentication URL and achieve a smooth transition. During the transition period, you can replace the authentication URL with the version generated by the backup key. After the primary key changes, gradually replace the authentication URL with that generated by the new primary key.</div><br> |
|signature parameter |The name of the signature parameter. The default value is `sign`.<br><br>The value must be 1\-100 characters in length and can contain:<br><br><br>* Digits (0\-9)<br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Underscore (_)<br><br>* Hyphen (\-)<br><br>* Dot (.)<br><br>* Comma (,)<br><br>* Exclamation mark (!)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The value must contain at least one letter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The signature parameter and the timestamp parameter cannot have the same name.</div><br> |
|Timestamp parameter |The name of the timestamp parameter. The default value is `expire`.<br><br>The value must be 1\-100 characters in length and can contain:<br><br><br>* Digits (0\-9)<br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Underscore (_)<br><br>* Hyphen (\-)<br><br>* Dot (.)<br><br>* Comma (,)<br><br>* Exclamation mark (!)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The value must contain at least one letter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The signature parameter and the timestamp parameter cannot have the same name.</div><br> |
|Valid period |The valid period of the signature. Unit: seconds. The default value is `600`. Value range: [0, 2592000].<br><br>This parameter is used together with the `timestamp` parameter in the authentication URL and can be used to calculate the actual signature invalidation time. After the signature becomes invalid, users cannot push or pull streams through the authenticated URL.<br><br>The signature invalidation time = `timestamp` + valid period. For example, if the value of `timestamp` is `1758296819` (2025\-09\-19 23:46:59) and the valid period is 600 seconds, the signature invalidation time will be `1758297419` (2025\-09\-19 23:56:59). |
|time format |Time format of `timestamp`. The default value is **Decimal**. Valid values:<br><br><br>* **Decimal**<br><br>* **Hexadecimal**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Domain names for stream pushing only support the decimal time format.</div><br> |


<span id="a4f520fc"></span>
## Type C URL authentication

<span id="b10ab2b8"></span>
### How it works

Authentication URL format:

```SQL
OriginalURL?txSecret=md5({key}{StreamName}{timestamp})&txTime=timestamp
```



|Field |Description |Example value |
|---|---|---|
|txSecret |The name of the signature parameter. You can configure the name in the **Edit URL authentication** dialog box of the console. |`txSecret` |
|key |Primary key or backup key, which can be configured in the **Edit URL authentication** dialog box of the console. |`123abc` |
|StreamName |The value of the `StreamName` field in the live stream address.<br><br>The value must be 1\-100 characters in length and can contain:<br><br><br>* Digits (0\-9)<br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Underscore (_)<br><br>* Hyphen (\-)<br><br><br>For example, if the original URL is `http://pull.example.com/live/test.flv`, then the value of `StreamName` is `test`. |`test` |
|timestamp |Unix timestamp, in seconds. Supports decimal or hexadecimal, and you must select the same time format in the **Edit URL authentication** dialog box of the console.<br><br>This field is used together with the valid period configured in the **Edit URL authentication** dialog box of the console to calculate the actual signature invalidation time. After the signature becomes invalid, users cannot pull streams through the authenticated URL.<br><br>The signature invalidation time = `timestamp` + valid period. For example, if the value of `timestamp` is `68cd7af3` (2025\-09\-19 23:46:59) and the valid period is 600 seconds, the signature invalidation time will be `68cd7d4b` (2025\-09\-19 23:56:59). |`68cd7af3` |
|txTime |The name of the timestamp parameter. You can configure the name in the **Edit URL authentication** dialog box of the console. |`txTime` |


Calculate the signature value based on `md5({key}{StreamName}{timestamp})`. In the example of this topic, the value of `{key}{StreamName}{timestamp}` is `123abctest68cd7af3`. Perform MD5 hashing on this value to generate a 32\-character lowercase string, resulting in `73af6af9c874d9d4cc50f8490325cd7b`.

Authentication URL example:

```Plain
http://pull.example.com/live/test.flv?txSecret=73af6af9c874d9d4cc50f8490325cd7b&txTime=68cd7af3
```


<span id="cdbc1626"></span>
### Authentication process


1. After the BytePlus MediaLive server receives an authentication URL request from users, it performs MD5 hashing on the value of `{key}{StreamName}{timestamp}` to generate a 32\-character lowercase string. In the example of this topic, the final generated string is `73af6af9c874d9d4cc50f8490325cd7b`.

2. The BytePlus MediaLive server validates the authentication parameters in the authentication URL. The validation passes if both of the following checks are met.

   * Determine whether the signature value calculated by the server matches the signature value in the request. If matches, the validation passes. In the example of this topic, the signature value is `txSecret=73af6af9c874d9d4cc50f8490325cd7b&txTime=68cd7af3`.

   * Determine whether the signature is valid. The server compares the current time with the signature invalidation time (`timestamp` + valid period). If the signature invalidation time is later than the current time, the signature is determined to be valid, and the validation passes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For protocols such as RTMP and FLV that are used to pull long\-duration streams, when a user initiates a pull stream request, the BytePlus MediaLive server validates the authentication parameters. Once the validation passes, users can continuously pull streams without being affected by the signature invalidation time. Therefore, as long as the request is initiated before the signature is invalid, stream pulling will not be interrupted due to invalid signature. Only newly initiated pull stream requests will fail due to invalid signature.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The HLS protocol is used for segmented video playback, and users continuously initiate new pull stream requests to get video segments. Each time a user initiates a pull stream request, the BytePlus MediaLive server validates the authentication parameters. Therefore, once the signature becomes invalid, requests will be rejected, resulting in playback interruption. Because new segments are frequently requested during live stream playback, we recommend that you set a longer signature invalidation time to prevent playback failures during the live stream.   </div>
   

3. Determine whether the request is valid based on the validation result.

   * Validation passes: The request is valid and the server responds to the request. Users can pull streams successfully.

   * Validation fails: The request is invalid. A 403 error is returned, and the request is denied. Users cannot pull streams, thus protecting live stream resources.


<span id="4c04cb54"></span>
### Console configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/185c77b4bf93468aac5d708525dfe8de~tplv-goo7wpa0wc-image.image) </span>


|Configuration item |Description |
|---|---|
|Primary key |Primary key.<br><br>The value must be 1\-100 characters in length and can contain digits (0–9), lowercase letters (a–z), and uppercase letters (A–Z).<br><br>You can also click the icon on the right of the text box to randomly generate a 24\-character key containing digits, lowercase and uppercase letters. |
|KEY |A backup key, which is used for smooth change of the primary key.<br><br>The value must be 1\-100 characters in length and can contain digits (0–9), lowercase letters (a–z), and uppercase letters (A–Z).<br><br>You can also click the icon on the right of the text box to randomly generate a 24\-character key containing digits, lowercase and uppercase letters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To prevent online service interruptions when changing the primary key, you can use the backup key to generate the authentication URL and achieve a smooth transition. During the transition period, you can replace the authentication URL with the version generated by the backup key. After the primary key changes, gradually replace the authentication URL with that generated by the new primary key.</div><br> |
|signature parameter |The name of the signature parameter. The default value is `txSecret`.<br><br>The value must be 1\-100 characters in length and can contain:<br><br><br>* Digits (0\-9)<br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Underscore (_)<br><br>* Hyphen (\-)<br><br>* Dot (.)<br><br>* Comma (,)<br><br>* Exclamation mark (!)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The value must contain at least one letter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The signature parameter and the timestamp parameter cannot have the same name.</div><br> |
|Timestamp parameter |The name of the timestamp parameter. The default value is `txTime`.<br><br>The value must be 1\-100 characters in length and can contain:<br><br><br>* Digits (0\-9)<br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Underscore (_)<br><br>* Hyphen (\-)<br><br>* Dot (.)<br><br>* Comma (,)<br><br>* Exclamation mark (!)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The value must contain at least one letter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The signature parameter and the timestamp parameter cannot have the same name.</div><br> |
|Valid period |The valid period of the signature. Unit: seconds. The default value is `600`. Value range: [0, 2592000].<br><br>This parameter is used together with the `timestamp` parameter in the authentication URL and can be used to calculate the actual signature invalidation time. After the signature becomes invalid, users cannot pull streams through the authenticated URL.<br><br>The signature invalidation time = `timestamp` + valid period. For example, if the value of `timestamp` is `68cd7af3` (2025\-09\-19 23:46:59) and the valid period is 600 seconds, the signature invalidation time will be `68cd7d4b` (2025\-09\-19 23:56:59). |
|time format |Time format of `timestamp`. The default value is **Hexadecimal**. Valid values:<br><br><br>* **Decimal**<br><br>* **Hexadecimal** |
