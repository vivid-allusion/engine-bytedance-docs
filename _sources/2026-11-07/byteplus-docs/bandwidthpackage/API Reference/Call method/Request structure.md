---
title: "Request structure"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Request-structure"
---

To call APIs, you must send requests to a specified service endpoint and meet signature and API service requirements. The request structure of BytePlus's OpenAPI is organized as follows, taking **CreateBandwidthPackage** as an example:

```Plain Text
GET /?Action=CreateBandwidthPackage&<interface request parameter> HTTP/1.1
Host:vpc.ap-southeast-1.byteplusapi.com HTTP/1.1
Region: ap-southeast-1
Service: vpc
```



* `GET` indicates that the OpenAPI in BytePlus supports GET requests.

* `Action=CreateBandwidthPackage` specifies the OpenAPI to be called.

* `HTTP` indicates the protocol of the request.

* `Host` indicates the service endpoint.

* `Region` specifies the region that a request is sent to. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-parameters).

* `Service` is the name of the service being requested.


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Protocol

Bandwidth Package API requests can be sent by using HTTP or HTTPS. We recommend using HTTPS, as this method is more secure.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service URL

The common endpoint for accessing APIs is vpc. *{RegionID}.* byteplusapi.com.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

For the request method, see the specific requirements of each API. System open APIs support Get requests.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">When you use GET to call an API, place the common parameters <code>Action</code> and <code>Version</code> in <code>Query String</code> and complete URL encoding for all request parameters.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

OpenAPI requests include two types of parameters: common request parameters and API request parameters. Among them, the common request parameters are required for every API. For details, see [common parameters](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-parameters). API request parameters are specific to each API. For details, see the description of each API.

<span id=".5a2X56ym57yW56CB"></span>
## Encoding

Requests and responses are encoded in UTF\-8.
