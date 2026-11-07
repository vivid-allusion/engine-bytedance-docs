---
title: "Request structure"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Request_structure"
---

When calling the BytePlus OpenAPI interface, it is done by sending a request to the specified service address, and it needs to satisfy the BytePlus signature information and the business information of the specific interface. 

The BytePlus OpenAPI request structure is organized as follows:

<span id="服务地址"></span>
## Service address 

The service address of Function Service （FaaS） BytePlus OpenAPI is `vefaas.<Region_ID>.byteplusapi.com`.

<span id="通信协议"></span>
## Communication protocol 

All interfaces use a more secure HTTPS method to send requests, providing a highly secure communication channel.

<span id="请求方法"></span>
## Request method 

OpenAPI allows only **POST** requests.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using the POST method, the <code>Action</code> and <code>Version</code> in the public parameter must be placed in the <code>Query String</code>. For example: <code>? Action=CreaeFunctiont & Version = 2024-06-06</code>.</div>


<span id="请求参数"></span>
## Request parameters 

BytePlus OpenAPI requests contain two types of parameters:


* Public request parameters: The request parameters that each interface needs to include. For detailed information, refer to [Public parameters](https://docs.byteplus.com/en/docs/faas/Public_parameter).

* Interface request parameters: Request parameters specific to each interface. For detailed information, refer to the documents of each individual interface.


<span id="字符编码"></span>
## Character encoding 

Request and response results are encoded using the UTF\-8 character set.
