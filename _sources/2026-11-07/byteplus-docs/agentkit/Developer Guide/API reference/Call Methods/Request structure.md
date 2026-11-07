---
title: "Request structure"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Request_structure"
---

To call an OpenAPI interface, the caller must send a request to the specified service address with the required signature and API\-specific business information. If you want to call the **DeleteAgentKitRuntime** operation, use the OpenAPI request structure as follows:

```JSON
POST https://agentkit.cn-beijing.byteplusapi.com.cn?Action=DeleteRuntime&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye6hflyl1c598vs****"
}
```



* `POST` indicates the API request method.

* `https://agentkit.cn-beijing.byteplusapi.com.cn` is the service access address. To achieve low latency, we recommend that you select the [service access address](https://docs.byteplus.com/en/docs/agentkit/Service_address) (endpoint) based on the region where your resources are located.

* `Action=DeleteRuntime` specifies the API to be called.

* `"RuntimeId": "r-ye6hflyl1c598vs****"` is a parameter required by the DeleteAgentKitRuntime operation.


<span id=".6YCa5L-h5Y2P6K6u"></span>
### Communication protocol

Requests can be sent via HTTP or HTTPS. We recommend that you use HTTPS for higher security.

<span id=".6K-35rGC5pa55rOV"></span>
### Request methods

See the specific requirements of each API operation for request methods. Only POST requests are supported for AgentKit OpenAPI.

<span id=".6K-35rGC5Y-C5pWw"></span>
### Request parameters

An OpenAPI request consists of two types of parameters: common request parameters and API request parameters. Common request parameters are included in every API call. For more information, see Common parameters. API request parameters are specific to each API operation. For more information, see the description of the specific API.

<span id=".5a2X56ym57yW56CB"></span>
### Character encoding

Requests and responses are encoded using the UTF\-8 character set.
