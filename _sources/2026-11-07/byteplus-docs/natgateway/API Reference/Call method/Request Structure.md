---
title: "Request Structure"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Request-structure"
---

To call APIs, you must send requests to a specified service endpoint and meet BytePlus signature and API service requirements. The Request structure for BytePlus's OpenAPI is organized as follows, with **CreateNatGateway** as an example:

```Plain Text
GET /?Action=CreateNatGateway&<API request parameter> HTTP/1.1
Host: natgateway.ap-southeast-1.byteplusapi.com HTTP/1.1
Region: ap-southeast-1
Service: natgateway
```

* GET` means open APIs in support Get requests.

* `Action=CreateNatGateway` specifies the API that you want to call.

* `HTTP` indicates the protocol of the request.

* `Host` indicates the service endpoint.

* `Service` is the name of the service being requested.

* `Region` specifies the Region that a request is sent to. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/natgateway/Public-parameters).

## Protocol

Open APIs of a NAT gateway support two communication protocols for requests, HTTP and HTTPS. We recommend that you use the safer HTTPS to send an API request.

## Service URL

The common service endpoint of open APIs is open.volcengineapi.com.

## Request Method

For the request method, refer to the specific requirements of each API.

**Note**: When you use GET to call an API, place the common parameters `Action` and `Version` in `Query String`, and complete URL encoding for all request parameters.

## Request Parameters

OpenAPI requests include two types of parameters: common request parameters and interface request parameters. Common request parameters are required for every API. For more information, refer to [common parameters](https://docs.byteplus.com/en/docs/natgateway/Public-parameters). Interface request parameters are specific to each API. See the description of individual interfaces for details.

## Encoding

The UTF\-8 character set is used to encode call requests and response parameters.
