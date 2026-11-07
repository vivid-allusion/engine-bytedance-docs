---
title: "BytePlus VOD API introduction"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction"
---

The BytePlus VOD APIs are HTTP\-based RESTful APIs that use signature algorithms for authentication. This document provides a comprehensive overview of how to interact with the VOD APIs, covering the initial setup, the detailed structure of an API request, and the format of the response. Following this guide will enable you to correctly construct and authenticate your API calls.

<span id="baf5850d"></span>
## Getting started


1. Contact your sales representative to activate BytePlus VOD for your BytePlus account.

2. After your service is enabled, log in to the [BytePlus console](https://console.byteplus.com/), click your account name in the upper right corner of the page, and then select **IAM** \> **Key Management** to get the Access Key ID (AK) and Secret Access Key (SK) of your account, which are used for API request authentication.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c0c5750-Obtain_the_AccessKey_ID_and_AccessKey_secret.JPEG) </span>


<span id="9a4c0290"></span>
## Request structure

A BytePlus VOD API request consists of the following components:


* **Protocol**: BytePlus VOD supports HTTP and HTTPS protocols. We recommend using HTTPS for enhanced API request security.

* **Region:** 

   
   |Region |Region code |Endpoint |
   |---|---|---|
   |Asia Pacific (Johor) |ap\-southeast\-1 |vod.byteplusapi.com |
   |Asia Pacific (Singapore) |ap\-singapore\-1 |vod.byteplusapi.com |
   

* **Request method**: Most of the BytePlus VOD APIs support both **GET** and **POST** methods, unless otherwise specified.

   * **GET**: Retrieves specified resources from the server. Common parameters can be added to headers and query string parameters.

   * **POST**: Adds resources or performs special operations on the server. Common parameters can be added to headers only.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Generally, it is recommended to use GET. If the parameter string is too long, it's recommended to use POST.   </div>
   

* **Request parameters**: When sending a request, you should include two types of parameters:

   * Common request parameters: These parameters are essential for identifying the account and interface signature. Every request must include these parameters. For detailed descriptions, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

   * Specific request parameters: Refer to the specific API reference for details regarding these parameters.

* **Request signature**: To ensure the security and integrity of API requests, BytePlus employs a signature mechanism. Clients are required to calculate a signature for the request parameters and transmit it to the API server for verification. If the signature verification fails, the server rejects the request. For details, see the following documentation:

   * [About the request signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-signature)

   * [Calculating a signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature)

   * [Example](https://docs.byteplus.com/en/docs/byteplus-platform/reference-example)

* **Character encoding**: API requests and responses are encoded in **UTF\-8**.


<span id="4a7528bb"></span>
## Response

<span id="cc3c4db9"></span>
### HTTP status codes

The HTTP status code for a successful request is always 200, and some failed requests may return error codes 4xx or 5xx.

<span id="f76f6bef"></span>
### Common response parameters

The common response parameters of BytePlus VOD are as follows.

<span id="d66f6db4"></span>
#### ResponseMetadata


|**Parameter** |**Type** |**Description** |
|---|---|---|
|RequestId |String |Request ID |
|Action |String |Action |
|Version |String |Version |
|Service |String |Service |
|Region |String |Region |
|Error |[ResponseError](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#709bf03f) |Error |


<span id="709bf03f"></span>
#### ResponseError


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Code |String |The error code |
|Message |String |The error message |
