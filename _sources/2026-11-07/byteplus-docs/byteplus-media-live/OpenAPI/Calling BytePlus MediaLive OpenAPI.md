---
title: "Calling BytePlus MediaLive OpenAPI"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-calling-byteplus-medialive-openapi"
---

This article introduces basic information about calling BytePlus MediaLive OpenAPI.

<span id="API request"></span>
## API request

A BytePlus MediaLive OpenAPI request consists of the following parts:

<span id="Service address"></span>
### Service address

URI: open.byteplusapi.com

<span id="Protocol"></span>
### Protocol

BytePlus MediaLive OpenAPI supports both HTTP and HTTPS protocols. We recommend that you use HTTPS to ensure API request security.

<span id="Character encoding"></span>
### Character encoding

API requests and responses are encoded with **UTF\-8**.

<span id="Request method"></span>
### Request method

Most of the BytePlus MediaLive OpenAPI services support **GET** and **POST** methods.


* **GET**: Sends requests to the server to return specified resources. Public data can be added to headers and query string parameters.

* **POST**: Sends requests to the server to add resources or perform special operations. Public data can be added to headers only.


<span id="Request URI"></span>
### Request URI

Format: `{URI-scheme}://{domain}/?{query-string}`.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/258f59a-Request_URI.png) </span>


|**Component** |**Description** |
|---|---|
|URI scheme |Transfer protocols. Supports both **HTTP** and **HTTPS**. |
|Domain |Domain name. The domain name of BytePlus MediaLive OpenAPI is `open.byteplusapi.com`. |
|Query string |Includes common request parameters and operation\-specific parameters. For operation\-specific parameters and a partial list of common request parameters, see the detailed description of each API operation. For a complete list of common request parameters, see [Common request parameters](/docs/byteplus\-media\-live/docs\-calling\-byteplus\-medialive\-openapi#Common request parameters). |


<span id="Common request parameters"></span>
## Common request parameters


|**Name** |**Type** |**Required** |**Location** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |Header |Endpoint. Set the value to `open.byteplusapi.com`. |
|Content\-Type |String |Yes |Header |A Multipurpose Internet Mail Extensions (MIME) resource type. If there are no specific requirements for individual operations, set the value to `application/json; charset=utf-8`. |
|X\-Date |String |Yes |Header |UTC time of the API request, in seconds. Format: `YYYYMMDDTHHMMSSZ`. Example: `20201103T104027Z`. |
|X\-Security\-Token |String |No |Header |Temporary session token issued by the Security Token Service (STS). This parameter is not required when using a long\-term access key. |
|Authorization |String |Yes |Header |Signature. For details, refer to [Signing BytePlus MediaLive requests](https://docs.byteplus.com/byteplus-media-live/docs/signing-byteplus-medialive-requests). |
|Action |String |Yes |Query string |API operation. For example, `EnableDomain`. |
|Version |String |Yes |Query string |Version of the API operation. Current version: `2020-08-01`. |
|X\-Expires |Integer |No |Header |The validity period of the signature (unit: second). Default value: `900`. |


<span id="Responses"></span>
## Responses

<span id="Sample success response"></span>
### Sample success response

```json
{
    "ResponseMetadata":{
        "RequestId":"201806041104200100100232280022D30",
        "Action":"DescribeDomain",
        "Version":"2020-08-01",
        "Service":"live",
        "Region":"ap-singapore-1"
    },
    "Result":{
        "DomainList":[
            {
                "Domain":"push-rtmp-f5.example.com",
                "Status":0,
                "Type":"push",
                "Region":"cn",
                "CName":"push-rtmp-f5.example.com.c.bytefcdn.com",
                "PushDomain": "push-rtmp-f5.example.com",
                "Vhost": "push-rtmp-f5.example.com",
                "CnameCheck":0,
                "DomainCheck":0,
                "CreateTime":"2006-01-02T15:04:05Z"
           
            }
        ]
    }
}
```


If the call is successful, a response containing `ResponseMetadata` (common response parameters) and `Result` (operation\-specific parameters) is returned.

For operation\-specific parameters, see the detailed description of each API operation. For common response parameters, see the following table:


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |Unique ID of the API request. |
|Action |String |Name of the requested API operation. |
|Version |String |Version of the requested API operation. |
|Service |String |Name of the requested API service. |
|Region |String |Region of the requested API service. |


<span id="Sample error response"></span>
### Sample error response

```json
{
    "ResponseMetadata":{
        "RequestId":"201806041104200100100232280022D30",
        "Action":"DescribeDomain",
        "Version":"2020-08-01",
        "Service":"live",
        "Region":"ap-singapore-1",
        "Error":{
            "CodeN":100024,
            "Code":"InvalidAuthorization",
            "Message":"Invalid 'Authorization' header, Pls check your authorization header."
        }
    }
}
```


If an error occurs when you call an API operation, an error response containing the error code and error message is returned. For more information, see [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).

If you cannot resolve the problem, contact your technical support and provide the `RequestId` for troubleshooting purposes.
