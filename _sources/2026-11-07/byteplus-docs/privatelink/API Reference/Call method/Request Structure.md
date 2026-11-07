---
title: "Request Structure"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Request-structure"
---

When you call an API, a request is sent to the specified service endpoint. The request must be signed and contain the relevant business information so that the service can be successfully called. The following example shows the structure of an API request. The sample request is sent to call the DescribeCens action, and the request URL is not encoded. The request structure of OpenAPI is organized as follows, using an unencoded URL request example of DescribeVpcEndpointServices:

```Plain Text
GET /?Action=DescribeVpcEndpointServices&Version=2020-04-01&<interface request parameter>
Host: privatelink.cn-beijing.byteplusapi.com.cn HTTP/1.1
Region: cn-beijing
Service: privatelink
```



* `GET` indicates that the OpenAPI for PrivateLink only supports GET requests.

* `Action=DescribeLoadBalancers` specifies the OpenAPI to be called, and `Version=2020-04-01` specifies the version of the OpenAPI.

* `HTTP` specifies the protocol of the request.

* `Host` specifies the service endpoint.

* `Region` and `Service` indicate the region and name of the service. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/clb/Public-parameters).


<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service URL

The common service endpoint for BytePlus OpenAPIs is: privatelink. *{RegionID}* .volcengineapi.com.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Among them, <em>{RegionID}</em> represents the region ID. Please refer to <a href="https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones">region list</a>.</div>


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Protocol

API requests can be communicated over `HTTP` or `HTTPS`. We recommend that you use `HTTPS` for higher security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request Method

For the request method, refer to the specific requirements of each API. PrivateLink's OpenAPI only supports GET requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you use the GET method, the <code>Action</code> and <code>Version</code> common parameters must be included in the <code>query string</code>.</div>


* <div data-tips="true" data-tips-type="tip">All request parameters must be in the URL\-encoded format when the GET method is used.</div>



<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters

OpenAPI requests include two types of parameters: common request parameters and interface request parameters. Common request parameters are required for every API. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/clb/Public-parameters). Interface request parameters are unique to each interface. For details, refer to the description of each interface.

<span id=".5a2X56ym57yW56CB"></span>
## Encoding

Requests and responses are encoded in UTF\-8.
