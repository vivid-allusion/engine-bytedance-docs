---
title: "ListDomainDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023-zh-TW"
---

呼叫 `ListDomainDetail` API 以查詢您帳戶下的域名資訊。您可以根據域名狀態、域名類型及其他維度篩選查詢結果。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多查詢 1 次。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListDomainDetail&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListDomainDetail` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|PageNum |Integer |是 |`1` |頁碼。BytePlus MediaLive 將查詢結果分頁，僅返回指定頁碼的結果。有效範圍：1–1000。 |
|PageSize |Integer |是 |`10` |每頁結果數。有效範圍：1–1000。 |
|VhostList |Array of String |否 |`["push.example.com","pull.example.com"]` |名稱空間列表，預設為查詢所有名稱空間下的域名。 |
|DomainStatusList |Array of Integer |否 |`[0,2,3]` |查詢中包含的域名狀態列表。若未指定，將查詢所有狀態的域名。有效值包括：<br><br><br>* `0`：啟用。<br><br>* `1`：審核中。<br><br>* `2`：停用。注意，停用的域名無法使用。<br><br>* `3`：已刪除。<br><br>* `4`：審核未通過。您需要重新提交域名進行審核。<br><br>* `5`：因帳戶逾期付款而凍結。<br><br>* `6`：因未備案而封鎖域名。 |
|DomainTypeList |Array of String |否 |`["push","pull-flv"]` |查詢中包含的域名類型列表。若未指定，將查詢兩種類型的域名。有效值包括：<br><br><br>* `push`：推流域名。<br><br>* `pull-flv`：拉流域名。 |
|DomainRegionList |Array of String |否 |`["cn"]` |加速區域。有效值包括：<br><br><br>* `oversea`：（預設）中國大陸以外。<br><br>* `cn`：中國大陸。<br><br>* `global`：全球。 |
|DomainNameList |Array of String |否 |`["push.example.com","pull.example.com"]` |查詢中包含的域名列表。若未指定，將查詢您所有的域名。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |Array of [DomainList](https://docs.byteplus.com/en/docs/24/107295#domainlist) |`-` |域名資訊。 |
|Total |Integer |`2` |查詢結果總數。 |


<span id="domainlist"></span>
### DomainList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |對應的域名空間。 |
|Domain |String |`push.example.com` |域名。 |
|Status |Integer |`0` |域名狀態。有效值包括：<br><br><br>* `0`：啟用。<br><br>* `1`：審核中。<br><br>* `2`：停用。注意，停用的域名無法使用。<br><br>* `3`：已刪除。<br><br>* `4`：審核未通過。您需要重新提交域名進行審核。<br><br>* `5`：因帳戶逾期付款而凍結。<br><br>* `6`：因未備案而封鎖域名。 |
|Type |String |`pull` |域名類型。有效值包括：<br><br><br>* `push`：推流域名。<br><br>* `pull-flv`：拉流域名。 |
|Region |String |`cn` |加速區域列表。有效值包括：<br><br><br>* `oversea`：中國大陸以外。<br><br>* `cn`：中國大陸。<br><br>* `global`：全球。 |
|CNAME |字串 |`push.example.com.bytefcdn.com` |分配給該網域名稱的 CNAME 位址。 |
|CnameCheck |整數 |`0` |CNAME 位址的狀態。<br><br><br>* `0`：未配置。<br><br>* `1`：已配置。 |
|DomainCheck |整數 |`0` |網域名稱的可用性。<br><br><br>* `0`：正常。網域名稱可用且已配置。<br><br>* `1`：配置中。網域名稱可用且正在配置。<br><br>* `2`：不可用。網域名稱不可用。 |
|ICPCheck |整數 |`1` |網域是否已完成 ICP 註冊。當網域加速區域包含中國大陸時，將驗證此參數。若網域加速區域不包含中國大陸，請忽略此參數。 |
|CreateTime |字串 |`2006-01-02T15:04:05+08:00` |網域名稱建立的時間。 |
|CertDomain |字串 |`*.example.com` |由相關憑證保護的萬用網域名稱。 |
|HTTP2 |布林值 |`false` |是否啟用 HTTP/2 協議。值如下：<br><br><br>* `false`：未啟用<br><br>* `true`：已啟用 |
|ChainID |字串 |`21614` |相關憑證的鏈 ID。 |
|PushDomain |字串 |`push.example.com` |用於推流的相關網域名稱。 |
|ProjectName |字串 |`default` |與網域名稱空間相關的專案。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListDomainDetail&Version=2023-01-01
{
    "DomainTypeList": [
        "pull-flv",
        "push"
    ],
    "PageNum": 1,
    "PageSize": 10
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata":{
        "RequestId":"201806041104200100100232280022D30",
        "Action":"ListDomainDetail",
        "Version":"2023-01-01",
        "Service":"live",
        "Region": "cn-north-1"
    }
    "Resutl": { 
        "DomainList": [
            {
                "Domain": "push.example.com",
                "Status": 0,
                "Type": "push",
                "Region": "cn",
                "CName": "push.example.com.bytefcdn.com",
                "CnameCheck":0,
                "DomainCheck":0,
                "CreateTime":"2006-01-02T15:04:05+08:00"
            },
            {
                "Domain": "pull.example.com",
                "Status": 0,
                "Type": "pull",
                "Region": "cn",
                "CName": "pull.example.com.bytefcdn.com",
                "CnameCheck":0,
                "DomainCheck":0,
                "CreateTime":"2006-01-02T15:04:05+08:00"
            }
        ],
        "Total": 2 
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107295#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParameter.Tags.Key |指定的參數 Tags.Key 無效。 |參數`Tags.Key`驗證失敗。請檢查該參數是否正確。 |
|400 |InvalidParameter.Tags.Value |指定的參數 Tags.Value 無效。 |參數`Tags.Value`驗證失敗。請檢查該參數是否正確。 |
