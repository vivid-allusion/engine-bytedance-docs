---
title: "File Compression"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-file-compression"
---

To reduce file size, improve transmission speed, and lower traffic costs, you can enable file compression in BytePlus CDN. This guide shows how to enable the feature and create rules to specify which files to compress and which algorithm (Gzip or Brotli) to use. When a request matches a rule, CDN automatically compresses and returns the file, caching both the original and compressed versions to accelerate future requests.

After enabling File Compression, you can create rules to specify which types of files need compression and the compression algorithm to use. When CDN receives a request, if the request matches a rule, CDN compresses the requested file according to the rule configuration and then returns the compressed file. This feature reduces file sizes, which improves file transfer speeds and lowers traffic costs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a request matches a compression rule, CDN not only returns the compressed file but also caches the compressed file. In other words, for the same file, CDN caches both the original and compressed versions.</div>


<span id="supported-compression-algorithms"></span>
## Supported Compression Algorithms

File Compression supports the Gzip and Brotli compression algorithms.


* Gzip is a widely used data compression format on the Internet; Gzip can typically compress plain text files to about 40% of their original size.

* Brotli is a compression algorithm introduced by Google in September 2015, offering significant improvements in compression ratio and performance over Gzip. Currently, the majority of browsers support Brotli.


<span id="relevant-request-and-response-headers"></span>
## Relevant Request and Response Headers

If a client can handle compressed data, its request must include the `Accept-Encoding` header, which specifies the supported compression algorithms. Algorithm weights are optional. For example, `Accept-Encoding: gzip;q=0.8, br;q=0.6` means the client supports both Gzip and Brotli, but Gzip is preferred. If this header is omitted, it means the client cannot handle compressed data.

The CDN response includes the `Content-Encoding` header, indicating the compression algorithm used for the response file.

<span id="supported-file-types"></span>
## Supported File Types

Currently, File Compression only supports compressing files whose `Content-Type` response header is of the following types. If the file type you need to compress is not on this list, please [submit a ticket](https://console.byteplus.com/workorder/create).


* text/html

* text/xml

* text/plain

* text/css

* application/javascript

* application/x\-javascript

* application/rss+xml

* text/javascript

* image/tiff

* image/svg+xml

* application/json

* application/xml


<span id="precautions"></span>
## Precautions


* CDN only compresses files for GET requests.

* If the origin server has enabled compression and the `Content-Encoding` header of the origin server's response is not empty and not `identity`, it indicates that the file has already been compressed by the origin server. In this case, the CDN will not compress the file again.

* If both Brotli and Gzip are selected in the File Compression configuration, and the `Accept-Encoding` header value in the user request includes both `br` and `gzip`, there are two scenarios:

   * If `Accept-Encoding` does not include the weight of algorithms, the CDN will compress the requested file using the Brotli algorithm.

   * If `Accept-Encoding` includes the weights of algorithms, the CDN will compress the requested file using the algorithm with the higher weight.

* If a range request matches a compression rule, then:

   * If the CDN edge node has a compressed copy of the requested file, CDN extracts the requested segment from the compressed copy and returns the **compressed** segment.

   * If the CDN edge node does not have a compressed copy of the requested file, CDN returns the **uncompressed** segment.

* If the origin server file is configured with an MD5 verification mechanism, do not enable the File Compression function.

* All browsers support Gzip. Older versions of browsers may not be compatible with Brotli. You can [check browser compatibility for Brotli](https://caniuse.com/?search=Brotli).

* If the `Vary` header in the origin server's response does not follow the [RFC standard](https://datatracker.ietf.org/doc/html/rfc7231#section-7.1.4), it may prevent file compression from working correctly.


<span id="steps"></span>
## Steps


1. Open the **File Compression** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enabled**.

3. Click **Add Rule**. You can add up to 50 rules.

4. Refer to the [Configuration Description](https://docs.byteplus.com/en/docs/18/6583#configuration-description) below to set up the rules.

5. After configuration, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aefab889f8655dfe4d644a2ca187a461.png) </span>

<span id="configuration-description"></span>
## Configuration Description


|**Configuration** |**Description** |
|---|---|
|Filter Type |Indicates the filter type in the rule. This configuration has the following options:<br><br><br>* **URL Path Extension**: Indicates the extension at the end of the path.<br><br>* **URL Path Directory**: Indicates a directory in the path.<br><br>* **URL Path**: Indicates the path in the request URL.<br><br>* **Content\-Type**: Indicates the `Content-Type` header in the request.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only have one <strong>Content\-Type</strong> rule in the rule list. This rule has the lowest priority, and you cannot adjust its priority.</div><br> |
|Patterns |Indicates the filter value in the rule. The filter value is case\-insensitive. Separate multiple values with a semicolon (;). The total length cannot exceed 1,024 characters, and the values cannot contain the following characters:<br><br><br>* Double slashes (//), spaces, dollar signs ($), question marks (?).<br><br><br>Additionally,<br><br><br>* If the **Rule Type** is **URL Path Extension**, the filter value is one or more file extensions. The file extension does not need to start with a period (.). For example: `png;txt`.<br><br>* If the **Rule Type** is **URL Path Directory**, the filter value is one or more directory paths. The directory path must start and end with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If the **Rule Type** is **URL Path**, the filter value is one or more file paths. The file path must start with a slash (/), and can contain an asterisk (\*) to indicate one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If the **Rule Type** is **Content\-Type**, the console provides the following options:<br><br>   * **Default**: Indicates that the rule applies to all the following file types: text/html, text/xml, text/plain, text/css, application/javascript, application/x\-javascript, application/rss+xml, text/javascript, image/tiff, image/svg+xml, application/json, application/xml, text/plain; charset=utf\-8.<br><br>   * **Customize**: Indicates that the rule applies to the file types you specify. You can check one or more file types from the list. You can also enter file types that are not in the file list. |
|File Size (Minimum) |Indicates a file size. If the size of the requested file is less than this value, the CDN will not compress the file. The value is in kilobytes (where 1 KB = 1,024 bytes) and can range from 0 to 2,147,483,647. If this value is set to 0, CDN compresses the file regardless of its size. |
|Compression Algorithm |Specifies the compression algorithm to use for requests that match the rule's filter conditions. This configuration has the following values:<br><br><br>* Gzip<br><br>* Brotli<br><br><br>When the CDN uses the Brotli algorithm to compress requested files, it uses compression level 6.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Brotli provides 12 compression levels, from 0 to 11. Level 0 offers the fastest compression speed with the lowest compression ratio, while level 11 provides the highest compression ratio but requires more computing resources and time.</div><br> |


<span id="rule-execution-logic"></span>
## Rule Execution Logic

When a user request is received, CDN processes rules sequentially in the order they appear in the list. During rule processing, CDN attempts to match the rule with the request. If any rule matches the request, CDN applies the compression configuration to the requested file and stops processing the remaining rules. You can drag rules to adjust their order in the list.
