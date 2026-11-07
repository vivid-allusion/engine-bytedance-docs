---
title: "Request structure"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Request-structure"
---

To call BytePlus OpenAPIs, you need to send requests to a specified server address and meet the signature and API service requirements of BytePlus. Below, we use a DescribeLoadBalancers request without URL encoding as an example to show the structure of OpenAPI requests.

```Plain Text
GET /?Action=DescribeLoadBalancers&Version=2020-04-01&<API request parameter>
Host: clb.ap-southeast-1.byteplusapi.com HTTP/1.1
Region: ap-southeast-1
Service: clb
```



* `GET` indicates that the OpenAPIs of CLB only support GET requests.

* `Action=DescribeLoadBalancers` specifies the API to call. `Version=2020-04-01` specifies the version of the API.

* `HTTP` specifies the communication protocol of the request.

* `Host` specifies the BytePlus service access address (endpoint).

* `Region` and `Service` indicate the region and service name of the request. For more information, refer to [Public parameters](https://docs.byteplus.com/en/docs/clb/Public-parameters).


<span id="url"></span>
## URL

The general service endpoint of open BytePlus APIs is `clb.{RegionID}.byteplusapi.com`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please refer to <a href="https://docs.byteplus.com/en/docs/clb/Product-Overview-08">Region List</a> to get the {RegionID}.</div>


<span id="communication-protocols"></span>
## Communication protocols

The `HTTP` and `HTTPS` protocols are supported. `HTTPS` is more secure, so we recommend it for sending API requests.

<span id="request-methods"></span>
## Request methods

For more information, refer to the specific requirements of each API. The OpenAPIs of CLB only support GET requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">When you use the GET method, include the public parameters <code>Action</code> and <code>Version</code> in <code>Query String</code>.</div>


* <div data-tips="true" data-tips-type="tip">When you use the GET method, all request parameters must undergo URL encoding.</div>



<span id="request-parameters"></span>
## Request parameters

BytePlus OpenAPI requests include two types of parameters: Public request parameters and API request parameters. Public request parameters are required for every API. For more information, refer to [Public parameters](https://docs.byteplus.com/en/docs/clb/Public-parameters). API request parameters vary with the API. For more information, refer to the description of each API.

<span id="character-encoding"></span>
## Character encoding

Requests and responses are encoded using UTF\-8 character sets.
