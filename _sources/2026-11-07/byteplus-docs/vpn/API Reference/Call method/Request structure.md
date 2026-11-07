---
title: "Request structure"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Request-structure-1"
---

When you call an open API of BytePlus Virtual Private Network (VPN), a request is sent to the specified service endpoint, and the request must contain BytePlus signature information and business information specific to the API. The structure of the request for calling an open API of the BytePlus VPN connection service is as follows: In the following example, the **CreateVpnGateway** action is called.

```Plain Text
GET /?Action=CreateVpnGateway&<API_request_parameters> HTTP/1.1 
Host: vpn.ap-southeast-1.byteplusapi.com
ServiceName: vpn
Region: ap-southeast-1
```



* `GET` means that open APIs for the BytePlus VPN connection service only support GET requests.

* `Action=CreateVpnGateway` specifies the API that you want to call.

* `HTTP` specifies the communication protocol of the request.

* `Host` specifies the endpoint of the BytePlus service.

* `ServiceName` specifies the name of the requested service.

* `Region` specifies the Region that a request is sent to. For more information, refer to [Public parameters](https://docs.byteplus.com/en/docs/vpn/Public-parameters).


&nbsp;

<span id="communication-protocol"></span>
## Communication protocol

Open APIs for the BytePlus VPN connection service support two communication protocols for requests, HTTP and HTTPS. We recommend that you use the more secure HTTPS to send an API request.

<span id="service-endpoint"></span>
## Service endpoint

The service address of BytePlus OpenAPI is: vpn. *{RegionID}* .byteplusapi.com.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please refer to <a href="https://docs.byteplus.com/en/docs/vpn/Regions#region-list">Region List</a> to get the <em>{RegionID}</em>.</div>


<span id="request-method"></span>
## Request method

Open APIs for the BytePlus VPN connection service only support GET requests. For more information on request methods, refer to the requirements of each API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="tip">When you use GET to call an API, place the common parameters <code>Action</code> and <code>Version</code> in <code>Query String</code> and complete URL encoding for all request parameters.</div>


<span id="request-parameters"></span>
## Request parameters

The request parameters of open APIs for the BytePlus VPN connection service are divided into: common request parameters and API request parameters. Common request parameters are required for each API. For more information, refer to [Public parameters](https://docs.byteplus.com/en/docs/vpn/Public-parameters). API request parameters are specific to each API. For details, refer to the description of each API.

<span id="character-encoding"></span>
## Character encoding

The UTF\-8 character set is used to encode call requests and response parameters.
