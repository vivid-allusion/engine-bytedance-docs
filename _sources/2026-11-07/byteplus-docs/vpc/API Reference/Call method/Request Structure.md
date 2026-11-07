---
title: "Request Structure"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Request-structure"
---

To call BytePlus APIs, you must send requests to a specified service endpoint and meet BytePlus signature and API service requirements. The request structure of BytePlus OpenAPI is organized as follows, using **CreateVpc** as an example:

```Plain Text
GET /?Action=CreateVpc&<interface request parameter> HTTP/1.1
Host: vpc.ap-southeast-1.byteplusapi.com
Service: vpc
Region:ap-southeast-1
```



* `GET` indicates that the OpenAPI in VPC only supports GET requests.

* `Action=CreateVpc` specifies the API to be called.

* `HTTP` indicates the protocol of the request.

* `Host` indicates the service endpoint.

* `Service` is the name of the service being requested.

* `Region` indicates the Region that a request is sent to. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/vpc/Public-parameters).


<span id=".6YCa5L-h5Y2P6K6u"></span>
## Protocol

VPC API requests can be communicated using both HTTP and HTTPS protocols. We recommend using HTTPS for higher security.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service URL

The general service endpoint of open  APIs is vpc.{RegionID}.byteplusapi.com. 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note：</div>


<div data-tips="true" data-tips-type="default">Please refer to <a href="https://docs.byteplus.com/en/docs/vpc/Regions-and-Availability-Zones">Region List</a> to get the {RegionID}.</div>


<span id=".6K-35rGC5pa55rOV"></span>
## Request Method

For the request method, refer to the specific requirements of each API. OpenAPI in VPC only supports GET requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note:</div>


<div data-tips="true" data-tips-type="tip">When you use GET to call an API, place the common parameters <code>Action</code> and <code>Version</code> in <code>Query String</code> and complete URL encoding for all request parameters.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters

BytePlus's OpenAPI requests include two types of parameters: common request parameters and interface request parameters. Common request parameters are required for every API. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/vpc/Public-parameters). Interface request parameters are specific to each API. See the description of individual interfaces for details.

<span id=".5a2X56ym57yW56CB"></span>
## Encoding

The UTF\-8 character set is used to encode call requests and response parameters.
