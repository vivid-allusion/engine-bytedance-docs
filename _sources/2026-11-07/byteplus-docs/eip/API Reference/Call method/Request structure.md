---
title: "Request structure"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Request-structure"
---

To call BytePlus OpenAPIs, send requests to a specified service endpoint with BytePlus signature and specific API service requirements. The request structure of BytePlus OpenAPI is as follows, taking **AllocateEipAddress** as an example:

```Plain Text
GET /?Action=AllocateEipAddress&<Interface request parameters>
Host: vpc.ap-southeast-1.byteplusapi.com HTTP/1.1
Region: ap-southeast-1
Service: vpc
```



* `GET` indicates that BytePlus OpenAPIs support Get requests.

* `Action=AllocateEipAddress` specifies the OpenAPI that you want to call.

* `HTTP` specifies the protocol of the request.

* `Host` specifies the BytePlus service endpoint.

* `Region` is the region of the request. See [Common parameters](https://docs.byteplus.com/en/docs/eip/Public-parameters) for details.

* `Service` is the name of the requested service.


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocols

OpenAPIs of the elastic IP address (EIP) support both HTTP and HTTPS protocols. We recommend using HTTPS for secure API requests.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service endpoint

The common service endpoint for BytePlus OpenAPIs is vpc. *{RegionID}.* byteplusapi.com.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Among them, <em>{RegionID}</em> represents the Region ID. See <a href="https://docs.byteplus.com/en/docs/eip/Regions">Region list</a>.</div>


<span id=".6K-35rGC5pa55rOV"></span>
## Request method

See the specific requirements of each API for request methods. BytePlus OpenAPIs only support Get requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="tip">To call the API using GET, include common parameters of <code>Action</code> and <code>Version</code> in the <code>Query String</code>, and encode all request parameters by URL.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

BytePlus OpenAPI requests include two types of parameters: common request parameters and API request parameters. Among them, each API must contain common request parameters. See [Common parameters](https://docs.byteplus.com/en/docs/eip/Public-parameters) for details. API request parameters are unique to each API. See the specific API descriptions for details.

<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

Requests and responses use UTF\-8 character encoding.
