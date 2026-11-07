---
title: "Request structure"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Request_structure"
---

This document describes the API request structure for Table Storage for HBase.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Endpoints

The regions where Table Storage for HBase is available are listed in the table below.


|**Available Regions** ||**RegionId** |**Service Access Address** |
|---|---|---|---|
|Chinese region<br><br> |China (Beijing) |cn\-beijing |hbase.cn\-beijing.byteplusapi.com.cn |
||China (Guangzhou) |cn\-guangzhou |hbase.cn\-guangzhou.byteplusapi.com.cn |
||China (Shanghai) |cn\-shanghai |hbase.cn\-shanghai.byteplusapi.com.cn |
||China (Hong Kong) |cn\-hongkong |hbase.cn\-hongkong.byteplusapi.com |
|Overseas region |Asia Pacific (Johor) |ap\-southeast\-1 |hbase.ap\-southeast\-1.byteplusapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |redis.ap\-southeast\-3.byteplusapi.com |


<span id="kzcIV9Uo"></span>
## Communication protocol

Requests support both HTTP and HTTPS. We recommend using HTTPS for enhanced security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The HTTP POST request method is supported. Specifically, the supported Content\-Type of POST requests is application/JSON (recommended).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All requests must adopt the BytePlus <a href="https://docs.byteplus.com/en/docs/HBase/Signature_mechanism">Signature mechanism</a>.</div>


<span id=".6K-35rGCLXVybA=="></span>
## Request URL

You can call the API service for Table Storage for HBase by sending an HTTPS POST request. The HTTPS request URL is formatted as follows:

```json
POST {URI-scheme}://{Endpoint}/?Action={Action}&Version={Version} HTTP/1.1
```


This includes:


* `URI-scheme`: The protocol used to transmit the request. All current APIs use the HTTPS protocol.

* `Endpoint`: The domain name or IP address of the server that hosts the service endpoint, also known as the service address. The service address for Table Storage for HBase is `hbase.<RegionId>.byteplusapi.com`. For more details, see [Service addresses](https://docs.byteplus.com/en/docs/HBase/Request_structure#.5pyN5Yqh5Zyw5Z2A).

* `Action`: The operation to be performed. This is the name of the API to call. For details about the APIs supported by Table Storage for HBase, see [API overview](https://docs.byteplus.com/en/docs/HBase/API_overview).

* `Version`: The API version number in `YYYY-MM-DD` format. The API version for Table Storage for HBase is `2018-01-01`.


For example, the following is an unencoded HTTPS request URL for creating an HBase instance.

```json
https://hbase.cn-beijing.byteplusapi.com.cn/?Action=CreateDBInstance&Version=2018-01-01
```


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Each API request contains the following two types of parameters:


* Common request parameters: A parameter that is used by every API is a common request parameter. For more details about common request parameters, refer to [Common parameters](https://docs.byteplus.com/en/docs/HBase/Common_parameters).

* API\-specific request parameters: Parameters specific to each API. For more information on the request parameters of each API, refer to the API descriptions in [API overview](https://docs.byteplus.com/en/docs/HBase/API_overview).


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
