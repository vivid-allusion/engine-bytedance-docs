---
title: "Request Method"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Request-Method"
---

When you call an API, a request is sent to the specified service endpoint. The request must be signed and contain the relevant business information so that the service can be successfully called. The following example shows the structure of an API request. The sample request is sent to call the DescribeCens action, and the request URL is not encoded. The request structure of OpenAPI is organized as follows, using an unencoded URL request example of DescribeVpcEndpointServices:

```Plain Text
GET /?Action=DescribeLoadBalancers&Version=2020-04-01&<interface request parameter>
Host: clb.cn-guangzhou.byteplusapi.com HTTP/1.1
Region: cn-guangzhou
Service: clb
```



* `GET` indicates that the Network Load Balancer's OpenAPI supports only GET requests.

* `Action=DescribeLoadBanlancers` specifies the OpenAPI to be called, and `Version=2020-04-01` specifies the version of the OpenAPI.

* `HTTP` specifies the protocol of the request.

* `Host` specifies the service endpoint.

* `Region` and `Service` indicate the region and name of the service. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/clb/NLB-Common-Parameters).


<span id="服务地址"></span>
## URL

The general service endpoint of open BytePlus APIs is `clb.{RegionID}.byteplusapi.com`.

Please refer to [Region List](https://docs.byteplus.com/en/docs/clb/NLB-Regions-and-availability-zones) to get the {RegionID}.

<span id="通信协议"></span>
## Protocol

API requests can be communicated over `HTTP` or `HTTPS`. We recommend that you use `HTTPS` for higher security.

<span id="请求方法"></span>
## Request Method

For the request method, refer to the specific requirements of each API. The OpenAPIs of Network Load Balancer only support GET requests.


* When you use the GET method, the `Action` and `Version` common parameters must be included in the `Query String`.

* All request parameters must be in the URL\-encoded format when the GET method is used.


<span id="请求参数"></span>
## Request Parameters

OpenAPI requests include two types of parameters: common request parameters and interface request parameters. Common request parameters are required for every API. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/clb/NLB-Common-Parameters). Interface request parameters are unique to each interface. For details, refer to the description of each interface.

<span id="字符编码"></span>
## Encoding

Requests and responses are encoded in UTF\-8.
