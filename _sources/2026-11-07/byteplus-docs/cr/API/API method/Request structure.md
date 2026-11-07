---
title: "Request structure"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/request-structure"
---

When you call a BytePlus API, a request is sent to the specified service endpoint. The request must be signed and contain the relevant business information so that the service can be successfully called. This topic describes the request structure of BytePlus OpenAPI.

<span id="服务地址"></span>
#### Endpoint

The service endpoint for all BytePlus APIs is `open.byteplusapi.com`.

<span id="通信协议"></span>
#### Protocol

All APIs communicate through HTTPS, which ensures highly secure communication channels.

<span id="请求方法"></span>
#### Request method

For more information on the request method, refer to the specific requirements of each API. BytePlus APIs support only POST requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The POST request allows the public information to be placed in the header.</div>


<span id="请求参数"></span>
#### Request parameters

Request parameters for BytePlus APIs are classified into common request parameters and action request parameters. All API requests contain common request parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/cr/common-parameters). Action\-specific request parameters vary depending on the action that you call. For more information, refer to the topic for the API action.

<span id="字符编码"></span>
#### Encoding

Requests and responses are encoded using the UTF\-8 character set.
