---
title: "Request structure"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/request-structure"
---

This topic introduces the request structure used by Cache for Redis APIs.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service endpoints

Cache for Redis is now available in regions listed in the table below.


|Region ||**RegionId** |Endpoint |
|---|---|---|---|
|Chinese region |China (Beijing) |cn\-beijing |redis.cn\-beijing.byteplusapi.com.cn |
||China (Guangzhou) |cn\-guangzhou |redis.cn\-guangzhou.byteplusapi.com.cn |
||China (Shanghai) |cn\-shanghai |redis.cn\-shanghai.byteplusapi.com.cn |
||China (Hong Kong) |cn\-hongkong |redis.cn\-hongkong.byteplusapi.com |
|Overseas region |Asia Pacific (Johor) |ap\-southeast\-1 |redis.ap\-southeast\-1.byteplusapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |redis.ap\-southeast\-3.byteplusapi.com |


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocol

HTTPS protocol is supported for request communication, while the latter is recommended for sending requests to ensure higher security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The HTTPS POST request method is supported. The supported Content\-Type for POST requests is application/JSON (recommended).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All requests must adopt the BytePlus <a href="https://docs.byteplus.com/en/docs/redis/signature-mechanism">Signature mechanism</a>.</div>


<span id=".6K-35rGCLXVyaQ=="></span>
## Request URI

Call the Redis API services by sending HTTPS POST requests. The URL format for HTTPS requests is:

```JSON
POST {URI-scheme}://{Endpoint}/?Action={Action}&Version={Version} HTTP/1.1
```


Among them:


* `URI-scheme`: The protocol used for transferring requests. All APIs currently use the HTTPS protocol.

* `Endpoint`: The domain name or IP address of the server assigned to host the service endpoint. It is also called the URL. The service address for Cache for Redis is `redis.<RegionId>.byteplusapi.com`. For more details, refer to [Service endpoints](https://docs.byteplus.com/en/docs/redis/request-structure#.5pyN5Yqh5Zyw5Z2A).

* `Action`: The action to be performed. Enter the name of the API to be called here. For the APIs supported by Cache for Redis, refer to [API overview](https://docs.byteplus.com/en/docs/redis/api-overview).

* `Version`: The API version in the format `YYYY-MM-DD`. The API version of Cache for Redis is `2020-12-07`.


For example, when calling the API to create a Redis instance in the Beijing region, the unencoded HTTPS request URI is as follows.

```JSON
https://redis.cn-beijing.byteplusapi.com/?Action=CreateDBInstance&Version=2020-12-07
```


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Every API request consists of two types of parameters:


* Common request parameters: Parameters that are required for every API. For more details on common parameters, refer to [Common parameters](https://docs.byteplus.com/en/docs/redis/common-parameter).

* API\-specific request parameters: Parameters specific to each API. For more details on the request parameters of each API, refer to API descriptions in [API overview](https://docs.byteplus.com/en/docs/redis/api-overview).


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
