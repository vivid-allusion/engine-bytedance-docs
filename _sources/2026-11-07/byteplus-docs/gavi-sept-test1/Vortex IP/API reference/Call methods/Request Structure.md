---
title: "Request Structure"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Request_Structure"
---

To call APIs, you must send requests to a specified service endpoint and meet signature and API service requirements. The organization of the Request structure of BytePlus's OpenAPI is as follows, taking **CreateVortexIP** as an example:

```Plain Text
GET /?Action=CreateVortexIP&<interface request parameter> HTTP/1.1\nHost: open.volcengineapi.com\nRegion: ap-southeast-1\nService: fasttrack
```



* `GET` indicates that the OpenAPI in BytePlus supports GET requests.

* `Action=CreateVortexIP` specifies the OpenAPI to be called.

* `HTTP` indicates the protocol of the request.

* `Host` indicates the service endpoint.

* `Region` specifies the Region that a request is sent to. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/gavi-sept-test1/Common_Parameters).

* `Service` is the name of the service being requested.


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Protocol

Fasttrack's OpenAPI supports communication requests through both HTTP and HTTPS protocols. It is recommended to use the more secure HTTPS method to send API requests.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service URL

The service endpoint for all BytePlus APIs is open.volcengineapi.com.

<span id=".6K-35rGC5pa55rOV"></span>
## Request Method

Request methods are detailed according to the specific needs of each interface. BytePlus open APIs support Get requests.

<div data-tips="true" data-tips-type="tip">Note:When you use GET to call an API, place the common parameters <code>Action</code> and <code>Version</code> in <code>Query String</code> and complete URL encoding for all request parameters.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters

BytePlus OpenAPI requests include two types of parameters: common request parameters and interface request parameters. Among them, the common request parameters are required for every interface. For details, refer to [Common parameters](https://docs.byteplus.com/en/docs/FT/Common_Parameters). Interface request parameters are unique to each interface. For details, refer to the description of each interface.

<span id=".5a2X56ym57yW56CB"></span>
## Character Encoding

Request and Response results are encoded using the UTF\-8 character set.
