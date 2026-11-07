---
title: "Request Structure"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Request-structure"
---

When you call an API, a request is sent to the specified service endpoint. The request must be signed and contain the relevant business information so that the service can be successfully called. The following example shows the structure of an API request. The sample request is sent to call the DescribeCens action, and the request URL is not encoded. The request structure of BytePlus OpenAPI is organized as follows, using an unencoded URL sample request for DescribeVpcEndpointServices as an example:

```Plain Text
GET /?Action=DescribeTransitRouters&Version=2020-04-01&<Action_specific_request_parameters>
Host: transitrouter.cn-guangzhou.byteplusapi.com.cn HTTP/1.1
Region: cn-guangzhou
Service: transitrouter
```



* `GET` specifies the HTTP method of the request. The Transit Router (TR) API supports only the GET method.

* `Action=DescribeTransitRouters` specifies the API action you want to call. `Version=2020-04-01` specifies the version of the API.

* `HTTP` specifies the protocol of the request.

* `Host` specifies the service endpoint.

* `Region` and `Service` indicate the region and name of the service. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/transitrouter/Public-parameters).


<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service URL

The service endpoint for all BytePlus APIs is transitrouter. *{RegionID}* ..volcengineapi.com。

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Among them, <em>{RegionID}</em> represents the Region ID. Please refer to the <a href="https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-05#.5Yy65Z-f5LiO5Zyw5Z-f5YiX6KGo">Region list</a>.</div>


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Protocol

API requests can be communicated over `HTTP` or `HTTPS`. We recommend that you use `HTTPS` for higher security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request Method

For the request method, refer to the specific requirements of each API. The Transit Router (TR) API supports only Get requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you use the GET method, the <code>Action</code> and <code>Version</code> common parameters must be included in the <code>Query String</code>.</div>


* <div data-tips="true" data-tips-type="tip">All request parameters must be in the URL\-encoded format when the GET method is used.</div>



<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters

OpenAPI requests include two types of parameters: common request parameters and interface request parameters. Common request parameters are required for every API. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/transitrouter/Public-parameters). Interface request parameters are unique to each interface. For details, refer to the description of each interface.

<span id=".5a2X56ym57yW56CB"></span>
## Encoding

Requests and responses are encoded in UTF\-8.
