---
title: "调用 BytePlus MediaLive OpenAPI"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-calling-byteplus-medialive-openapi-zh-CN"
---

要成功与 BytePlus MediaLive 服务进行交互，必须正确构建 API 请求。本主题介绍每个 API 调用的基本组成部分，包括服务地址、所需协议、请求方式、常用参数，以及成功和错误返回调用结果的结构。理解这些基础内容是集成任何 BytePlus MediaLive OpenAPI 的第一步。

<span id="API request"></span>
## API 请求

BytePlus MediaLive OpenAPI 请求由以下部分组成：

<span id="Service address"></span>
### 服务地址

URL：open.byteplusapi.com

<span id="Protocol"></span>
### 协议

BytePlus MediaLive OpenAPI 支持 HTTP 和 HTTPS 协议。建议使用 HTTPS 以确保 API 请求的安全性。

<span id="Character encoding"></span>
### 字符编码

API 请求和返回调用结果均采用 **UTF\-8** 编码。

<span id="Request method"></span>
### 请求方式

大多数 BytePlus MediaLive OpenAPI 服务支持 **GET** 和 **POST** 请求方式。


* **GET**：向服务器发送请求以返回指定资源。公共数据可添加到请求头和查询字符串参数中。

* **POST**：向服务器发送请求以新增资源或执行特殊操作。公共数据只能添加到请求头中。


<span id="Request URI"></span>
### 请求 URI

格式：`{URI-scheme}://{domain}/?{query-string}`。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/258f59a-Request_URI.png) </span>


|**组件** |**接口行为** |
|---|---|
|URI scheme |指定传输协议。支持 HTTP 和 HTTPS。 |
|Domain |域名。BytePlus MediaLive OpenAPI 的域名为 `open.byteplusapi.com`。 |
|查询字符串 |包含常用请求参数和操作特定参数。操作特定参数及部分常用请求参数请参见每个 API 操作的详细说明。完整常用请求参数列表请参见 [常用请求参数](/docs/byteplus\-media\-live/docs\-calling\-byteplus\-medialive\-openapi#Common request parameters)。 |


<span id="Common request parameters"></span>
## 常用请求参数


|**名称** |**类型** |**是否必填** |**位置** |**接口行为** |
|---|---|---|---|---|
|Host |String |是 |Header |终端节点。值设置为 `open.byteplusapi.com`。 |
|Content\-Type |String |是 |Header |多用途互联网邮件扩展（MIME）资源类型。如无单独操作的特殊要求，值设置为 `application/json; charset=utf-8` |
|X\-Date |String |是 |Header |API 请求的 UTC 时间，精确到秒。格式：`YYYYMMDDTHHMMSSZ`。示例：`20201103T104027Z`。 |
|X\-Security\-Token |String |否 |Header |由安全令牌服务（STS）签发的临时会话令牌。使用长期访问密钥时无需填写。 |
|Authorization |String |是 |Header |签名。详情请参见 [签名 BytePlus MediaLive 请求](https://docs.byteplus.com/byteplus-media-live/docs/signing-byteplus-medialive-requests) |
|Action |String |是 |查询字符串 |API 操作。例如 `EnableDomain`。 |
|Version |String |是 |查询字符串 |API 操作的版本。当前版本：`2020-08-01`。 |
|X\-Expires |Integer |否 |Header |签名的有效期（单位：秒）。默认值：`900`。 |


<span id="Responses"></span>
## 返回调用结果

<span id="Sample success response"></span>
### 成功返回调用结果示例

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


如果调用成功，将返回包含 `ResponseMetadata`（常用返回参数）和 `Result`（操作特定参数）的返回调用结果。

操作特定参数请参见每个 API 操作的详细说明。常用返回参数请参见下表：


|**名称** |**类型** |**接口行为** |
|---|---|---|
|RequestId |String |API 请求的唯一 ID。 |
|Action |String |请求的 API 操作名称。 |
|Version |String |请求的 API 操作版本。 |
|Service |String |请求的 API 服务名称。 |
|Region |String |所请求 API 服务的区域。 |


<span id="Sample error response"></span>
### 错误返回调用结果示例

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


调用 API 操作时发生错误，将返回包含错误码和错误信息的错误返回调用结果。更多信息请参见 [常见错误码](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes)。

如无法解决问题，请联系技术支持并提供 `RequestId` 以便排查。
