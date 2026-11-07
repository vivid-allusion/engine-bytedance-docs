---
title: "Request structure"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/request_structure_1"
---

This topic describes the API request structure of RDS for MySQL.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Endpoints

The following table lists the regions where RDS for MySQL is available.


|Region ||RegionId |Endpoints (new) |Endpoints (old) |
|---|---|---|---|---|
|Regions in China |China (Beijing) |cn\-beijing |rds\-mysql.cn\-beijing.byteplusapi.com.cn |rds.volcengineapi.com |
||China (Shanghai) |cn\-shanghai |rds\-mysql.cn\-shanghai.byteplusapi.com.cn |rds.volcengineapi.com |
||China (Guangzhou) |cn\-guangzhou |rds\-mysql.cn\-guangzhou.byteplusapi.com.cn |rds.volcengineapi.com |
||China (Hong Kong) |cn\-hongkong |rds\-mysql.cn\-hongkong.byteplusapi.com |rds.volcengineapi.com |
|Overseas regions |Asia Pacific (Johor) |ap\-southeast\-1 |rds\-mysql.ap\-southeast\-1.byteplusapi.com |rds.volcengineapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |rds\-mysql.ap\-southeast\-3.byteplusapi.com |\- |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To provide more stable and high\-quality services, RDS for MySQL has upgraded the service access addresses in some regions. The old service access address will still be available for some time in the future, but it will eventually stop providing service. It is recommended that you use the new service access address directly in the new business, and update the service access address used in the existing business as soon as possible.</div>


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocol

HTTP and HTTPS protocols are supported for request communication, while the latter is recommended for sending requests to ensure higher security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The HTTP POST request method is supported. Specifically, the supported` Content-Type` of POST requests is application/JSON (recommended).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All requests must adopt the BytePlus <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/signature_mechanism_1">Signature mechanism</a>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Each API request contains two types of parameters:


* Common request parameters: A parameter that is used by every API is a common request parameter. For more details on common request parameters, refer to [Common parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/common_parameters_1).

* API\-specific request parameters: Parameters specific to each API. For the request parameters of each API, refer to the detailed descriptions in the [API list](https://docs.byteplus.com/en/docs/RDS_for_MySQL/api_overview_1).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a sub\-user has only project\-level privileges, you must add the Project field and specify a project for which the sub\-user has privileges when using their AK and SK to call an API where InstanceID is an optional parameter.</div>


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
