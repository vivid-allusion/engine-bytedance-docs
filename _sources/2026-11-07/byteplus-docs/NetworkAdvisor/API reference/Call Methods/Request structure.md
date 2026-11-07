---
title: "Request structure"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Request-structure"
---

To call the BytePlus OpenAPI, send a request to the specified service endpoint while fulfilling the BytePlus signature and the specific API service parameters. The request structure for BytePlus  OpenAPI is organized as follows, using CreateDiagnosisInstance as an example:

```Plain Text
GET /?Action=CreateDiagnosisInstance&<Interface request parameters> HTTP/1.1
Host: na.byteplusapi.com
```



* `GET` indicates that BytePlus OpenAPIs support Get requests.

* `Action=CreateDiagnosisInstance` specifies the OpenAPI to be called.

* `HTTP` specifies the communication protocol for the request.

* `Host` specifies the BytePlus service endpoint.


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocols

The OpenAPIs of the Network Advisor (NA) support both HTTP and HTTPS protocols. It is recommended to use the more secure HTTPS method for sending API requests.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service endpoint

BytePlus OpenAPI common service endpoint is: na.byteplusapi.com.

<span id=".6K-35rGC5pa55rOV"></span>
## Request method

See the specific requirements of each API for request methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">To call the API using GET, include common parameters of <code>Action</code> and <code>Version</code> in the <code>Query String</code>, and encode all request parameters by URL.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

BytePlus OpenAPI requests include two types of parameters: common request parameters and API request parameters. Common request parameters, included in every API call. For details, see [Common parameters](https://docs.byteplus.com/en/docs/NetworkAdvisor/Common-parameters). API request parameters are unique to each API. See the specific API descriptions for details.

<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

Requests and responses use UTF\-8 character encoding.
