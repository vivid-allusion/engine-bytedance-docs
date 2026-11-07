---
title: "Request structure"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Request-structure"
---

To call BytePlus APIs, you must send requests to a specified service endpoint and meet BytePlus signature and API service requirements. The request structure of OpenAPI is organized as follows, using **CreateScalingGroup** as an example:

```Plain
GET /?Action=CreateScalingGroup&ScalingGroupName=scaling-group-test&<interface request parameter> HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: cn-beijing
Service: auto_scaling
```



* `GET` indicates that OpenAPI in BytePlus only supports Get requests.

* `Action=CreateScalingGroup` specifies the API to call, and `ScalingGroupName=scaling-group-test` is an argument required by the CreateScalingGroup interface.

* `Host` specifies the service access address. To achieve low latency, it is recommended that you select the corresponding [service access address](https://docs.byteplus.com/en/docs/as/Service-URL) (Endpoint) based on the Region of the resource.

* `Region` and `Service` indicate the region and name of the service. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/as/Public-parameters).

* `HTTP` specifies the protocol of the request.


<span id=".6YCa5L-h5Y2P6K6u"></span>
### Communication protocols

Requests can be sent via either HTTP or HTTPS. We recommend that you use HTTPS for higher security.

<span id=".6K-35rGC5pa55rOV"></span>
### Request methods

See the specific requirements of each API operation for request methods. The OpenAPI of Auto Scaling (AS) supports only the GET requests.

**Note that**:


* The Action and Version parameters in the common parameters must be included in the query string.

* For GET requests, all parameters must be URL\-encoded.


<span id=".6K-35rGC5Y-C5pWw"></span>
### Request parameters

An OpenAPI request consists of two types of parameters: common parameters and interface request parameters. Common request parameters are included in every API call. For more information, see Common parameters. API request parameters are unique to each API operation. For more information, see the specific API operation description.

<span id=".5a2X56ym57yW56CB"></span>
### Character encoding

Requests and responses are encoded using the UTF\-8 character set.
