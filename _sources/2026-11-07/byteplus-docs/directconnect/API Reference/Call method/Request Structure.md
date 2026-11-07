---
title: "Request Structure"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Request-structure"
---

You call a BytePlus Direct Connect\-related OpenAPI API by sending a request with valid signature details and information required by the specific API to the specified service URL. The Request structure of BytePlus Direct Connect OpenAPI is organized as follows: In the following example, the **CreateDirectConnectGateway** action is called.

```SQL
GET /?Action=CreateDirectConnectGateway&<Interface request parameter> HTTP/1.1 
Host: directconnect.ap-southeast-1.byteplusapi.com HTTP/1.1
Region: ap-southeast-1
Region: cn-beijing
```



* `GET` indicates that the BytePlus Direct Connect OpenAPI only supports Get requests.

* `Action=CreateDirectConnectGateway` specifies the API to be called.

* `HTTP` indicates the protocol of the request.

* `Host` indicates the service endpoint.

* `ServiceName` specifies the name of the requested service.

* `Region` indicates the Region that a request is sent to. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/directconnect/Public-parameters).


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocol

BytePlus Direct Connect OpenAPI supports HTTP and HTTPS protocol requests. It is recommended to send API requests using the more secure HTTPS method.

<span id="V8fKZQmJ"></span>
## Service address

The general service URL of OpenAPI APIs is: open.volcengineapi.com.

<span id=".6K-35rGC5pa55rOV"></span>
## Request Method

The OpenAPI of BytePlus Direct Connect only supports GET requests. For more information about the request method of an API, refer to the specific requirements of the API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="tip">When you use GET to call an API, place the common parameters <code>Action</code> and <code>Version</code> in <code>Query String</code> and complete URL encoding for all request parameters.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters

The OpenAPI request of BytePlus Direct Connect includes two types of parameters: common request parameters and interface request parameters. Common request parameters are required for every API. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/directconnect/Public-parameters). Interface request parameters are specific to each API. See the description of individual interfaces for details.

<span id=".5a2X56ym57yW56CB"></span>
## Character Encoding

Both the request calls and the response results use the UTF\-8 character set for encoding.
