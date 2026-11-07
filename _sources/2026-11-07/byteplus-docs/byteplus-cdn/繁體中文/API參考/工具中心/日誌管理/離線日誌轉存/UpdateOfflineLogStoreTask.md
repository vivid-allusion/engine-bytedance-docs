---
title: "UpdateOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateOfflineLogStoreTask_zh-tw"
---

修改一個離線日誌轉存任務的設定。在呼叫該 API 時，如果某個參數未指定，該參數將被設定為預設值。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=UpdateOfflineLogStoreTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `UpdateOfflineLogStoreTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Bucket |String |是 |表示儲存桶下存放日誌檔案的目錄路徑，不能以 `/` 結尾，格式為 `<儲存桶名稱>/<目錄路徑>`。<br><br>如果路徑中的目錄不存在，CDN 會在儲存桶下建立對應的目錄。 |`mybucket/new/logs` |
|Domain |String |是 |表示該任務將關聯的網域名稱列表。<br><br><br>* 如果您要關聯帳戶下的所有網域名稱，請傳入`*`。這裡，所有網域名稱涵蓋您後續在 CDN 中新增的網域名稱。<br><br>* 如果您要關聯指定的網域名稱，請傳入待關聯的網域名稱列表，列表中最多可以包含 200 個網域名稱，多個網域名稱之間以逗號（,）分隔。<br><br><br>注意<br><br>如果已存在關聯指定網域名稱的其他任務，您無法指定 `Domain` 為 `*`。<br><br>您可以呼叫 [ListOfflineLogStoreTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_zh-tw) 並指定該網域名稱作為篩選條件，以檢視該網域名稱是否已與某個任務關聯。 |`www.example.com` |
|Endpoint |String |是 |表示物件儲存服務的公網存取點，不包含儲存桶的名稱。<br><br><br>* 如果 `TaskId` 所表示任務的轉存目標為 `s3`，存取點必須以 `https://`開頭，不包含儲存桶的名稱，長度不能超過 1,024 個字元。<br><br>* 如果轉存目標為 `tos`，該參數有以下取值，與 `Region` 的取值對應。<br><br>   * `tos-cn-hongkong.volces.com`<br><br>   * `tos-ap-southeast-1.volces.com`<br><br>   * `tos-ap-southeast-3.volces.com` |`tos-ap-southeast-1.volces.com` |
|Region |String |是 |表示儲存桶所在的地域代碼（region code），長度不能超過 64 個字元。<br><br><br>* 如果 `TaskId` 所表示任務的轉存目標為 `s3`，請諮詢該儲存桶的物件儲存服務提供者以取得該儲存桶的地域代碼。<br><br>* 如果轉存目標為 `tos`，地域代碼有以下取值：<br><br>   * `cn-hongkong`：表示中國香港。<br><br>   * `ap-southeast-1`：表示亞太東南（柔佛）。<br><br>   * `ap-southeast-3`：表示亞太東南（雅加達）。 |`ap-southeast-1` |
|TaskID |String |是 |表示一個待修改任務的 ID。 |`dPFEQ8vwbRShTdW5kNbZe3` |
|AuthInformation |Object |否 |表示轉存目標的存取憑證。僅當 `PrivateBucketAccess` 為 `true` 並且 `TaskType` 為 `s3` 時，您需要指定該結構體。 | |
|AccessKeyID |String |否 |表示憑證中的 AccessKey ID。 |`xxxxxxxxxx` |
|AccessKeySecret |String |否 |表示憑證中的 AccessKey Secret。 |`xxxxxx` |
|Desc |String |否 |表示任務的描述，長度為 3\-45 個字元，可以包含漢字，字母，數字，但不能以下劃線（_）開頭或結尾。 |`newDesc` |
|PrivateBucketAccess |Boolean |否 |表示該儲存桶是否是私有的，該參數有以下取值：<br><br><br>* `true`<br><br>* `false`<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=UpdateOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "mybucket/new/log",
    "Desc": "myDesc_new",
    "Domain": "www.example.com",
    "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
    "PrivateBucketAccess": true,
    "Region": "us-east-1",
    "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
    "AuthInformation": {
        "AccessKeyID": "xxxxxxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxxxx"
    }
}
```


&nbsp;
