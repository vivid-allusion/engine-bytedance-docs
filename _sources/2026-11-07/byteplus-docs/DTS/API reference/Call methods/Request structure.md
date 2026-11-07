---
title: "Request structure"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/request_structure"
---

<span id=".6K-35rGC57uT5p6E"></span>
## Request structure

This topic describes the API request structure information of Database Transmission Service (DTS).

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Endpoints

The regions currently opened are shown in the table below.


|**Region** ||**RegionId** |**Endpoints** |
|---|---|---|---|
|China |China (Shanghai) |cn\-shanghai |dts.cn\-shanghai.byteplusapi.com.cn |
||China (Beijing) |cn\-beijing |dts.cn\-beijing.byteplusapi.com.cn |
||China (Guangzhou) |cn\-guangzhou |dts.cn\-guangzhou.byteplusapi.com.cn |
||China (Hong Kong) |cn\-hongkong |dts.cn\-hongkong.byteplusapi.com |
|Overseas |Asia Pacific (Johor) |ap\-southeast\-1 |dts.ap\-southeast\-1.byteplusapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |dts.ap\-southeast\-3.byteplusapi.com |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For latency\-sensitive services, it is suggested to specify the Region in the request Header. For details, refer to <a href="https://docs.byteplus.com/en/docs/DTS/common_parameters">Common parameters</a>.</div>


* <div data-tips="true" data-tips-type="tip">The domain name is the access point of the API and does not represent the region where the product directly provides services.</div>



<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocol

Both HTTP and HTTPS request communication methods are supported. It is recommended that you use the more secure HTTPS method to send requests.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The HTTP POST request method is supported. Specifically, the supported Content\-Type of POST requests is `application/json` (recommended).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All requests must adopt the BytePlus <a href="https://docs.byteplus.com/en/docs/DTS/signature_mechanism">Signature mechanism</a>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Each API request contains the following two types of parameters:


* Common request parameters: A parameter that is used by every API is a common request parameter. For more details about common request parameters, refer to [Common parameters](https://docs.byteplus.com/en/docs/DTS/common_parameters).

* API\-specific request parameters: Parameters specific to each API. For more information on the request parameters of each API, refer to [API overview](https://docs.byteplus.com/en/docs/DTS/api_overview).


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
