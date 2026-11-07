---
title: "Request structure"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Request_structure"
---

<span id=".6K-35rGC57uT5p6E"></span>
## Request structure

This article describes the API request structure.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Endpoints

The regions currently opened are shown in the table below.


|Region ||RegionId |Endpoints |
|---|---|---|---|
| |China (Hong Kong) |cn\-hongkong |vedbm.cn\-hongkong.byteplusapi.com |
|Overseas |Asia Pacific (Johor) |ap\-southeast\-1 |vedbm.ap\-southeast\-1.byteplusapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |vedbm.ap\-southeast\-3.byteplusapi.com |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For latency\-sensitive services, it is suggested to specify the Region in the request Header. For details, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Common_parameters">Common parameters</a>.</div>


* <div data-tips="true" data-tips-type="tip">The domain name is the access point of the API and does not represent the region where the product or service is actually provided.</div>



<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocol

Both HTTP and HTTPS request communication methods are supported. It is recommended that you use the more secure HTTPS method to send requests.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The HTTP POST request method is supported. Specifically, the supported Content\-Type of POST requests is `application/JSON` (recommended).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All requests must adopt the BytePlus <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Signature_mechanism">Signature mechanism</a>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Each API request contains the following two types of parameters:


* Common request parameters: A parameter that is used by every API is a common request parameter. For more details about common request parameters, refer to [Common parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Common_parameters).

* API\-specific request parameters: Parameters specific to each API. For more information on the request parameters of each API, refer to the API descriptions in [API overview](https://docs.byteplus.com/en/docs/NDB_for_MySQL/API_overview_1).


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

`UTF-8` encoding is used for all requests.
