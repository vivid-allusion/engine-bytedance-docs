---
title: "Request structure"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Request_structure"
---

When calling a OpenAPI interface, you must send a request to the specified service address and ensure that both the signature information and the business information required by the specific interface are provided.

The OpenAPI request structure is as follows:

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service Addresses

The OpenAPI addresses differ across regions. For details, please refer to [Service Addresses](https://docs.byteplus.com/en/docs/cp/Service_Addresses).

<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication Protocol

All interfaces use the more secure HTTPS protocol to send requests, providing a highly secure communication channel.

<span id=".6K-35rGC5pa55rOV"></span>
## Request Method

OpenAPI only allows **POST** requests.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using the POST method, the public parameters <code>Action</code> and <code>Version</code> must be specified in the <code>Query String</code>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

openAPI requests include two types of parameters:


* Common request parameters: Request parameters that must be included in every API request. For more details, please refer to the [Public parameters](https://docs.byteplus.com/en/docs/cp/Public_parameters) documentation.

* API request parameters: Request parameters specific to each API. For more details, see the documentation for each interface.


<span id=".5a2X56ym57yW56CB"></span>
## Character Encoding

Both the request and response results are encoded using the UTF\-8 character set.
