---
title: "ListRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_zh-tw"
---

取得即時日誌投遞任務的列表。您可以指定一系列過濾條件對任務列表進行過濾。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=ListRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `ListRealtimeLogDeliveryTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Desc |String |否 |指定 `Desc` 作為過濾條件，支援模糊比對。 |`my` |
|Domain |String |否 |指定一個 Domain 作為過濾條件，取得投遞該網域日誌的任務。 |`www.example.com` |
|Status |String |否 |指定一個任務的狀態作為過濾條件。該參數有以下取值：<br><br><br>* `enable`: 表示已啟用。<br><br>* `disable`: 表示已停用。 |`enable` |
|TaskID |String |否 |指定一個任務 ID 作為過濾條件。 |`33a1f4df-f384-453e-9d59-3e9ff4b04b4e` |
|TaskType |String |否 |指定一個投遞目標作為篩選條件。該參數有以下取值：<br><br><br>* `tls`：表示 BytePlus 日誌服務（TLS）。<br><br>* `sls`：表示阿里雲日誌服務（SLS）。<br><br>* `http_server`：表示 HTTP 伺服器。<br><br>* `splunk`: 表示 Splunk 日誌服務。 |`tls` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|TaskInfo |Object[] |表示符合過濾條件的任務列表。 | |
|Area |String |該參數值始終是 `outside_chinese_mainland`。 |`outside_chinese_mainland` |
|CreateTime |Long |表示任務的建立時間，格式是 Unix 時間戳記。 |`1761816153` |
|Desc |String |表示任務的描述。 |`myDesc` |
|Domain |String |表示任務所關聯的網域列表，也就是該任務投遞的是哪些網域的日誌。 |`www.example.com` |
|HttpServer |Object |當 `TaskType` 為 `http_server` 時，該結構體表示 HTTP 伺服器側的相應配置。 | |
|AuthMechanism |Boolean |表示 HTTP 伺服器是否啟用了鑑權。該參數有以下取值：<br><br><br>* `true`。<br><br>* `false`。 |`true` |
|CompressType |String |表示在 CDN 投遞日誌時所啟用壓縮類型。該參數有以下取值：<br><br><br>* `gzip`：表示 Gzip 壓縮。<br><br><br>如果該參數為空（""），表示未啟用壓縮。 |`gzip` |
|RequestHeader |Object[] |表示 CDN 在向 HTTP 伺服器投遞日誌時，請求中包含的額外頭部列表。 | |
|Key |String |表示列表中一個頭部的 Key。 |`key1` |
|Value |String |表示 `Key` 的值。 |`value1` |
|SecretKey |String |表示鑑權 Key，用於計算權杖。該參數僅當 `AuthMechanism` 為 `true` 時才有效。<br><br>關於更多關於鑑權流程與權杖演算法的資訊，參見 [建立日誌投遞任務](https://www.volcengine.com/docs/6454/1536426#http-%E6%9C%8D%E5%8A%A1%E5%99%A8)。 |`xxxxxxxxxxx` |
|Url |String |表示 HTTP 伺服器的存取點、連接埠以及日誌存放的路徑。 |`http://www.example.com:8080/mylog` |
|SampleRate |Double |表示日誌採樣率。 |`50` |
|Sls |Object |當 `TaskType` 為 `sls` 時，該結構體表示 SLS 側的相應配置。 | |
|AccessKeyId |String |表示您阿里雲帳號的 AccessKey ID。 |`xxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |表示您阿里雲帳號的 AccessKey Secret。 |`xxxxxxxxxxxxx` |
|Endpoint |String |表示 `Project` 的公網網域。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |表示儲存日誌的 LogStore。 |`my_store` |
|Project |String |表示 `LogStore` 所屬的日誌專案。該專案在 `Endpoint` 所對應的投遞地域下。 |`my_project` |
|Status |String |表示該任務的狀態，該參數有以下取值：<br><br><br>* `enable`：表示任務已啟用。<br><br>* `disable`：表示任務已停用。 |`enable` |
|StatusDetail |Object[] |表示任務最近發生的異常列表。列表中最多記錄 10 個異常。 | |
|Detail |String |表示異常的詳情。 |`exception details` |
|Time |Long |表示異常發生的時間，格式為 Unix 時間戳記。 |`1761815000` |
|TaskID |String |表示任務的 ID。 |`42de0332-b6e0-4fe1-9a5a-847bb7471def` |
|TaskType |String |表示投遞目標，有以下取值：<br><br><br>* `tls`：表示火山引擎日誌服務（TLS）。<br><br>* `sls`：表示阿里雲日誌服務（SLS）。<br><br>* `http_server`：表示 HTTP 伺服器。<br><br>* `http_server`：表示 HTTP 伺服器。<br><br>* `splunk`: 表示 Splunk 日誌服務。 |`tls` |
|Tls |Object |當 `TaskType` 為 `tls` 時，該結構體表示 TLS 側的相應配置。 | |
|Endpoint |String |表示 `Project` 的公網網域。 |`tls-ap-southeast-1.volces.com` |
|ProjectID |String |表示日誌主題所屬的日誌專案 ID。該專案在 `Endpoint` 所對應的投遞地域下。 |`a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747` |
|ProjectName |String |表示日誌主題所屬的日誌專案名稱。 |`test` |
|Region |String |表示日誌專案所在的地域。該參數有以下取值：<br><br><br>* `cn-beijing`：表示華北2（北京）。<br><br>* `cn-shanghai`：表示華東2（上海）。<br><br>* `cn-guangzhou`：表示華南1（廣州）。 |`ap-southeast-1` |
|TopicID |String |表示儲存日誌的日誌主題 ID。 |`b23298e8-c262-4cb6-8138-2c311230b972` |
|TopicName |String |表示儲存日誌的日誌主題的名稱。 |`test4` |
|Ttl |Long |表示日誌的儲存時長，單位是天。<br><br>如果該參數值是 `3650`，表示日誌為永久保存。 |`3` |
|UpdateTime |Long |表示該任務最近的更新時間，格式是 Unix 時間戳記。 |`1761816153` |
|Splunk |Object |當 `TaskType` 為 `splunk` 時，該結構體表示 Splunk 側的相應配置。 | |
|CompressType |String |表示在 CDN 日誌傳遞時，是否啟用 Gzip 壓縮。該參數有以下取值：<br><br><br>* `true`：表示啟用 Gzip 壓縮。<br><br>* `false`：表示不啟用 Gzip 壓縮。 |`true` |
|Token |String |表示 HEC 鑑權 Token。 |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |表示 HEC 介面位址。 |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |當 `TaskType` 為 `bigquery` 時，該結構體表示 BigQuery 側的相應配置。 | |
|Authentication |String |Google Cloud 服務帳號 (Service Account) 的 JSON 格式金鑰。該金鑰包含身分認證資訊，用於授權 BytePlus CDN 存取您的 BigQuery 資源並串流寫入日誌。 | |
|DatasetID |String |您在 BigQuery 中建立的資料集 (Dataset) ID。 |`my_dataset` |
|ProjectID |String |BigQuery 所在的 GCP 專案 (Project) ID。 |`my-project` |
|TableID |String |您在 BigQuery 中建立的資料表 (Table) ID。 |`my_table` |
|Total |Long |表示列表中的任務數量。 |`3` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=ListRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Desc": "my",
    "Domain": "www.example.com",
    "TaskType": "tls",
    "Status": "enable",
    "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20251030175056FC7B92C49D1494225A51",
        "Action": "ListRealtimeLogDeliveryTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskInfo": [
            {
                "Area": "outside_chinese_mainland",
                "CreateTime": 1761816153,
                "Desc": "myDesc",
                "Domain": "www.example.com",
                "HttpServer": null,
                "SampleRate": 100,
                "Sls": null,
                "Status": "enable",
                "StatusDetail": [],
                "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972",
                "TaskType": "tls",
                "Tls": {
                    "Endpoint": "tls-ap-southeast-1.volces.com",
                    "ProjectID": "a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747",
                    "ProjectName": "test",
                    "Region": "ap-southeast-1",
                    "TopicID": "b23298e8-c262-4cb6-8138-2c311230b972",
                    "TopicName": "test4",
                    "Ttl": 7
                },
                "UpdateTime": 1761816153
            }
        ],
        "Total": 1
    }
}
```


&nbsp;
