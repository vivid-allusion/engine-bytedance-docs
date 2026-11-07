---
title: "UpdateAuthKey"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023-zh-TW"
---

呼叫 `UpdateAuthKey` API，以新增或更新推流與拉流地址的 URL 驗證配置。使用此 API 更新配置時，所有驗證參數都會被更新。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateAuthKey&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須傳入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateAuthKey` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domain |String |是 |`live.push.example.com` |網域名稱。可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的 [網域管理](https://console.byteplus.com/live/main/domain/list)頁面取得網域名稱。 |
|SceneType |String |是 |`push` |驗證場景類型，取值及含義如下。<br><br><br>* `push`：推流驗證。<br><br>* `pull`：拉流驗證。 |
|AuthDetailList |[AuthDetailList](https://docs.byteplus.com/en/docs/24/107265#authdetaillist) 陣列 |是 |`-` |驗證資訊列表。最多可新增 100 個陣列元素。 |
|ValidDuration |Integer |否 |`60` |驗證資訊的有效期間，單位為秒。預設值為 `0`。有效範圍：[0,2592000]。 |
|PushPullEnable |Boolean |否 |`true` |是否啟用目前的驗證配置。<br><br><br>* `false`：（預設）未啟用。<br><br>* `true`：已啟用。 |
|TimeStampBase |Integer |否 |`10` |時間戳格式。預設值為 `10`。但當 `AuthType` 的值設為 `TypeC` 時，預設值為 `16`。有效取值：<br><br><br>* `2`：二進位。<br><br>* `8`：八進位。<br><br>* `10`：十進位。<br><br>* `16`：十六進位。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>SceneType</code> 的值設為 <code>push</code> 時，此參數值固定為 <code>10</code>。</div><br> |


<span id="authdetaillist"></span>
### AuthDetailList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|SecretKey |String |是 |`1*****1` |驗證密鑰。可包含大寫字母（A\-Z）、小寫字母（a\-z）及數字（0\-9），長度為 1 到 100 字元。 |
|EncryptionAlgorithm |String |是 |`md5` |加密字串生成演算法。有效取值：<br><br><br>* `md5`：標準 MD5 演算法。當 `AuthType` 的值設為 `TypeA`、`TypeB` 或 `TypeC` 時，此參數值必須設為 `md5`。<br><br>* `md5_custom`：自定義 MD5 演算法。當 `AuthType` 的值設為 `TypeCustom` 時，此參數值必須設為 `md5_custom`。 |
|AuthField |JSON Map |否 |`{ "volcSecret":"signature","volcTime":"expireTime" }` |驗證參數名稱。僅當 `AuthType` 的值設為 `TypeCustom` 時，才需配置此參數。<br><br>此參數值為 Key\-Value 對。預設值為 `{"volcSecret":"sign","volcTime":"expire"}`。你可以自定義 `volcSecret` 和 `volcTime` 對應的值，例如 `{"volcSecret":"signature","volcTime":"expireTime"}`，這表示以 `signature` 作為加密字串的驗證參數名稱，以 `expireTime` 作為時間戳的驗證參數名稱，從而啟用 URL 驗證。 |
|EncryptField |String 陣列 |否 |`["key","volcTime","Domain"]` |產生加密字串所需的欄位。僅當`AuthType`的值設為`TypeCustom`時，才需要配置此參數。<br><br>此參數預設為空，但建議至少包含`SecretKey`（驗證金鑰）和`volcTime`（時間戳）。例如，若參數值為`["SecretKey","volcTime","Domain"]`，則可使用`md5({SecretKey}{volcTime}{Domain})`計算加密字串。 |
|AuthType |String |是 |`TypeB` |URL 驗證型別。有效值：<br><br><br>* `TypeA`：A 型。<br><br>* `TypeB`：B 型。<br><br>* `TypeC`：C 型。<br><br>* `TypeCustom`：自訂型。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當<code>SceneType</code>的值設為<code>push</code>時，此參數僅可為<code>TypeB</code>或<code>TypeCustom</code>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如需瞭解 A 型、B 型或 C 型的更多資訊，請參見<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">設定 URL 驗證</a>。</div><br> |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateAuthKey&Version=2023-01-01
{
    "AuthDetailList": [
        {
            "SecretKey": "1*****1",
            "EncryptionAlgorithm": "md5",
            "AuthType": "TypeB"
        }
    ],
    "Domain": "live.push.example.com",
    "PushPullEnable": true,
    "SceneType": "push",
    "ValidDuration": 60,
    "TimeStampBase": 10
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateAuthKey",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107265#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Length |%s 不應超過 %d |參數長度不正確。請檢查錯誤訊息中指定參數的長度是否超出限制。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未啟用計費狀態，請開通服務或儲值。 |尚未啟用視訊直播服務或帳號欠費，導致帳單不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到網域名稱空間（Vhost）。請檢查傳入的網域名稱空間是否與實際使用的一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
