---
title: "UpdateCustomizationViewPermissionAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatecustomizationviewpermissionapi-zh-TW"
---

呼叫此 API 以更新直播活動的登入連結，讓您能夠使用自己的帳戶系統來管理觀看與評論權限。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`UpdateCustomizationViewPermissionAPI`

* 請求方法：POST

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=UpdateCustomizationViewPermissionAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參閱[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|ActivityId |是 |整數 |直播活動的 ID。 |
|CustomUrl |是 |字串 |指向您帳戶系統的自訂登入連結。 |
|CustomApp |否 |字串 |自訂檢視應用程式的名稱。 |
|ErrorRedirectUrl |否 |字串 |自訂驗證失敗時要重新導向的 URL。此 URL 必須包含協定。預設情況下，使用者會被重新導向至直播服務的預設驗證失敗頁面。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateCustomizationViewPermissionAPI&Version=2020-06-01
{
     "ActivityId":123,
     "CustomUrl":"www.example.com" }
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|SecretKey |字串 |用於根據您的帳戶系統驗證觀眾的密鑰。 |


<span id="Sample response"></span>
### 回應範例

```JSON
{
   "ResponseMetadata":{
     "RequestId": "201806041104200100100232280022D30",
     "Action":"UpdateCustomizationViewPermissionAPI",
     "Version":"2020-06-01",
     "Service":"livesaas",
     "Region":"ap-singapore-1" 
  },
   "Result":{
       "SecretKey":"qw***" 
  }
}
```
