---
title: "Request structure"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/request_structure"
---

This topic describes the API request structure of RDS for PostgreSQL.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Endpoints

RDS for PostgreSQL is now available in the region listed in the table below.

&nbsp;


|Region |Region ID |Endpoints (new) |Endpoints (old) |
|---|---|---|---|
|China (Beijing) |cn\-beijing |rds\-postgresql.cn\-beijing.byteplusapi.com.cn |open.volcengineapi.com |
|China (Shanghai) |cn\-shanghai |rds\-postgresql.cn\-shanghai.byteplusapi.com.cn |open.volcengineapi.com |
|China (Guangzhou) |cn\-guangzhou |rds\-postgresql.cn\-guangzhou.byteplusapi.com.cn |open.volcengineapi.com |
|China (Hong Kong) |cn\-hongkong |rds\-postgresql.cn\-hongkong.byteplusapi.com |rds\-postgresql.cn\-hongkong.byteplusapi.com |
|Asia Pacific (Johor) |ap\-southeast\-1 |rds\-postgresql.ap\-southeast\-1.byteplusapi.com |open.volcengineapi.com |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |rds\-postgresql.ap\-southeast\-3.byteplusapi.com |rds\-postgresql.ap\-southeast\-3.byteplusapi.com |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In order to provide more stable and high\-quality services, RDS for PostgreSQL has upgraded some regional service access addresses. The old service access address will still be available for some time in the future, but it will eventually stop providing service. It is recommended that you use the new service access address directly in the new business, and update the service access address used in the existing business as soon as possible.</div>


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocol

HTTP and HTTPS protocols are supported for request communication, while the latter is recommended for sending requests to ensure higher security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The HTTP POST request method is supported. Specifically, the supported Content\-Type of POST requests is application/JSON (recommended).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All requests must adopt the BytePlus <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/signature_mechanism">Signature mechanism</a>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Each API request contains two types of parameters:


* Common request parameters: A parameter that is used by every API is a common request parameter. For more details on common request parameters, refer to [Common parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/common_parameters).

* API\-specific request parameters: Parameters specific to each API. For more information about the request parameters of each API, refer to the API descriptions in [API overview](https://docs.byteplus.com/en/docs/RDS_for_PG/api_references).


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
