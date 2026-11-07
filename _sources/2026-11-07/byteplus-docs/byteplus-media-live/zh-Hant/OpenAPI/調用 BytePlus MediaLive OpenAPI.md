---
title: "調用 BytePlus MediaLive OpenAPI"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-calling-byteplus-medialive-openapi-zh-TW"
---

若要成功與 BytePlus MediaLive 服務互動，您必須正確構建 API 請求。本主題涵蓋每個 API 調用的基本組成部分，包括服務地址、所需協議、請求方法、通用參數，以及成功與錯誤響應的結構。了解這些基礎知識是整合任何 BytePlus MediaLive OpenAPI 的第一步。

<span id="API request"></span>
## API 請求

BytePlus MediaLive OpenAPI 請求包含以下部分：

<span id="Service address"></span>
### 服務地址

URL：open.byteplusapi.com

<span id="Protocol"></span>
### 協議

BytePlus MediaLive OpenAPI 支援 HTTP 及 HTTPS 協議。建議您使用 HTTPS 以確保 API 請求的安全性。

<span id="Character encoding"></span>
### 字元編碼

API 請求與回應均採用**UTF\-8**編碼。

<span id="Request method"></span>
### 請求方法

大多數 BytePlus MediaLive OpenAPI 服務支援**GET**與**POST**方法。


* **GET**：向伺服器發送請求以返回指定資源。公共資料可加入至標頭與查詢字串參數中。

* **POST**：向伺服器發送請求以新增資源或執行特殊操作。公共資料僅可加入至標頭。


<span id="Request URI"></span>
### 請求 URI

格式：`{URI-scheme}://{domain}/?{query-string}`。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/258f59a-Request_URI.png) </span>


|**組件** |**說明** |
|---|---|
|URI scheme |指定傳輸協議。支援 HTTP 及 HTTPS。 |
|網域 |網域名稱。BytePlus MediaLive OpenAPI 的網域名稱為`open.byteplusapi.com`。 |
|查詢字串 |包含通用請求參數與操作專屬參數。有關操作專屬參數及部分通用請求參數，請參閱各 API 操作的詳細說明。完整通用請求參數列表，請參閱[通用請求參數](/docs/byteplus\-media\-live/docs\-calling\-byteplus\-medialive\-openapi#Common request parameters)。 |


<span id="Common request parameters"></span>
## 通用請求參數


|**名稱** |**型別** |**是否必填** |**位置** |**說明** |
|---|---|---|---|---|
|Host |字串 |是 |標頭 |端點。設為`open.byteplusapi.com`。 |
|Content\-Type |字串 |是 |標頭 |多用途網際網路郵件擴展（MIME）資源型別。若個別操作無特殊要求，請設為`application/json; charset=utf-8` |
|X\-Date |字串 |是 |標頭 |API 請求的 UTC 時間，精確到秒。格式：`YYYYMMDDTHHMMSSZ`。範例：`20201103T104027Z`。 |
|X\-Security\-Token |字串 |否 |標頭 |由安全憑證服務（STS）簽發的臨時會話令牌。使用長期存取金鑰時無需填寫。 |
|Authorization |字串 |是 |標頭 |簽名。詳情請參閱[簽名 BytePlus MediaLive 請求](https://docs.byteplus.com/byteplus-media-live/docs/signing-byteplus-medialive-requests) |
|Action |字串 |是 |查詢字串 |API 操作。例如，`EnableDomain`。 |
|Version |字串 |是 |查詢字串 |API 操作的版本。目前版本：`2020-08-01`。 |
|X\-Expires |整數 |否 |標頭 |簽名的有效期限（單位：秒）。預設值：`900`。 |


<span id="Responses"></span>
## 回應

<span id="Sample success response"></span>
### 成功回應範例

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


調用成功時，會返回包含`ResponseMetadata`（通用回應參數）及`Result`（操作專屬參數）的回應。

有關操作專屬參數，請參閱各 API 操作的詳細說明。有關通用回應參數，請參閱下表：


|**名稱** |**型別** |**說明** |
|---|---|---|
|RequestId |字串 |API 請求的唯一 ID。 |
|Action |字串 |所請求 API 操作的名稱。 |
|Version |字串 |所請求 API 操作的版本。 |
|Service |字串 |所請求 API 服務的名稱。 |
|Region |字串 |所請求 API 服務的區域。 |


<span id="Sample error response"></span>
### 錯誤回應範例

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


當您調用 API 操作時發生錯誤，將返回包含錯誤碼與錯誤訊息的錯誤回應。如需更多資訊，請參閱[常見錯誤碼](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes)。

若您無法解決問題，請聯繫您的技術支援，並提供`RequestId`以便故障排除。
