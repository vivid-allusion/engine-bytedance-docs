---
title: "Request structure"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Response_structure"
---

When you call the console OpenAPI interface, it is done by sending a request to the specified service endpoint, and it requires an appropriate signature along with the specific interface's business information. An OpenAPI request needs to include the service endpoint, request method, request parameters, and other information.

Taking the creating space API as an example, a sample request with an unencoded URL is as follows:

```json
POST https://{Host}/?Action={Action name}&Version={Registered version}
ServiceName: {server name}
AccessKey: xxx
SecretKey: xxx
Region: xxx
Data: {<request_parameters>}
```



* `POST` is the request method supported by the console OpenAPI. The supported Content\-Type is `application/json`.

* `Host` specifies the service access endpoint. The service endpoints for the server\-side (apmplus_server) and client\-side (apmplus_openapi) vary across different regions. For details, see [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address).

* `Action={Action name}` specifies the API to be called.

* `Version={Registered version}` specifies the version of the API to be called. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

* `Region` is the requested region. For details, see [Service regions](https://docs.byteplus.com/en/docs/apmplus/server-launching_region).

* `ServiceName` is the requested service name. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

* `AccessKey` and `SecretKey` are used to verify signature information. For details, see [Signature mechanism](https://docs.byteplus.com/en/docs/apmplus/Signature_methods).

* `Data` specifies the request parameters of the API.


<span id=".6YCa5L-h5Y2P6K6u"></span>
### **Communication protocols**

Both `HTTP` and `HTTPS` are supported for sending requests. We recommend using `HTTPS`, the more secure method for sending API requests.

<span id=".6K-35rGC5pa55rOV"></span>
### **Request methods**

The request method depends on the specific requirements of each API. Select either GET or POST to initiate the request.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using the POST method, the public parameters <code>Action</code> and <code>Version</code> must be placed in the <code>Query String</code>.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
### **Request parameters**

When initiating an OpenAPI request, the request body may contain two types of parameters: public request parameters and API\-specific request parameters.


* Public request parameters are required for every API. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

* API\-specific request parameters are unique to each API. For details, see the description of each API.


<span id=".5a2X56ym57yW56CB"></span>
### **Character encoding**

Both requests and responses are encoded using the UTF\-8 character set.
