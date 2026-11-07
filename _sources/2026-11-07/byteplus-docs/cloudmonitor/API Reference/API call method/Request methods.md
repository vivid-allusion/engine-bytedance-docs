---
title: "Request methods"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Request-method"
---

To call Volcengine OpenAPI, you need to send requests to the designated service endpoint, and include the required BytePlus signature information as well as the business\-specific parameters for the particular API. This topic describes the basic structure and communication methods of OpenAPI requests.

```Bash
POST https://{Host}?Action={Action name}&Version={Registered version}
ServiceName: {Monitor server name}
AccessKey: xxx
SecretKey: xxx
Region: xxx
Data: {<The request parameters>}
```


Parameter description:


* `POST`: The Cloud Monitor API only supports POST requests.

* `Host`: Service endpoint. For details, see [Service addresses](https://docs.byteplus.com/docs/cloudmonitor/Service_address).

* `Action={Action name}`: The name of the API being called.

* `Version={Registered version}`: The version of the API being called. For details, see [Public parameters](https://docs.byteplus.com/docs/cloudmonitor/Common-parameters).

* `Region` and `ServiceName`: The requested region and service name. For details, see [Public parameters](https://docs.byteplus.com/docs/cloudmonitor/Common-parameters).

* `AccessKey` and `SecretKey`: Credentials used to verify the signature information. For details, see [Signature mechanism](https://docs.byteplus.com/docs/cloudmonitor/Signature-method).

* `Data`: The request parameters.


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocols

Requests can be sent using either `HTTP` or `HTTPS`. We recommend using the more secure `HTTPS` protocol to send OpenAPI requests.

<span id=".6K-35rGC5pa55rOV"></span>
## Request methods

For request method details, see the specific requirements of each API. Cloud Monitor OpenAPI only supports POST requests.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions

An OpenAPI request contains the following two types of parameters:


* **Public request parameters**: Parameters that must be included in every API call to the service. For details, see [Public parameters](https://docs.byteplus.com/docs/cloudmonitor/Common-parameters).

* **API\-specific request parameters**: Parameters specific to different APIs. For details, see the description of each API.


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

Requests and responses are encoded using the UTF\-8 character set.

&nbsp;
