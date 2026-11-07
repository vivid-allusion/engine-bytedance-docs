---
title: "ListOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListOfflineLogStoreTask_zh-tw"
---

獲取離線日誌轉存任務的列表。您可以指定一系列篩選條件對任務列表進行篩選。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=ListOfflineLogStoreTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `ListOfflineLogStoreTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Bucket |String |否 |指定儲存桶下存放日誌檔案的路徑作為篩選條件，格式為 `<儲存桶名稱>/<日誌檔案路徑>`。 |`mybucket/storage/logs` |
|Desc |String |否 |指定 `Desc` 作為篩選條件，支援模糊比對。 |`myDesc` |
|Domain |String |否 |指定一個 Domain 作為篩選條件，獲取轉存該網域名稱日誌的任務，也就是關聯了該任務的網域名稱。 |`www.example.com` |
|Region |String |否 |指定儲存桶所在的地域代碼（region code）作為篩選條件。地域代碼的長度不能超過 64 個字元。<br><br><br>* 如果 `TaskType` 為 `s3`，請諮詢該儲存桶的物件儲存服務提供者以取得您可以指定的地域代碼。<br><br>* 如果 `TaskType` 為 `tos`，您可以指定以下地域代碼：<br><br>   * `cn-hongkong`：表示中國香港。<br><br>   * `ap-southeast-1`：表示亞太東南（柔佛）。<br><br>   * `ap-southeast-3`：表示亞太東南（雅加達）。 |`cn-beijing` |
|Status |String |否 |指定一個任務的狀態作為篩選條件。該參數有以下取值：<br><br><br>* `enable`: 表示已啟用。<br><br>* `disable`: 表示已停用。 |`enable` |
|TaskID |String |否 |指定一個任務 ID 作為篩選條件。 |`nj2S29or5KaAeEiwcGWA5S` |
|TaskType |String |否 |指定一個轉存目標作為篩選條件。該參數有以下取值：<br><br><br>* `tos`：表示 BytePlus 物件儲存（TOS）。<br><br>* `s3`：表示 AWS S3 或使用相容 S3 驗證方式的物件儲存服務。 |`s3` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|TaskInfo |Object[] |表示符合篩選條件的任務列表。 | |
|AuthInformation |Object |表示轉存目標的存取憑證。 | |
|AccessKeyID |String |表示憑證中的 AccessKey ID。 |`xxxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |表示憑證中的 AccessKey Secret。 |`xxxxxxxxx` |
|Bucket |String |表示儲存桶下存放日誌檔案的路徑。 |`mybucket/log` |
|CreateTime |Long |表示任務的建立時間，格式是 Unix 時間戳。 |`1761908274` |
|Desc |String |表示任務的描述。 |`myDesc` |
|Domain |String |表示關聯了該任務的網域名稱。 |`www.example.net` |
|Endpoint |String |表示物件儲存服務的公網存取點。 |`tos-cn-shanghai.volces.com` |
|PrivateBucketAccess |Boolean |表示該儲存桶是否是私有的。 |`true` |
|Region |String |表示儲存桶所在的地域代碼（region code）。 |`us-east-1` |
|Status |String |表示該任務的狀態，該參數有以下取值：<br><br><br>* `enable`：表示任務已啟用。<br><br>* `disable`：表示任務已停用。 |`enable` |
|StatusDetail |Object[] |表示任務最近發生的異常列表。列表中最多記錄 10 個異常。 | |
|Detail |String |表示異常的詳情。 |`exception details` |
|Time |Long |表示異常發生的時間，格式為 Unix 時間戳。 |`1761815000` |
|TaskID |String |表示任務的 ID。 |`dPFEQ8vwbRShTdW5kNbZe3` |
|TaskType |String |表示日誌轉存目標，有以下取值：<br><br><br>* `tos`：表示 BytePlus 物件儲存（TOS）。<br><br>* `s3`：表示 AWS S3 或使用相容 S3 驗證方式的物件儲存服務。 |`s3` |
|UpdateTime |Long |表示該任務最近的更新時間，格式是 Unix 時間戳。 |`1761908274` |
|Total |Long |表示列表中的任務數量。 |`1` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=ListOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "mybucket/log",
    "Desc": "myDesc",
    "Domain": "www.example.net",
    "Region": "us-east-1",
    "Status": "enable",
    "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
    "TaskType": "s3"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20251103163008001C7913418610FF31AA",
        "Action": "ListOfflineLogStoreTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskInfo": [
            {
                "AuthInformation": {
                    "AccessKeyID": "xxxxxxxxxxxxxxx",
                    "AccessKeySecret": "xxxxxxxx"
                },
                "Bucket": "mybucket/log",
                "CreateTime": 1761908274,
                "Desc": "myDesc",
                "Domain": "www.example.net",
                "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
                "PrivateBucketAccess": true,
                "Region": "us-east-1",
                "Status": "enable",
                "StatusDetail": [],
                "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
                "TaskType": "s3",
                "UpdateTime": 1761908274
            }
        ],
        "Total": 1
    }
}
```


&nbsp;
