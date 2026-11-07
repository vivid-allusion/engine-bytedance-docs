---
title: "Request structure"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Request_structure"
---

To call BytePlus's OpenAPI interface, send requests to the specified service endpoint. This request must include BytePlus signature information and the relevant business details for the specific interface, or the call will fail. The request structure for BytePlus OpenAPI is organized as follows, using an unencoded URL example for calling **CreateDataMigrateTask**:

```Plain
POST /?Action=CreateDataMigrateTask&Version=2018-01-01 HTTP/1.1 
Host: open.byteplusapi.com
Region: cn-beijing
Service: dms
<API request parameters>
```



* `POST` indicates the request method; the DMS OpenAPI supports POST requests.

* `Action=CreateDataMigrateTask` specifies the API to be called, and `Version=2018-01-01` is the API version.

* `Host` specifies the BytePlus service access endpoint.

* `Region` and `Service` refer to the requested region and service; for details, see [Public Parameters](https://docs.byteplus.com/docs/dms/Common_Parameters).

* `HTTP` specifies the communication protocol for the request.


<span id="d32de9ee"></span>
## Service address

The available regions for DMS are listed in the table below.


|**Available region** |**Region ID** |**Service access address** |
|---|---|---|
|China (Beijing) |cn\-beijing |dms.cn\-beijing.byteplusapi.com.cn |
|China (Guangzhou) |cn\-guangzhou |dms.cn\-guangzhou.byteplusapi.com.cn |
|China (Shanghai) |cn\-shanghai |dms.cn\-shanghai.byteplusapi.com.cn |
|China (Hong Kong) |cn\-hongkong |dms.cn\-hongkong.byteplusapi.com |
|Asia Pacific (Johor) |ap\-southeast\-1 |dms.ap\-southeast\-1.byteplusapi.com |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |dms.ap\-southeast\-3.byteplusapi.com |


<span id="fda9963f"></span>
## Communication protocol

Supports HTTP and HTTPS protocols for request communication. HTTPS is recommended for enhanced security.

<span id="f7ece59a"></span>
## Request Method

For details on the request methods, refer to the specific requirements of each API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Action and Version parameters in public requests must be placed in the Query String.</div>


* <div data-tips="true" data-tips-type="tip">When using GET, all request parameters must be URL\-encoded.</div>



<span id="a65d7393"></span>
## Request Parameters

Each API request includes two types of parameters:


* Public request parameters: Common parameters required by every API endpoint. For more information on public parameters, see [Public Parameters](https://docs.byteplus.com/docs/dms/Common_Parameters).

* Interface request parameters: Parameters unique to each API endpoint. For details about the request parameters of each API, see the descriptions for each interface in [API Overview](https://docs.byteplus.com/docs/dms/API_Overview).


<span id="8307e3ad"></span>
## Character encoding

Requests and responses use the UTF\-8 character set for encoding.
