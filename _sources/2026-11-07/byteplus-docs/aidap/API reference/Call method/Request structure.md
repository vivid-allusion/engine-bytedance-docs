---
title: "Request structure"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Request_structure"
---

This topic introduces the API request structure of the AI Native Database Platform.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Endpoints

The table below lists the regions where the AI Native Database Platform service is available.


|Region |RegionId |Endpoints |
|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |aidap.ap\-southeast\-1.byteplusapi.com |


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocol

HTTP and HTTPS protocols are supported for request communication, while the latter is recommended for sending requests to ensure higher security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The HTTP POST request method is supported. Specifically, the supported` Content-Type` of POST requests is application/JSON (recommended).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All requests must adopt the BytePlus <a href="https://docs.byteplus.com/en/docs/330/Signature_mechanism">Signature mechanism</a>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Each API request contains two types of parameters:


* Common request parameters: A parameter that is used by every API is a common request parameter. For more details on common request parameters, refer to [Common parameters](https://docs.byteplus.com/en/docs/330/Common_parameters).

* API\-specific request parameters: Parameters specific to each API. For the request parameters of each API, refer to the documentation of each interface through the [API list](https://docs.byteplus.com/en/docs/330/API_overview).


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
