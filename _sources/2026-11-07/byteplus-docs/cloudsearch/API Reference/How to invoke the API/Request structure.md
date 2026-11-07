---
title: "Request structure"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/request-structure"
---

This topic introduces information on the API request structure for Cloud Search.

<span id="通信协议"></span>
## Communication protocol

API requests can be communicated over HTTP or HTTPS. We recommend that you use HTTPS for higher security.

<span id="请求方法"></span>
## Request method

The Cloud Search API supports the HTTP POST request method. In a POST request, the Content\-Type field is set to `application/json` by default.

Requests must be signed using the BytePlus signature method. For more information, refer to [Signature method](https://docs.byteplus.com/en/docs/cloudsearch/signature-method).

<span id="请求参数"></span>
## Request parameters

Each API request contains the following two types of parameters:


* Common request parameters: parameters required by every API action.

* Action\-specific parameters: specific parameters unique to each API action.


<span id="字符编码"></span>
## Character encoding

All encoding is in `UTF-8`.
