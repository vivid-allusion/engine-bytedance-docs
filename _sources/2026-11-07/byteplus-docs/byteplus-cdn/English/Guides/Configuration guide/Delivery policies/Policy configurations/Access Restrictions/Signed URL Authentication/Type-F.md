---
title: "Type-F"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us"
---

Type F is the most advanced URL authentication configuration in BytePlus CDN, designed for creating highly flexible and complex security rules. With Type F, you can define custom conditions for authentication, specify intricate methods for retrieving tokens and timestamps from requests, and combine various algorithms for token calculation. This configuration also supports automatically modifying HLS and DASH video manifests to secure individual video fragments, making it ideal for protecting streaming media content.

<span id="overview"></span>
## Overview

In Type F configuration, you can:


* Configure request matching conditions. Only user requests that meet the conditions need to be authenticated.

* Configure complex methods to obtain tokens and token timestamp from user requests.

* Configure complex token calculation logic, including specifying various parameters for token calculation, parameter value concatenation methods, and token algorithm combinations.

* Modify video manifests to add tokens and token timestamps to video fragment URIs.

* Configure whether origin requests include tokens.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Type F can implement the configurations in Type A, Type B, Type C, Type D, and Type E.</div>


<span id="steps"></span>
## Steps


1. Open the **Signed URL Authentication** configuration page. For steps, see [Domain Management](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to enabled.

3. Set **Authentication Type** to **Type F**.

4. Click **Add Rule**. You can add up to 5 rules.

5. Configure according to the Configuration Instructions.

6. After configuration, click **Save**.


When CDN receives a user request, it evaluates the rules sequentially. The first rule that matches the request is applied, and all subsequent rules are ignored.

<span id="configuration-instructions"></span>
## Configuration Instructions


|**Configuration Category** |**Configuration** |**Description** |
|---|---|---|
|Conditions |Conditions |Represents a set of matching conditions. CDN authenticates user requests that meet the conditions. You need to add at least one condition and can add up to 10. You can specify the relationship between multiple conditions, with **Or** as the default.<br><br><br>* **Or:**  Indicates that user requests matching any condition will be authenticated.<br><br>* **And**: Indicates that only user requests matching all conditions will be authenticated. Each condition includes match type, match method, and match value.<br><br><br>The total length of match values cannot exceed 1,024 characters and cannot contain the following characters:<br><br><br>* Consecutive slashes (//), spaces, dollar signs ($), question marks (?), Delete (ASCII code 127).<br><br><br>Additionally,<br><br><br>* If the match type is **URL Path Extension**, the match value must be one or more file extensions separated by semicolons (;). Do not include a leading period (.) in file extensions. For example: `png;txt`.<br><br>* If the match type is **URL Path Directory**, the match value must be one or more path directories separated by semicolons (;). Path directories must start and end with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If the match type is **URL Path Literal**, the match value must be one or more file paths separated by semicolons (;). File paths must start with a slash (/) and can include asterisks (\*) to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If the match type is **URL Path RegEx**, the match value must be one or more regular expressions separated by semicolons (;) to match request paths. For example: `/a{1,2}(.*)g`. |
|Signing Keys |Primary Key |Represents the primary key. |
||Secondary Key |Represents the backup key. If authentication fails, CDN will recalculate the token using the backup key and compare it with the token in the user request. |
|Token Retrieval |Get Token From |Represents the token retrieval method, including:<br><br><br>* Query Parameter: Indicates the token comes from a query parameter in the request URL. You need to enter the name of the query parameter below.<br><br>* Path Segment: Indicates the token comes from a directory in the request path. You need to specify the level below. The level is a non\-zero integer. The absolute value of the specified level cannot exceed the total number of levels in the path.<br><br>   * If the level is a positive integer, it counts from the leftmost directory in the path to locate the corresponding directory.<br><br>   * If the level is a negative integer, it counts from the rightmost directory in the path.<br><br>&nbsp;<br><br>      **Example:** <br><br>      If the request path is `/a/b/c/d`, and the token comes from `b`. In this case, you can specify the level as `2` or `-3`.<br><br>* Request Header: Indicates the token comes from a header in the user request. You need to specify the request header below.<br><br>* Cookie: Indicates the token comes from a cookie in the user request. You need to specify the cookie's key below, and CDN will get the cookie's value.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The cookie format must comply with <a href="https://datatracker.ietf.org/doc/html/rfc6265">RFC 6265</a>. Otherwise, CDN may not be able to get the cookie's value.   </div><br>   <br><br>When **Get Token From** is **Query Parameter** or **Path Segment**, for the obtained content, you can specify the following options:<br><br><br>* **Value Not Delimited**: Indicates the content itself is the token. This is the default option.<br><br>* **Value Is Delimited**: Indicates the content is a delimited string from which the token must be extracted. Extraction methods include the following options:<br><br>   * Delimiter: Indicates the delimiter used to split the content.<br><br>   * Token Index: Indicates the level where the token is located after splitting the content into multiple level segments using the delimiter. See the description of **Path Segment** in this configuration.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For input requirements of this configuration, see <a href="https://docs.byteplus.com/en/docs/18/46937#configuration-input-requirements">Configuration Input Requirements</a>.</div><br> |
|Expiration Time |Get Token Timestamp From |Specifies the method for retrieving the token timestamp. The description of this configuration is similar to the description of **Get Token From** configuration. |
||Timestamp Format |Represents the format of the token timestamp. This parameter has the following options:<br><br><br>* Octal Unix Timestamp: Indicates the expiration time is an octal Unix timestamp, for example, `14751410031`.<br><br>* Decimal Unix Timestamp: Indicates the expiration time is a decimal Unix timestamp, for example, `1738936345`.<br><br>* Hexadecimal Unix Timestamp: Indicates the expiration time is a hexadecimal Unix timestamp, for example, `67a61019`. |
||Token TTL |Represents the token's validity period in seconds, ranging from 0\-315,360,000, with a default value of `0`.<br><br><br>* Token expiration time = Time represented by token timestamp + Token TTL<br><br><br>When receiving a user request, if the token expiration time calculated by CDN is earlier than the current time, CDN determines the token has expired and returns a 403 response status code. |
|Signing Parameters |Parameters |Represents the list of objects used by CDN when calculating tokens. Click **Add Parameter** to add an object. Object types include:<br><br><br>* Signing Key: Represents the primary key or backup key.<br><br>* Fixed String: Represents a string. You need to enter the string below.<br><br>* Path Segments: Represents consecutive segments in the user request path. The path does not include query strings. For this type, you need to specify the following options:<br><br>   * Delimiter: Indicates the delimiter used to split the URL path.<br><br>   * Connector: Indicates the connector used to join these segments.<br><br>   * Beginning Index: Indicates the level where the starting segment is located.<br><br>   * Ending Index: Indicates the level where the ending segment is located.<br><br>   * Source of Signing Parameter When Processing URL Signing for Video Manifests: In scenarios where video manifests need to be modified to add tokens to the video fragment URIs, this option indicates the path source used by CDN when calculating the token. Sources include:<br><br>      * Client Request URL: Indicates the path in the user request URL.<br><br>      * Video Fragment URI: Indicates the path in the video fragment URI.<br><br>      The starting level must be a positive integer, and the ending level can be either a positive or negative integer. The absolute values of both levels cannot be greater than the total number of levels. Additionally, the path segment at the starting level cannot be to the right of the path segment at the ending level.<br><br>   * If the ending level is a negative integer, it counts from the rightmost segment.<br><br>&nbsp;<br><br>      **Example:** <br><br>      Request path is `/a/b/c/d/e`, delimiter is `/`, connector is `-`.<br><br>      * If starting level is `1` and ending level is `-4`, the result is `a-b`.<br><br>      * If starting level is `2` and ending level is `-4`, the result is `b`.<br><br>      * If starting level is `3` and ending level is `-4`, error. The reason is that the path segment at the starting level is to the right of the path segment at the ending level.<br><br>* Custom URL Object: Represents certain objects in the user request URL. For this type, you can specify the following options:<br><br>   * Query Parameter: Represents a specific query parameter. You need to enter the name of the query parameter below.<br><br>   * Path Segment: Represents a directory in the path. You need to enter the directory level below. The level is a non\-zero integer, and its absolute value cannot be greater than the total number of levels. If the level is negative, it counts from the rightmost directory.<br><br>   * Delimiting options. For the obtained object, you can additionally specify the following options:<br><br>      * Value Not Delimited: Indicates the obtained object is the desired object. This is the default option.<br><br>      * Value Is Delimited: Indicates the obtained content needs to be split to extract the desired object. You need to specify the following options:<br><br>         * Delimiter: Indicates the delimiter used to split the content.<br><br>         * Timestamp Index: Indicates the level where the actual desired object is located after splitting the obtained content into multiple level segments. The level is a non\-zero integer, and its absolute value cannot be greater than the total number of levels. If the level is negative, it counts from the rightmost segment.<br><br>   * Source of Signing Parameter When Processing URL Signing for Video Manifests: See the description of this configuration in **Path Segments**.<br><br>* Request Domain: Represents the request domain.<br><br>* Referer: Represents the Referer header in the user request.<br><br>* Origin: Represents the Origin header in the user request.<br><br>* Client IP: Represents the client IP address that sent the user request.<br><br>* User\-Agent: Represents the User\-Agent header in the user request.<br><br>* Custom Header: Represents the header you specify. You need to enter the header below. This header cannot be Referer, Origin, or User\-Agent. Note that:<br><br>   * If the header you specify doesn't exist, the object value will be empty ("").<br><br>   * For input requirements of this configuration, see [Configuration Input Requirements](https://docs.byteplus.com/en/docs/18/46937#configuration-input-requirements).<br><br>* Cookie: Represents a cookie in the user request. You need to specify the cookie's key below, and CDN will get the cookie's value.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The cookie format must comply with <a href="https://datatracker.ietf.org/doc/html/rfc6265">RFC 6265</a>. Otherwise, CDN may not be able to get the cookie's value.   </div><br>   <br><br>* Full Path: Represents the complete path of the user request, not including query strings.<br><br>   * Source of Signing Parameter When Processing URL Signing for Video Manifests: See the description of this configuration in **Path Segments**. |
|Parameter Concatenation |Authentication Parameter Combination Method |Represents the connector used to join signing objects. Following the order of objects in the signing object list, CDN uses your specified connector to join these objects, resulting in a string. CDN calculates the token by applying the specified algorithms to the concatenated string of signing parameters.<br><br>&nbsp;<br><br>If you don't specify this configuration, it means the connector is empty ("").<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For input requirements of the connector, see <a href="https://docs.byteplus.com/en/docs/18/46937#configuration-input-requirements">Configuration Input Requirements</a>.</div><br> |
|Signing Algorithms |Connector |Represents the algorithms used to calculate the token. For the string obtained after concatenating signing objects, CDN applies your specified algorithm to this string to obtain the token. You can specify up to 5 algorithms, and CDN generates the token calculation formula in the order of algorithm appearance.<br><br>&nbsp;<br><br>The algorithms you can specify include: Base64, Base64URL, MD5, MD5_Bin, SHA\-1, SHA\-224, SHA\-256, SHA\-384, SHA\-512, SHA3\-224, SHA3\-256, SHA3\-384, SHA3\-512, UpperCase(), LowerCase().<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">UpperCase() converts the input string to uppercase, LowerCase() converts the input string to lowercase.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">MD5_Bin indicates applying the MD5 algorithm to the input string, with the algorithm reading the input string in binary mode.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you specify MD5_Bin, you must specify Base64URL as the next algorithm. Examples of correct and incorrect configurations are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Correct configuration: SHA\-1, MD5_Bin, Base64URL</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Correct configuration: SHA\-1, MD5_Bin, Base64URL, Base64URL, MD5_Bin, Base64URL</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Incorrect configuration: SHA\-1, MD5_Bin, Base64URL, Base64URL, MD5_Bin</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Incorrect configuration: SHA\-1, MD5_Bin</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Incorrect configuration: SHA\-1, MD5_Bin, SHA3\-256, Base64URL</div><br> |
|URL Signing for HLS Manifests |URL Signing for HLS Manifests |If the request URL points to an HLS manifest, you can configure whether to add tokens to video fragment URIs in the manifest.<br><br><br>* Enable: Indicates that before returning the HLS manifest, CDN will first add tokens to video fragment URIs under the `EXTINF` tag, then return the modified HLS manifest.<br><br>* Disable: Indicates that CDN will not modify the HLS manifest.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The HLS manifest must comply with <a href="https://datatracker.ietf.org/doc/html/rfc8216">RFC 8216</a>, otherwise CDN will not modify the manifest.</div><br><br><br>For CDN's default URL signing logic, as well as examples, see [Default URL Signing Logic for Video Manifests](https://docs.byteplus.com/en/docs/18/46937#default-url-signing-logic-for-video-manifests).<br><br>&nbsp;<br><br>**Notes**<br><br><br>* If **Get Token From** is **Request Header** or **Cookie**, you cannot enable **URL Signing for HLS Manifests**, this configuration will be grayed out.<br><br>* If the corresponding query parameter or directory level doesn't exist in the fragment URI, CDN won't rewrite that URI.<br><br>* If manifests are compressed, CDN cannot modify the manifests. Manifests may be compressed in the following scenarios:<br><br>   * When the origin server responds to CDN's back\-to\-origin request, it compresses the manifests. In this case, please configure the origin server not to compress HLS manifests.<br><br>   * In CDN, you have enabled "File Compression". In this case, please configure "File Compression" to filter out files with .m3u8 extension. |
||Apply URL Signing to Extra Tags |In HLS manifests, if there are URIs under other tags that need CDN to add tokens, you can specify these tags in this configuration. You need to enable this configuration, then click **Add Tag**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The input tags do not need to start with a hash symbol (#).</div><br><br><br>After you add the tags, CDN will not only add tokens to URIs under the `EXTINF` and `EXT-X-STREAM-INF` tags, but also add tokens to URIs within the tags you specified. See [Example](https://docs.byteplus.com/en/docs/18/46937#example-of-applying-url-signing-to-extra-tags). |
|URL Signing for DASH Manifests |URL Signing for DASH Manifests |If the request URL points to a DASH manifest, you can configure whether to add tokens to video fragment URIs in the manifest.<br><br><br>* Enable: Indicates that before returning the DASH manifest, CDN will first add tokens to video fragment URIs within the `initialization` and `media` attributes of the `SegmentTemplate` tag, then return the modified DASH manifest.<br><br>* Disable: Indicates that CDN will not modify the DASH manifest.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The DASH manifest must comply with <a href="https://www.iso.org/standard/83314.html">ISO/IEC 23009\-1:2022</a>, otherwise CDN will not modify the manifest.</div><br><br><br>For CDN's default URL signing logic as well as examples, see [Default URL Signing Logic for Video Manifests](https://docs.byteplus.com/en/docs/18/46937#default-url-signing-logic-for-video-manifests).<br><br>&nbsp;<br><br>**Notes**<br><br><br>* If **Get Token From** is **Request Header** or **Cookie**, you cannot enable **URL Signing for DASH Manifests**, this configuration will be grayed out.<br><br>* If the corresponding query parameter or directory level doesn't exist in the fragment URI, CDN won't rewrite that URI.<br><br>* If the DASH manifest is compressed, CDN cannot modify the manifest. Manifests may be compressed in the following scenarios:<br><br>   * When the origin server responds to CDN's back\-to\-origin request, it compresses the manifests. In this case, please configure the origin server not to compress DASH manifests.<br><br>   * In CDN, you have enabled "File Compression". In this case, please configure "File Compression" to filter out files with .mpd extension. |
||Template Parameter Substitution |Indicates whether to replace parameters in URIs under `SegmentTemplate` with actual values.<br><br><br>* When this configuration is enabled, CDN first replaces parameters in the video segment URI with actual values, then generates a token based on the URI containing actual values, and finally adds the token to the URI.<br><br>* When this configuration is disabled, the parameter names themselves are used as fixed strings for token generation.<br><br><br>When this configuration is enabled, only parameters that meet all of the following conditions will be replaced with actual values:<br><br><br>* The parameter is `$RepresentationID$`.<br><br>* Under SegmentTemplate, there is at least one URI that meets the following condition:<br><br>   * In this URI, at least one occurrence of `$RepresentationID$` is not in the last segment of the URI path.<br><br>* No other content can appear between `<SegmentTemplate ... />` and `<Representation .../>`.<br><br><br>Additionally, in the modified DASH Manifest, the original `SegmentTemplate` will be preserved.<br><br>&nbsp;<br><br>**Examples**<br><br><br>* URI is `/streams/$RepresentationID$M_$Number$.mp4` or `$RepresentationID$M_$Number$.mp4`. In this case, parameters in this URI won't be replaced because `$RepresentationID$` appears in the last segment of the path.<br><br>* URI is `/streams_$RepresentationID$M/init-$Number$.mp4`. In this case, the `$RepresentationID$` parameter in this URI will be replaced, but `$Number$` won't be replaced.<br><br>* The Manifest content includes `<SegmentTemplate ... /><ContentComponent .../><Representation ... />`. In this case, parameters in the URI won't be replaced because other content appears between `<SegmentTemplate ... />` and `<Representation ... />`.<br><br>* The `SegmentTemplate` content is `<SegmentTemplate initialization="$RepresentationID$/$RepresentationID$-init.m4s" media="/media/$RepresentationID$-$Number$.m4s">`. This example meets the requirements because under this SegmentTemplate, there is a URI where one occurrence of $RepresentationID$ is not in the last segment of the path.<br><br><br>See the [Complete Examples](https://docs.byteplus.com/en/docs/18/46937#template-parameter-substitution-examples) below. |
|Custom Signing Settings | |Represents extended configuration of URL signing for video manifests. You can only enable this configuration when **URL Signing for HLS Manifests** or **URL Signing for DASH Manifests** is enabled, or both are enabled.<br><br>&nbsp;<br><br>In this configuration, you can set the following:<br><br><br>* Add Token To: Indicates how CDN adds tokens to video fragment URIs.<br><br>* Token generation: When **Custom Signing Settings** is enabled, you need to separately specify a series of objects. CDN concatenates these objects into a token and adds it to the video fragment URI.<br><br><br>After this configuration is enabled, CDN no longer modifies video manifests based on the default URL signing logic, but based on the custom URL signing logic instead.<br><br><br>* For default URL Signing logic, see [Default URL Signing Logic for Video Manifests](https://docs.byteplus.com/en/docs/18/46937#default-url-signing-logic-for-video-manifests).<br><br>* For custom URL signing logic, see [Custom URL Signing Logic for Video Manifests](https://docs.byteplus.com/en/docs/18/46937#custom-url-signing-logic-for-video-manifests). |
| |Add Token To |Indicates how CDN adds generated tokens to video fragment URIs. This configuration has the following options:<br><br><br>* Query Parameter: Indicates setting the specified query parameter in the URI to the token.<br><br>   * If the query parameter doesn't exist in the URI, CDN will add this query parameter.<br><br>   * If the query parameter already exists in the URI, its value will be set to the token.<br><br>* Path Segment: Indicates adding the token to the URI path as a directory at the specified level.<br><br>   * You need to specify the directory level below. The level is a non\-zero integer.<br><br>      * If the level is a positive integer, it counts from the leftmost directory in the path to locate the corresponding directory.<br><br>      * If the level is a negative integer, it counts from the rightmost directory in the path.<br><br>         Example:<br><br>      * For video fragment URI `/dir1/dir2/videoclip1.ts`, you need to add the token to this path as the first directory. In this case, you can specify the path segment as `1` or `-3`.<br><br>   * If this specified segment doesn't exist in the URI, CDN won't rewrite that URI. |
| |Connector |Indicates the connector used to join signing objects. Following the order of objects in the signing object list, CDN uses your specified connector to join these objects to generate the token to be added to video fragment URIs.<br><br>&nbsp;<br><br>If you don't specify this configuration, it means the connector is empty (""). |
| |Token Concatenated From |Represents a list of objects. CDN concatenates these objects to generate the token to be added to video fragment URIs. Click **Add Parameter** to add an object. Object types include:<br><br><br>* Custom URL Object in User Request: See the description of **Custom URL Object** in **Signing Parameters** above.<br><br>* Fixed String: See the description of **Fixed String** in **Signing Parameters** above.<br><br>* Path Segments in User Request: See the description of **Path Segments** in **Signing Parameters** above.<br><br>* Token Timestamp from User Request: Represents the token timestamp obtained from the user request. See the description of **Expiration Time** above.<br><br>* Token from User Request: Represents the token calculated by CDN based on **Signing Parameters**.<br><br>* Full Path of User Request: Represents the complete path of the user request, not including query strings. |
|Other Settings |URL Signing for Origin Requests |Indicates whether to include the token from user requests in origin requests.<br><br>&nbsp;<br><br>This configuration has the following options:<br><br><br>* Exclude Token from Origin Requests: Do not include the token in origin requests.<br><br>* Include Token in Origin Requests: Include the token in origin requests. The token appears in the same position as specified in **Get Token From**. In this case, disable URL authentication on the origin server. |
||Format Preference for Video Fragment URI |Specifies the format of the rewritten video fragment URI. This configuration has the following options:<br><br><br>* Default: Uses the **Absolute Path** mode.<br><br>* Relative Path: Keeps the current URI format. Note that this option is not applicable and will be grayed out if **Get Token From** or **Get Timestamp From** is set to **Path Segment**.<br><br>* Absolute Path: If the URI is a relative path, CDN converts it to an absolute path. If the URI is an absolute path or full URL, the current URI format is kept.<br><br>* Full URL: If the URI is an absolute path or relative path, CDN converts it to full URL. |
||Query from User Request |Indicates whether the rewritten video fragment URI includes all query parameters from the user request URL except those representing token and token timestamp. This configuration has the following options:<br><br><br>* Ignore: The rewritten segment URI will not include these query parameters.<br><br>* Inherit: The rewritten segment URI will include these query parameters. |
||Handling of Identical Parameters |This configuration appears when **Query from User Request** is set to **Inherit**. This setting specifies how to handle cases where the same query parameter exists in both the video fragment URI and the user request URL. This configuration has the following options:<br><br><br>* Use Value from Video Fragment URI: Uses the parameter value from the video fragment URI.<br><br>* Use Value from User Request URL: Uses the parameter value from the user request URL. |
||Original Query in Video Fragment URI |Indicates whether the rewritten video fragment URI retains the original query parameters in the URI. This configuration has the following options:<br><br><br>* Keep: The rewritten segment URI will retain these query parameters.<br><br>* Discard: The rewritten segment URI will not retain these query parameters. |


<span id="configuration-input-requirements"></span>
## Configuration Input Requirements


|**Configuration** |**Input Requirements** |
|---|---|
|Signing Key |The length of both primary and secondary authentication keys should be 6\-40 characters. |
|Get Token From |Input requirements for **Query Parameter**, **Request Header**, and **Cookie** are as follows:<br><br><br>* Length must be 1 to 100 characters.<br><br>* Can only contain letters, numbers, underscores (_), hyphens (\-), periods (.), commas (,), exclamation marks (!).<br><br>* Cannot contain only symbols or only numbers. |
|Expiration Time |Related configuration input requirements are the same as **Get Token From**. |
|Signing Parameters |Input requirements for **Fixed String**, **Delimiter**, **Concatenation** are as follows:<br><br><br>* The length of the fixed string is 1 to 20 characters. The length of both the delimiter and the connector is 1 character.<br><br>* Can only contain letters, numbers, underscores (_), hyphens (\-), forward slashes (/), exclamation marks (!).<br><br><br>Input requirements for **Query Parameter** and **Custom Header** are the same as their corresponding parameters in **Get Token From**. |
|Connector |* Length must be 1 to 20 characters.<br><br>* Can only contain letters, numbers, underscores (_), hyphens (\-), forward slashes (/), exclamation marks (!). |
|Rule Name |Length cannot exceed 120 characters and can contain Chinese characters, letters, numbers, hyphens (\-), underscores (_), and spaces. One Chinese character counts as 3 characters. |


<span id="default-url-signing-logic-for-video-manifests"></span>
## Default URL Signing Logic for Video Manifests

CDN rewrites video fragment URIs according to the following steps:


1. Determine the format of the video fragment URI and perform initial rewriting:

   * If the format is absolute path or full URL, skip step 1.

   * If the format is relative path, CDN rewrites the URI into absolute path.

2. Based on the settings of **Get Token From** and **Get Timestamp From**, CDN performs further URI rewriting.

   * If **Get Token From** or **Get Timestamp From** is **Query Parameter**, CDN sets the corresponding query parameter in the URI as the token or token timestamp. If this query parameter doesn't exist, CDN adds it to the URI.

   * If **Get Token From** or **Get Timestamp From** is **Path Segment**, CDN inserts a directory at the corresponding directory level in the URI and sets this directory as the token or token timestamp. If CDN cannot set the directory at this level in the URI, it will not rewrite the directories in the URI.


Additionally,


* CDN retains the original query parameters in the video fragment URI.

* CDN does not add query parameters from the user request URL to the video fragment URI.


**Examples**

Assume that **Get Token From** is set to the second directory in the request path, and **Get Timestamp From** is set to the query parameter `param1`. The token is `r5Bp7zX9k2Lc`, and the token timestamp is `1725786731`. The user request URL is `https://www.example.com/signed/test.m3u8?param1=1725786731&hello=world`.


* If the video fragment URI to be rewritten is `/a/segment1.ts?year=2024`, which is an absolute path, the rewritten video fragment URI will be `/a/r5Bp7zX9k2Lc/segment1.ts?year=2024&param1=1725786731`.

* If the URI to be rewritten is `segment1.ts?year=2024`, which is a relative path, the rewritten URI will be `/signed/r5Bp7zX9k2Lc/segment1.ts?year=2024&param1=1725786731`.

* If the URI to be rewritten is `/segment1.ts?year=2024`, which is an absolute path, since it's impossible to set the second directory in this URI, CDN will not add the token to this URI and will only add the token timestamp. The rewritten URI will be `/segment1.ts?year=2024&param1=1725786731`.

* If the URI to be rewritten is `https://www.example.com/a/segment1.ts?year=2024`, which is a full URL, the rewritten URI will be `https://www.example.com/a/r5Bp7zX9k2Lc/segment1.ts?year=2024&param1=1725786731`.


**Example of URL signing for HLS Manifest**

Assume that the token source is the first directory in the user request path, the timestamp source is the second directory in the user request path. The token is `r5Bp7zX9k2Lc`, and the timestamp is `1725786731`. The HLS manifest on the origin server contains the following content.

```xml
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0

#EXTINF:10,
/videos/segment0.ts
#EXT-X-ENDLIST
```


The content of the manifest with URL signing is as follows:

```xml
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0

#EXTINF:10,
/r5Bp7zX9k2Lc/1725786731/videos/segment0.ts
#EXT-X-ENDLIST
```


**Example of URL signing for MPD manifest**

Assume that the token source is the first directory in the user request path, the timestamp source is the second directory in the user request path. The token is `r5Bp7zX9k2Lc`, and the timestamp is `1725786731`. The DASH manifest on the origin server contains the following content.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     type="static"
     mediaPresentationDuration="PT0H10M0S"
     minBufferTime="PT2S">
  <Period duration="PT0H10M0S">
    <AdaptationSet mimeType="video/mp4" codecs="avc1.640028" frameRate="25/1">
      <Representation id="1" bandwidth="2000000" width="1280" height="720">
        <SegmentTemplate initialization="/videos/init.mp4"
                         media="/segments/seg-$Number$.m4s"
                         startNumber="1"
                         timescale="1000"
                         duration="4000"/>
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


The content of the manifest with URL signing is as follows:

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="static" minBufferTime="PT2S">
  <Period>
    <AdaptationSet mimeType="video/mp4" codecs="avc1.640028">
      <Representation bandwidth="2000000">
        <SegmentTemplate initialization="/r5Bp7zX9k2Lc/1725786731/videos/init.mp4" media="/r5Bp7zX9k2Lc/1725786731/segments/seg-$Number$.m4s" timescale="1000" duration="4000" />
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


<span id="example-of-applying-url-signing-to-extra-tags"></span>
## Example of Applying URL Signing to Extra Tags

Suppose the content of the HLS manifest on the origin server is as follows.

```xml
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080,CODECS="avc1.64002A,mp4a.40.2",AUDIO="audio"
/video/high/stream.m3u8
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="English",LANGUAGE="en",DEFAULT=YES,AUTOSELECT=YES,URI="/audio/en/audio.m3u8"
```


In this manifest, the `EXT-X-STREAM-INF` tag specifies the video stream information, and the `EXT-X-MEDIA` tag specifies the audio stream information. You need CDN to rewrite all URIs under the tags in the manifest.

In this scenario, if you only enable **URL Signing for HLS Manifests**, CDN will only rewrite the URI under the `EXT-X-STREAM-INF` tag. Therefore, you need to enable **Apply URL Signing to Extra Tags**, add the `EXT-X-MEDIA` tag, and then save the configuration.

Assume that the token source is the first directory in the user request path, the timestamp source is the second directory in the user request path. The token is `r5Bp7zX9k2Lc`, and the timestamp is `1725786731`. The modified manifest is as follows:

```xml
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080,CODECS="avc1.64002A,mp4a.40.2",AUDIO="audio"
/r5Bp7zX9k2Lc/1725786731/video/high/stream.m3u8
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="English",LANGUAGE="en",DEFAULT=YES,AUTOSELECT=YES,URI="/r5Bp7zX9k2Lc/1725786731/audio/en/audio.m3u8"
```


<span id="custom-url-signing-logic-for-video-manifests"></span>
## Custom URL signing logic for video manifests

In **Custom Signing Settings**, you need to specify a series of objects. Typically, these objects contain the token from user request and token timestamp. CDN concatenates the objects you specify to generate a token and adds it to the location you specify in the video fragment URI.

**Example**

In **Custom Signing Settings**, the objects you specify are: token from the user request, token timestamp, fixed string. The token is `r5Bp7zX9k2Lc`, the timestamp is `1725786731`, the fixed string is `abc123`, and the connector is `-`. Additionally, you specify to add the token to the second directory in the video fragment URI. If the video fragment URI before rewriting is `/a/b/1.ts`, the URI after rewriting becomes `/a/r5Bp7zX9k2Lc-1725786731-abc123/b/1.ts`.

<span id="template-parameter-substitution-examples"></span>
## Template Parameter Substitution Examples

Assume that the token source is the first directory in the user request path, the timestamp source is the second directory in the user request path. The token is `r5Bp7zX9k2Lc`, and the timestamp is `1725786731`.

**Example 1: No Sub\-elements Under Both SegmentTemplate and Representation**

The content of the manifest before parameter replacement is as follows:

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     minBufferTime="PT1.5S"
     type="static"
     mediaPresentationDuration="PT704S"
     profiles="urn:mpeg:dash:profile:isoff-live:2011">
    <Period duration="PT250S">
        <AdaptationSet>
            <SegmentTemplate timescale="12288" duration="24576" media="BBB_720_$RepresentationID$M/video-$Number$.mp4" initialization="BBB_720_$RepresentationID$M/video-init-$Number$.mp4"/>
            <Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" bandwidth="980104"/>
            <Representation id="2" mimeType="video/mp4" codecs="avc1.4d401f" bandwidth="1950145"/>
        </AdaptationSet>
    </Period>
</MPD>
```


The content of manifest after parameter replacement is as follows:

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     minBufferTime="PT1.5S"
     type="static"
     mediaPresentationDuration="PT704S"
     profiles="urn:mpeg:dash:profile:isoff-live:2011">
    <Period duration="PT250S">
        <AdaptationSet>
            <SegmentTemplate timescale="12288" duration="24576" media="BBB_720_$RepresentationID$M/video-$Number$.mp4" initialization="BBB_720_$RepresentationID$M/video-init-$Number$.mp4"/>
            <Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" bandwidth="980104">
              <SegmentTemplate timescale="12288" duration="24576" media="/r5Bp7zX9k2Lc/1725786731/signed/BBB_720_1M/video-$Number$.mp4" initialization="/r5Bp7zX9k2Lc/1725786731/signed/BBB_720_1M/video-init-$Number$.mp4"/>
            </Representation>
            <Representation id="2" mimeType="video/mp4" codecs="avc1.4d401f" bandwidth="1950145">
              <SegmentTemplate timescale="12288" duration="24576" media="/r5Bp7zX9k2Lc/1725786731/signed/BBB_720_2M/video-$Number$.mp4" initialization="/r5Bp7zX9k2Lc/1725786731/signed/BBB_720_2M/video-init-$Number$.mp4"/>
            </Representation>
        </AdaptationSet>
    </Period>
</MPD>
```


**Example 2: No Sub\-elements Under SegmentTemplate, Has Sub\-elements Under Representation**

The content of the manifest before parameter replacement is as follows:

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="static">
    <Period>
        <AdaptationSet mimeType="audio/mp4">
            <SegmentTemplate duration="4000" initialization="/video/$RepresentationID$/init.mp4" media="/video/$RepresentationID$/seg-$Number$.m4s" timescale="1000"/>
            <Representation bandwidth="71514" codecs="mp4a.40.2" id="audio/en/mp4a/1">
                <AudioChannelConfiguration value="2"/>
            </Representation>
        </AdaptationSet>
    </Period>
</MPD>
```


The content of manifest after parameter replacement is as follows:

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="static">
    <Period>
        <AdaptationSet mimeType="audio/mp4">
            <SegmentTemplate duration="4000" initialization="/video/$RepresentationID$/init.mp4" media="/video/$RepresentationID$/seg-$Number$.m4s" timescale="1000"/>
            <Representation bandwidth="71514" codecs="mp4a.40.2" id="audio/en/mp4a/1">
              <SegmentTemplate duration="4000" initialization="/r5Bp7zX9k2Lc/1725786731/video/audio/en/mp4a/1/init.mp4" media="/r5Bp7zX9k2Lc/1725786731/video/audio/en/mp4a/1/seg-$Number$.m4s" timescale="1000"/>
                <AudioChannelConfiguration value="2"/>
            </Representation>
        </AdaptationSet>
    </Period>
</MPD>
```


**Example 3: Has Sub\-elements Under SegmentTemplate, No Sub\-elements Under Representation**

The content of the manifest before parameter replacement is as follows:

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="dynamic" minBufferTime="PT6S">
  <Period>
    <AdaptationSet contentType="video" segmentAlignment="true">
      <SegmentTemplate timescale="90000" initialization="/media/$RepresentationID$/$RepresentationID$-init.m4s" media="/media/$RepresentationID$/$RepresentationID$-$Number$.m4s">
        <SegmentTimeline>
          <S d="540000" r="19" t="80010231598"/>
        </SegmentTimeline>
      </SegmentTemplate>
      <Representation id="360p" mimeType="video/mp4" codecs="avc1.4d001e" bandwidth="502000" />
    </AdaptationSet>
  </Period>
</MPD>
```


The content of manifest after parameter replacement is as follows:

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="dynamic" minBufferTime="PT6S">
  <Period>
    <AdaptationSet contentType="video" segmentAlignment="true">
        <SegmentTemplate timescale="90000" initialization="/media/$RepresentationID$/$RepresentationID$-init.m4s" media="/media/$RepresentationID$/$RepresentationID$-$Number$.m4s">
          <SegmentTimeline>
            <S d="540000" r="19" t="80010231598"/>
          </SegmentTimeline>
        </SegmentTemplate>
      <Representation id="360p" mimeType="video/mp4" codecs="avc1.4d001e" bandwidth="502000" >
        <SegmentTemplate timescale="90000" initialization="/r5Bp7zX9k2Lc/1725786731/media/360p/360p-init.m4s" media="/r5Bp7zX9k2Lc/1725786731/media/360p/360p-$Number$.m4s">
          <SegmentTimeline>
            <S d="540000" r="19" t="80010231598"/>
          </SegmentTimeline>
        </SegmentTemplate>
     </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


<span id="cache-purge"></span>
## Cache Purge

After you enable URL authentication, refer to the following guidelines if you need to initiate a cache purge operation for requested files:


|**Source of Token or Token Timestamp** |**Purge Operation Guidelines** |**Additional Notes** |
|---|---|---|
|Query parameter |When initiating a purge operation, the URL you specify must include query parameters that represent the token or token timestamp. |You can configure the "cache key" feature in the rules engine or general configuration to exclude query parameters that represent the token or token timestamp. This way, you won't need to include these query parameters in the URL when initiating a purge operation. |
|Path Segment |When initiating a purge operation, the URL you specify cannot contain the token and token timestamp. | |
|Request header |Cannot perform purge operations by specifying file URLs. |You can configure the "cache key" feature in the rules engine to exclude request headers or cookies that represent the token or token timestamp. This way, you can perform purge operations by specifying file URLs. |
|Cookie |||


<span id="examples"></span>
### Examples

**Example 1**

Suppose the token source is the query parameter `token-param`, and the token timestamp source is the second directory in the request path. The request URL is `https://www.example.com/files/1747993083/chinese/myfile?token-param=sadfasdfasf`.


* If you haven't configured the "cache key" feature to exclude `token-param`, when initiating a purge operation, your specified URL should be `https://www.example.com/files/chinese/myfile?token-param=sadfasdfasf`.

* If you have configured the "cache key" feature to exclude `token-param`, when initiating a purge operation, your specified URL should be `https://www.example.com/files/chinese/myfile`.


**Example 2**

Suppose the token source is the first directory in the request path, and the token timestamp source is the second directory in the request path. The request URL is `https://www.example.com/files/sadfasdfasf/1747993083/chinese/myfile`. In this case, when initiating a purge operation, your specified URL should be `https://www.example.com/files/chinese/myfile`.

<span id="token-calculation-sample-code"></span>
## Token Calculation Sample Code

The token included in client requests can be provided by a dedicated signing server or generated on the client side. You can refer to the following sample code to implement the token calculation logic on the client or signing server using your preferred programming language.

The sample code includes the following parts:


* Type\-F configuration module. You can define Type\-F configuration through any of the following methods:

   * JSON configuration.

   * Struct, which is only available in the Go and Java sample code.

* Token calculation module: Generate a token based on your defined Type\-F configuration and add the token to the request.


You can specify a request URL for testing in the sample code. The sample code will generate a request containing the token and print the request body and request URL.

**Sample Code for Go**

Define Type\-F configuration using JSON

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dad81b2171083a5024a24f29bd1a6caf.txt" name="TypeF for Go_JSON.txt">TypeF for Go_JSON.txt</Attachment>


Define Type\-F configuration using the `AuthRulesF` struct

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d6ccf4f3a460da2e13ae0d99490dbb0.txt" name="TypeF for Go_Struct.txt">TypeF for Go_Struct.txt</Attachment>


**Sample Code for Python**

Define Type\-F configuration using JSON

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f621b1613dda2f805840baaa34b1ad41.txt" name="TypeF for Python_JSON.txt">TypeF for Python_JSON.txt</Attachment>


**Sample Code for PHP**

Define Type\-F configuration using JSON

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_76b52faf00b163847270cef67ec2595c.txt" name="TypeF for PHP_JSON.txt">TypeF for PHP_JSON.txt</Attachment>


**Sample Code for Java**

Define Type\-F configuration using JSON

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e7a18b115d911780249d47acdfcce3bf.txt" name="TypeF for Java_JSON.txt">TypeF for Java_JSON.txt</Attachment>


Define Type\-F configuration using the `JsonArray` struct

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_98bda910c299b729027745814011b4c1.txt" name="TypeF for Java_Struct.txt">TypeF for Java_Struct.txt</Attachment>
