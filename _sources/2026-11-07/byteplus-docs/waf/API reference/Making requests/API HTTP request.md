---
title: "API HTTP request"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/API_HTTP_request"
---

Calling OpenAPI via the console involves sending a request to a designated service address, which must include the required signature information and specific details of the interface. The request for OpenAPI primarily consists of the request URL, request Header, and request Body.

<span id="0e026845"></span>
## Background information

<span id="97e6f505"></span>
### **Request method**

For detailed request methods, please refer to the specific requirements of each interface, and choose to initiate the request using `GET` or `POST`.

<span id="e6d36d6b"></span>
### **Communication protocol**

Supports requests over both `HTTP` and `HTTPS` protocols. It is recommended to use the more secure `HTTPS` for sending API requests.

<span id="9de865db"></span>
### **Character encoding**

Requests and responses are encoded in the UTF\-8 character set.

<span id="8d79aaa3"></span>
### Region information

When calling the API, the `Region` information needs to be consistent with the ID of the region where the instance is located. Our service uses the following regions.


|Region name |Region ID |
|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |
|China (Hong Kong) |cn\-hongkong |
|Edge |byteplus\-global |


<span id="c9095e0f"></span>
## Request composition

<span id="5609a972"></span>
### Request URL

You can call the Web Application Firewall's API by sending an HTTP or HTTPS request. The URL for initiating an API request is composed of multiple parameters, with a fixed request structure. Requests and responses are both encoded in the UTF\-8 character set.

Example of HTTPS request URL format is as follows:

```JSON
POST https://{Host}?Action={Action name}&Version={Registered version}
```



* `POST` represents a request method supported by the OpenAPI for the console.

* `Host` specifies the service domain (Endpoint), the current access domain is `waf.byteplusapi.com`.

* `Action={Action name}` specifies the API to call.

* `Version={Registered version}` specifies the version of the API.


<span id="258aed0c"></span>
### Request Header

The request header (Header) needs to specify the `Content-Type` and the public parameters, such as request authentication information to identify the user and the interface signature. If not necessary, these parameters will not be explained separately in each individual interface documentation, but these parameters need to be carried with each request to initiate the request properly.

Among these, the `Content-Type` specifies the structured format of the request message body. The Content\-Type for Web Application Firewall is fixed to `application/json`. If the `Content-Type` value is not specified when requesting, the default format is `application/json`. For a detailed list and description of parameters, please refer to [Region information](https://docs.byteplus.com/docs/waf/API_HTTP_request#8d79aaa3).

The example format for the request Header is as follows:

```JSON
X-Date: 20230711T035055Z
Authorization: HMAC-SHA256 Credential=AKLTNGU0OGEyMT***/20230711/byteplus-global/waf/request, SignedHeaders=content-type;x-content-sha256;x-date, Signature=da4fac562d00f41ad8***
```



* `X-Date` tag is used for time, in UTC, accurate to the second. The format is `YYYYMMDD'T'HHMMSS'Z'`, for example: `20230711T035055Z`.

* `Authorization` refers to the authorization information. The format is `HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`

   * AccessKeyId (String): The Access Key ID of the account initiating the request. For example: `AKLTNGU0OGEyMT***`.

   * ShortDate (String): The short date of the request, in UTC, accurate to the day. The format is `YYYYMMDD`, for example: `20230711`.

   * Region (String): The region requested, for example: `byteplus-global`.

   * Service (String): The service that is being requested. The service name for Web Application Firewall is `waf`.

   * SignedHeaders (String): Headers involved in signing, separated by semicolons. For example `content-type;x-content-sha256;x-date`.

   * Signature (String): The calculated signature. In the example it is `da4fac562d00f41ad8***`.


<span id="68e2c961"></span>
### Request Body

Request Body, that is, the request message body, mainly transmits business\-related Request parameters. If the parameters in the request message body support Chinese, then the Chinese characters must be encoded in UTF\-8.

The request message body content differs for each interface, and not all interfaces require a request message body (meaning the body could be empty). When calling an interface, please refer to the specific API documentation to construct the request message body.

For example, the request Body format for obtaining attack source information is as follows:

```JSON
{
  "Host": "example.volcwaf001.com",
  "StartTime": 1695767322,
  "EndTime": 1697185065,
  "AnalysisKey": "Country",
  "Plugins": [
    "web_policy"
  ]
}
```


<span id="5b88544b"></span>
## Initiating a request

You can use [curl](https://curl.haxx.se/), [Postman](https://www.getpostman.com/) or directly write code to send requests to call the API.

For example, the sample request for getting protection overview information is as follows:

```JSON
POST https://waf.byteplusapi.com/?Action=QueryProtectionOverviewLb&Version=2023-12-25
X-Date: 20230711T035055Z
Authorization: HMAC-SHA256 Credential=AKLTNGU0OGEyMT***/20230711/byteplus-global/waf/request, SignedHeaders=content-type;x-content-sha256;x-date, Signature=da4fac562d00f41ad8***

{
    "Host": "example.volcwaf001.com",
    "StartTime": 1695767322,
    "EndTime": 1697185065,
    "AnalysisKey": "Country",
    "Plugins": [
        "web_policy"
    ]
}
```
