---
title: "Common Data Processing Issues"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/About_datasets"
---

*To experience more Viking AI Search capabilities, visit: * [Viking AI Search, the all-in-one intelligent engine for enterprise search, recommendations, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)


---



If you encounter issues like data synchronization failures, slow processing, or display errors with BytePlus data services, this guide can help. It provides troubleshooting steps for common problems related to data import, processing, and usage, enabling you to quickly identify the cause and find a solution.

**How to use this guide?** 


* Quickly identify problems: Find your issue faster with categorized troubleshooting scenarios.

* Improve resolution efficiency: Reduce problem\-solving time with clear troubleshooting steps and solutions.


**Typical use cases**


* Data import and synchronization: Resolve issues such as data synchronization failures and inconsistent item counts.

* Data processing and display: Troubleshoot issues such as slow image processing, inaccessible links, and front\-end display errors.


&nbsp;


---



<span id="fa1ef09c"></span>
## Data synchronization failed

Troubleshooting based on error codes


|**Error code** |**Error code meaning** |**Troubleshooting items** |
|---|---|---|
|InvalidParameter |Invalid parameter |Check if the account_id and dataset_id are correct<br><br>Check if the dataset_id is configured |
|ErrCodeInvalidRequestBody |Request deserialization failed |Check if the request format is correct. For a sample of the correct format, see: https://www.volcengine.com/docs/85296/2123234?lang=zh |
|InvalidMediaCoverUrlError |Video/Image URL expired or inaccessible |Copy the link and paste it into a browser to verify that it opens. Replace it with a working link. |
|VideoSizeExceedsLimitError |Video size/duration exceeds the limit.<br><br> |(Maximum 10 GB/3.5 hours)<br><br> |
|ErrCodeInternalServiceError |Server\-side internal error, possibly caused by a timeout or network fluctuations. |Add a retry mechanism on the client side and extend the timeout configuration. |


<span id="e7a24aa5"></span>
## Slow data processing

For image and text data, most of the processing time is for handling images. The platform downloads the image from the client\-side using the URL, transfers it to the BytePlus TOS environment, and then performs image validation, resizing, and VLM enhancement. The following factors affect processing speed:


* Client\-side CDN capabilities, where rate limiting leads to longer processing times

* The number and size of images in a data record affect processing time; the more images and the larger their size, the longer the processing time.


**Suggestion:** 


* Wait for the process to complete.

* If you have large\-scale data upload requirements AND can guarantee your CDN's capacity, contact BytePlus to increase concurrency and speed up the process.


&nbsp;

<span id="f307b8af"></span>
## Data preview shows `Failed` or displaying `Image URL inaccessible`.

The `Image URL inaccessible` error in the `Data preview` means that BytePlus failed to retrieve the `Image`. It does not necessarily mean that the `Image` URL cannot be opened. You can check the following items in order:


1. `Copy` the `Image` URL into a browser to see if it opens. If it does not open, you need to provide a working URL.


Note: The `Image URL` must be a link to an `Image` itself, not to a webpage. Otherwise, data validation will fail, indexing will fail, and the `Image` cannot be used.


2. In your CDN provider's console, check the IP access control (allowlist/denylist) settings and `Confirm` that BytePlus's IP addresses are not blocked. (Contact your BytePlus representative for the list of IP addresses.) The BytePlus service uses this IP address to fetch your image resources. If your CDN policy blocks this IP, image fetching will fail. (Note: If the customer does not own the image source and cannot whitelist the IP, use the Base64 format.)

3. Check the traffic limit (QPS limit) configuration in your CDN provider's console to confirm that rate limiting is not causing fetch timeouts.

4. If your Wufu or data source is deployed overseas, use the Johor platform to avoid timeouts caused by unstable cross\-border public network connections.

5. Check if the image format meets the requirements

   * File size: Recommended: within 300 KB (larger files can cause response delays)

   * Base64 format: Must include a data header. Sample data: data:<MIME type\>;base64,<Base64\-encoded string\>


&nbsp;

<span id="58e77ff3"></span>
## The item count of the dataset does not match the imported item count

Possible reasons:


* Items in the dataset are deduplicated by their primary key. If a customer uploads duplicate data, the number of imported items will be greater than the number of items in the dataset.


**Suggestion:** 


* Invoke the ListItem API to query for existing items in the Datasets. You can then re\-import any missing items. For details, see [ListItems - Get the list of items in a dataset](https://docs.byteplus.com/docs/393/92273).


<span id="3a8636a3"></span>
## Possible reasons for a sudden spike in user events

BytePlus does not generate or augment a customer's user event data. This indicates that the customer uploaded the volume of data that caused the spike. There are several possible reasons:


* Major sales promotions

* Crawlers

* Duplicate uploads via the API


<span id="cf79db1d"></span>
## Cannot find the corresponding upload record in Datasets \> Activity history?

Activity history only records uploads for the last 7 days, so it is expected that records older than 7 days are not returned. If records within 7 days are not returned, contact BytePlus technical support to investigate.

<span id="58388931"></span>
## On the demo page, "Image not found" or "403" is displayed

Copy the image URL into your browser's address bar. If the image displays correctly in your browser but fails to load on the demo page, the cause is likely hotlink protection. The customer's image server is not configured to allow access from the BytePlus domain.

**Suggestion:** 

Configure your CDN to allow access from the BytePlus domain.

<span id="803c594f"></span>
## Is it possible to crawl and index HTML webpages?

This is not currently supported. You need to extract the information into structured data.

&nbsp;


---



*To learn more about Viking AI Search product capabilities, see: * [Viking AI Search, the integrated intelligent engine for enterprise search, recommendations, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)
