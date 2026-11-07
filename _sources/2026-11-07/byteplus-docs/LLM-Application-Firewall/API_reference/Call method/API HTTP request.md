---
title: "API HTTP request"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/API_HTTP_request"
---

Invoking Console OpenAPI interfaces is accomplished by sending requests to the specified service address and ensuring that both the signature information and the required business information for the specific interface are provided. An OpenAPI request primarily includes the request URL, request header, and request body.

<span id="0e026845"></span>
## Background information

<span id="97e6f505"></span>
### **Request methods**

For details on the request method, refer to the specific requirements of each interface. Then, use the `GET` or `POST` method to make the request.

<span id="e6d36d6b"></span>
### **Communication protocols**

This service supports requests via `HTTPS`.

<span id="9de865db"></span>
### **Character encoding**

Requests and responses are encoded using the UTF\-8 character set.

<span id="8d79aaa3"></span>
### Regional information

When calling the API, the `Region` information must be consistent with the ID of the region where the instance is located. The following table shows the corresponding region IDs.


|**Region** |**ID** |
|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |
|Hong Kong |cn\-hongkong |


<span id="c9095e0f"></span>
## Request composition

<span id="5609a972"></span>
### Request URL

You can invoke the API of the LLM Application Firewall by sending an HTTPS request. The URL for initiating an API request consists of multiple parameters and follows a fixed request structure.

The following is an example of the HTTPS request URL format:

```JSON
POST https://{Host}?Action={Action name}&Version={Registered version}
```



* `POST` is a request method supported by the console's OpenAPI.

* `Host` specifies the service access address (Endpoint). The current access address is `{region}.sdk.access-bp.llm-shield.omni-shield.ai`.

* `Action={Action name}` specifies the API to be called.

* `Version={Registered version}` specifies the version of the API to be called.


<span id="258aed0c"></span>
### Request headers

The request header must specify the `Content-Type` and common parameters such as authentication information, which are used for user identification and API signature. Unless necessary, individual API documentation will no longer describe these parameters; however, each request must include them to succeed.

The `Content-Type` specifies the structured format of the request body, and the `Content-Type` for the LLM Application Firewall is always `application/json`. If the Content\-Type header is omitted, it defaults to application/json. See the detailed list of parameters and their descriptions in [Common request parameters](/5qm0d9do/1ifshm94).

Sample request header format is as follows:

```JSON
X-Date: 20250904T124957Z
Authorization: HMAC-SHA256 Credential=AKLTYjVlMGIxZWVlOTlkNDUwNmJhMjRkNzlkNz********/20250904/cn-hongkong/llmshield/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=3d51784baf1a1c600b9fcaf14bc0f1340f3db98b02fb3be8615c9c65********
```



* `X-Date` refers to the time used for signing, which uses UTC time and is accurate to the second. The format is `YYYYMMDD'T'HHMMSS'Z'`, for example: `20230711T035055Z`.

* `Authorization` contains the signature and credential information. The format is `HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`

   * AccessKeyId (String): The Access Key ID of the account initiating the request. For example: `AKLTNGU0OGEyMT***`.

   * ShortDate (String): The short date of the request in UTC, accurate to the day. The format is `YYYYMMDD`, for example: `20230711`.

   * Region (String): The requested region, for example: `cn-beijing`.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>Region</code> information must be consistent with the ID of the region where the instance is located.       </div>
      

   * `Service` (String): Specifies the service being requested. The service name of the LLM Application Firewall is .

   * `SignedHeaders` (String): Specifies the headers included in the signature, separated by semicolons. For example, .

   * `Signature` (String): The computed signature string. In the example, it is .


<span id="68e2c961"></span>
### Request body

The request body contains the API\-specific parameters for the operation. If any parameters in the request body contain Chinese characters, they must be UTF\-8 encoded.

The content of the request body is specific to each API, and some APIs do not require a request body. When calling an API, refer to the specific API documentation to construct the request body.

For example, the following is the request body format for a prompt compliance check:

```JSON
{
    "Message": {
        "Role": "user",
        "Content": "What's the weather today?",
        "ContentType": 1
    },
    "MsgID": "",
    "UseStream": 0,
    "Scene": "app-d2ql7d4jslssiv08****",
    "History": [
        {
            "Role": "system",
            "Content": "You are an intelligent question-answering assistant. Your task is to generate a response that meets the requirements based on the user's question.",
            "ContentType": 1
        },
        {
            "Role": "assistant",
            "Content": "It's very sunny today.",
            "ContentType": 1
        }
    ]
}
```


<span id="5b88544b"></span>
## Initiate a request

You can call the API using tools like [curl](https://curl.haxx.se/) and [Postman](https://www.getpostman.com/), or by writing a custom script.

For example, here is a sample request to determine whether LLM prompts are compliant:

```JSON
POST /v2/moderate?Action=Moderate&Version=2025-08-31 HTTP/1.1
Host: cn-hongkong.sdk.access-bp.llm-shield.omni-shield.ai
Authorization: HMAC-SHA256 Credential=AKLTYjVlMGIxZWVlOTlkNDUwNmJhMjRkNzlkNz********/20250904/cn-hongkong/llmshield/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=3d51784baf1a1c600b9fcaf14bc0f1340f3db98b02fb3be8615c9c65********
Content-Type: application/json
X-Content-Sha256: 904037c4d0cd16e0918291d33c3acfc9b6f871c0459644b571bdbc5********
X-Date: 20250904T124957Z
  
{
    "Message": {
        "Role": "user",
        "Content": "What's the weather today?",
        "ContentType": 1
    },
    "MsgID": "",
    "UseStream": 0,
    "Scene": "app-d2ql7d4jslssiv08****",
    "History": [
        {
            "Role": "system",
            "Content": "You are an intelligent question-answering assistant. Your task is to generate a response that meets the requirements based on the user's question.",
            "ContentType": 1
        },
        {
            "Role": "assistant",
            "Content": "It's very sunny today.",
            "ContentType": 1
        }
    ]
}
```
