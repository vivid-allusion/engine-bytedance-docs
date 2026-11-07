---
title: "Request structure"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Request-structure"
---

This topic introduces the request structure used by PFS APIs.

<span id="d3ebb5ff"></span>
## Service endpoints

PFS is now available in regions listed in the table below.


|Region |RegionId |Endpoint |
|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |open.ap\-southeast\-1.byteplusapi.com |
|China(Hong Kong) |cn\-hongkong |open.cn\-hongkong.byteplusapi.com |


<span id="0bf2a292"></span>
## Communication protocol

HTTP and HTTPS protocols are supported for request communication, while the latter is recommended for sending requests to ensure higher security.

<span id="0e19587e"></span>
## Request method

The HTTP POST method is supported, where the recommended Content\-Type for POST requests is `application/json`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">Requests must use the BytePlus <a href="https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature">Calculating a signature</a>.</div>


<span id="a7ef3ee3"></span>
## Request URL

Call the Redis API services by sending HTTPS POST requests. The URL format for HTTPS requests is:

```JSON
POST {URI-scheme}://{Endpoint}/?Action={Action}&Version={Version} HTTP/1.1
```


Where:


* `URI-scheme`: The protocol used for transferring requests. All APIs currently use the HTTPS protocol.

* `Endpoint`： The domain name or IP address of the server assigned to host the service endpoint. It is also called the URL. The URL of PFS is `open.ap-southeast-1.byteplusapi.com`.

* `Action`： The action to be performed. Enter the name of the API to be called here. For the APIs supported by PFS, refer to [API overview](https://docs.byteplus.com/docs/pfs/API-overview).

* `Version`： API version in the format `YYYY-MM-DD`. The API version of PFS is `2022-01-01.`


<span id="0ff15512"></span>
## Request parameters

Every API request consists of two types of parameters:


* Common request parameters: Parameters that are required for every API. For more information on common request parameters, refer to [Common parameters](https://docs.byteplus.com/docs/pfs/Public-parameters).

* API\-specific request parameters: Parameters specific to each API. For more information on the request parameters of each API, refer to the API descriptions in [API overview](https://docs.byteplus.com/docs/pfs/API-overview).


<span id="e7abc013"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
