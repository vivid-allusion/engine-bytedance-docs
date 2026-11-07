---
title: "Request structure"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Request-structure"
---

To call an OpenAPI API, send a request to the specified service endpoint and include the required signature information and API\-specific business parameters. The structure of an OpenAPI request is organized as follows. An unencoded URL request for DescribeInstances is used as an example.


<Tabs>
<Tab zoneid="uqX9OY9VpA" title="Example 1: GET request">
<TabTitle>Example 1: GET request</TabTitle>

```Plain Text
GET /?Action=DescribeInstances&Version=2020-04-01&InstanceIds.1=i-3ti9101aju3vj0****** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```



</Tab>
<Tab zoneid="YnM92pdjYS" title="Example 2: POST (form) request">
<TabTitle>Example 2: POST (form) request</TabTitle>

```JSON
POST /?Action=DescribeInstances&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
--data-urlencode 'InstanceIds.1=i-3ti9101aju3vj0******' \
--data-urlencode 'MaxResults=1'
```



</Tab>
</Tabs>



* `GET` and `POST` indicate request methods. The OpenAPI of ECS supports the following request methods:

   * GET request.

   * POST request with parameters submitted via a form.

* `Action=DescribeInstances` specifies the operation to be called, and `Version=2020-04-01` specifies the API version.

* `Host` specifies the service endpoint. For more information, see [Service address](https://docs.byteplus.com/en/docs/ecs/Service_address).

* `Region` and `Service` indicate the region and name of the service. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/ecs/Public-parameters).

* `HTTP` specifies the protocol of the request.


<span id="rae6BTR2"></span>
### Communication protocols

Requests can be sent via either HTTP or HTTPS. We recommend that you use HTTPS for higher security.

<span id=".6K-35rGC5pa55rOV"></span>
### Request methods

See the specific requirements of each API operation for request methods.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">The Action and Version parameters in the common parameters must be included in the query string.</div>


* <div data-tips="true" data-tips-type="warning">For GET requests, all parameters must be URL\-encoded.</div>



<span id=".6K-35rGC5Y-C5pWw"></span>
### Request parameters

An OpenAPI request consists of two types of parameters: common parameters and API\-specific parameters. Common parameters are required for every API call. For more information, see Common parameters. API\-specific parameters are unique to each API. See the description of the specific API for details.

<span id=".5a2X56ym57yW56CB"></span>
### Character encoding

Requests and responses are encoded using the UTF\-8 character set.
