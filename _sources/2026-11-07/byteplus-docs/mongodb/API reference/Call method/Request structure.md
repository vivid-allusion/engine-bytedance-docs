---
title: "Request structure"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/request-structure"
---

This topic introduces the request structure used by Document Database for MongoDB APIs.

<span id="9TeFSOVO"></span>
## Service endpoints

Document Database for MongoDB is now available in regions listed in the table below.


|Region ||**RegionId** |Endpoint |
|---|---|---|---|
|Chinese region |China (Beijing) |cn\-beijing |mongodb.cn\-beijing.byteplusapi.com.cn |
||China (Guangzhou) |cn\-guangzhou |mongodb.cn\-guangzhou.byteplusapi.com.cn |
||China (Shanghai) |cn\-shanghai |mongodb.cn\-shanghai.byteplusapi.com.cn |
||China (Hong Kong) |cn\-hongkong |mongodb.cn\-hongkong.byteplusapi.com |
|Overseas region |Asia Pacific (Johor) |ap\-southeast\-1 |mongodb.ap\-southeast\-1.byteplusapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |mongodb.ap\-southeast\-3.byteplusapi.com |


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocol

HTTPS protocol is supported for request communication, while the latter is recommended for sending requests to ensure higher security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The HTTPS POST request method is supported. The supported Content\-Type for POST requests is application/JSON (recommended).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All requests must adopt the BytePlus <a href="https://docs.byteplus.com/en/docs/mongodb/signature-mechanism">Signature mechanism</a>.</div>


<span id=".6K-35rGCLXVyaQ=="></span>
## Request URI

Call the MongoDB API services by sending HTTPS POST requests. The URL format for HTTPS requests is:

```json
POST {URI-scheme}://{Endpoint}/?Action={Action}&Version={Version} HTTP/1.1
```


Among them:


* `URI-scheme`: The protocol used for transferring requests. All APIs currently use the HTTPS protocol.

* `Endpoint`: The domain name or IP address of the server assigned to host the service endpoint. It is also called the URL. The URL of Document Database for MongoDB is `mongodb.<RegionId>.byteplusapi.com`. For more details, refer to [Service endpoints](https://docs.byteplus.com/en/docs/mongodb/request-structure#9TeFSOVO).

* `Action`: The action to be performed. Enter the name of the API to be called here. For the APIs supported by Document Database for MongoDB, refer to [API overview](https://docs.byteplus.com/en/docs/mongodb/api-overview).

* `Version`: The API version in the format `YYYY-MM-DD`. The API version of Document Database for MongoDB is `2022-01-01`.


For example, when calling the API to create a MongoDB instance in the Beijing region, the unencoded HTTPS request URI is as follows.

```json
https://mongodb.cn-beijing.byteplusapi.com/?Action=CreateDBInstance&Version=2022-01-01
```


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Each API request contains two types of parameters:


* Common request parameters: Parameters that are required for every API. For more details on common parameters, refer to [Common parameters](https://docs.byteplus.com/en/docs/mongodb/common-parameter).

* API\-specific request parameters: Parameters specific to each API. For more information on the request parameters of each API, refer to the API descriptions in [API overview](https://docs.byteplus.com/en/docs/mongodb/api-overview).


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
