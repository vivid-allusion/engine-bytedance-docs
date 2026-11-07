---
title: "Request structure"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Request_structure"
---

To call an OpenAPI operation of the BytePlus platform, send a request to the specified service endpoint with BytePlus platform signature and specific API service requirements. The OpenAPI request structure of the BytePlus platform is organized as follows. An unencoded URL request for **CreateMigrationJob** is used as an example:

```HTTP
GET /?Action=CreateMigrationJob&Version=2020-04-01&DestinationConfig.DestinationType=ECSInstance&DestinationConfig.Region=ap-southeast-1&MigrationJobName=VMtoECS&MigrationSourceId=s-iegs1y963vj0******&NetworkConfig.NetworkTransitionMode=PublicNetwork&SyncConfig.SyncType=File&SyncConfig.TriggerLastSync=true HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```



* `GET` specifies the request method. Server Migration Center (SMC) OpenAPI supports GET requests.

* `Action=CreateMigrationJob` specifies the API to be called, and `Version=2020-04-01` is the API version.

* `Host` specifies the BytePlus platform service endpoint.

* `Region` and `Service` indicate the region and name of the service. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/smc/Public_parameters).

* `HTTP` specifies the protocol of the request.


<span id=".5pyN5Yqh5Zyw5Z2A"></span>
### Service address

The general service endpoint for the BytePlus platform OpenAPIs is smc.byteplusapi.com.

<span id=".6YCa5L-h5Y2P6K6u"></span>
### Communication protocol

Requests can be sent via HTTP or HTTPS. We recommend that you use HTTPS for higher security.

<span id=".6K-35rGC5pa55rOV"></span>
### Request methods

See the specific requirements of each API operation for request methods. The SMC OpenAPI supports GET requests.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The Action and Version parameters in the common parameters must be included in the query string.</div>


* <div data-tips="true" data-tips-type="warning">For GET requests, all parameters must be URL\-encoded.</div>



<span id=".6K-35rGC5Y-C5pWw"></span>
### Request parameters

BytePlus platform OpenAPI requests include two types of parameters: common request parameters and API\-specific request parameters. Common request parameters are included in every API call. For more information, see Common parameters. API request parameters are specific to each API operation. For more information, see the description of the specific API.

<span id=".5a2X56ym57yW56CB"></span>
### Character encoding

Requests and responses are encoded using the UTF\-8 character set.
