---
title: "CreateOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateOfflineLogStoreTask_zh-tw"
---

在 CDN 中建立一個離線日誌轉存任務。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `CreateOfflineLogStoreTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Bucket |String |是 |表示儲存桶下存放日誌檔案的目錄路徑，不能以 `/` 結尾，格式為 `<儲存桶名稱>/<目錄路徑>`。<br><br>如果路徑中的目錄不存在，CDN 會在儲存桶下建立對應的目錄。 |`mybucket/storage/logs` |
|Domain |String |是 |表示要投遞哪些網域名稱的即時日誌，也就是該任務將關聯的網域名稱。<br><br><br>* 如果您要關聯帳戶下的所有網域名稱，請傳入`*`。這裡，所有網域名稱涵蓋您後續在 CDN 中新增的網域名稱。<br><br>* 如果您要關聯指定的網域名稱，請傳入待關聯的網域名稱列表，列表中最多可以包含 200 個網域名稱，多個網域名稱之間以逗號（,）分隔。<br><br><br>注意<br><br>如果您已建立了關聯帳戶下所有網域名稱的任務，則無法再建立關聯指定網域名稱的任務。反之亦然。<br><br>您可以呼叫 [ListOfflineLogStoreTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListOfflineLogStoreTask_zh-tw) 並指定該網域名稱作為篩選條件，以檢視該網域名稱是否已與某個任務關聯。 |`www.example.com,img.example.com` |
|Endpoint |String |是 |表示物件儲存服務的公網存取點，不包含儲存桶的名稱。<br><br><br>* 如果 `TaskType` 為 `s3`，存取點必須以 `https://`開頭，不包含儲存桶的名稱，長度不能超過 1,024 個字元。<br><br>* 如果 `TaskType` 為 `tos`，該參數有以下取值，與 `Region` 的取值對應。<br><br>   * `tos-cn-hongkong.volces.com`<br><br>   * `tos-ap-southeast-1.volces.com`<br><br>   * `tos-ap-southeast-3.volces.com` |`https://oss-ap-southeast-1.aliyuncs.com` |
|Region |String |是 |表示儲存桶所在的地域代碼（region code），長度不能超過 64 個字元。<br><br><br>* 如果 `TaskType` 為 `s3`，請諮詢該儲存桶的物件儲存服務提供者以取得該儲存桶的地域代碼。<br><br>* 如果 `TaskType` 為 `tos`，地域代碼有以下取值：<br><br>   * `cn-hongkong`：表示中國香港。<br><br>   * `ap-southeast-1`：表示亞太東南（柔佛）。<br><br>   * `ap-southeast-3`：表示亞太東南（雅加達）。 |`ap-southeast-1` |
|TaskType |String |是 |表示日誌轉存目標，有以下取值：<br><br><br>* `tos`：表示 BytePlus 物件儲存（TOS）。<br><br>* `s3`：表示 AWS S3 或使用相容 S3 驗證方式的物件儲存服務。 |`s3` |
|AuthInformation |Object |否 |表示轉存目標的存取憑證。僅當 `PrivateBucketAccess` 為 `true` 並且 `TaskType` 為 `s3` 時，您需要指定該結構體。 | |
|AccessKeyID |String |否 |表示憑證中的 AccessKey ID。 |`xxxxxxxxxxxxx` |
|AccessKeySecret |String |否 |表示憑證中的 AccessKey Secret。 |`xxxxx` |
|Desc |String |否 |表示任務的描述，長度為 3\-45 個字元，可以包含漢字，字母，數字，但不能以下劃線（_）開頭或結尾。 |`myDesc` |
|PrivateBucketAccess |Boolean |否 |表示該儲存桶是否是私有的，該參數有以下取值：<br><br><br>* `true`<br><br>* `false`<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|TaskID |String |表示任務的 ID。 |`nj2S29or5KaAeEiwcGWA5S` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

**日志转存目标为 TOS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "myBucket/logfile",
    "Desc": "myDesc",
    "Domain": "www.example.com,img.example.com",
    "Endpoint": "tos-ap-southeast-1.volces.com",
    "PrivateBucketAccess": true,
    "Region": "ap-southeast-1",
    "TaskType": "tos"
}
```


**日志转存目标为 AWS S3**

```json
POST https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021-03-01
{
    "AuthInformation": {
        "AccessKeyID": "xxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxx"
    },
    "Bucket": "mybucket/log",
    "Desc": "myDesc",
    "Domain": "www.example.com",
    "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
    "PrivateBucketAccess": true,
    "Region": "us-east-1",
    "TaskType": "s3"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202510311813528D239468E6A7A99DA92C",
        "Action": "CreateOfflineLogStoreTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "5daCXtLTDpRYDDhFruQ9hP"
    }
}
```


&nbsp;
