---
title: "CreateRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateRealtimeLogDeliveryTask_zh-tw"
---

在 CDN 中创建一个实时日志投递任务。主账号下最多可以存在 20 个任务。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `CreateRealtimeLogDeliveryTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Area |String |是 |表示從哪個加速區域內的 CDN 節點上採集日誌。目前，該參數值只能是 `chinese_mainland`，表示中國內地。 |`outside_chinese_mainland` |
|Domain |String |是 |表示投遞哪些網域的即時日誌，也就是該任務所關聯的網域。<br><br><br>* 如果您要關聯帳號下的所有網域，請傳入`*`。這裡，所有網域涵蓋您後續在 CDN 中添加的網域。<br><br>* 如果您要關聯指定的網域，請傳入待關聯的網域列表，列表中最多可以包含 200 個網域，多個網域之間以逗號（,）分隔。<br><br><br>注意<br><br>如果您已建立了關聯帳號下所有網域的任務，則無法再建立關聯指定網域的任務。反之亦然。<br><br>您可以呼叫 ListRealtimeLogDeliveryTask 並指定該網域作為過濾條件，以查看該網域是否已與某個任務關聯。 |`www.example.com,img.example.com` |
|TaskType |String |是 |表示投遞目標，有以下取值：<br><br><br>* `tls`：表示 BytePlus 日誌服務（TLS）。<br><br>* `sls`：表示阿里雲日誌服務（SLS）。<br><br>* `http_server`：表示 HTTP 伺服器。<br><br>* `splunk`: 表示 Splunk 日誌服務。<br><br>* `bigquery`: 表示 GCP BigQuery。 |`sls` |
|Desc |String |否 |表示任務的描述。該參數的輸入要求如下：<br><br><br>* 長度為 3 \- 64 個字元，可以包含中文、字母、數字、底線（_）和連字號（\-）。中文佔 3 個字元。<br><br>* 不能以連字號（\-）或底線（_）開頭或結尾。 |`my desc` |
|HttpServer |Object |否 |當 `TaskType` 為 `http_server` 時，該結構體表示 HTTP 伺服器側的相應配置。 | |
|AuthMechanism |Boolean |否 |表示 HTTP 伺服器是否啟用了鑑權。該參數有以下取值：<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |否 |表示在 CDN 投遞日誌時所啟用壓縮類型。該參數有以下取值：<br><br><br>* `gzip`：表示 Gzip 壓縮。<br><br><br>如果該參數不指定，表示不啟用壓縮。 |`gzip` |
|RequestHeader |Object[] |否 |表示 CDN 在向 HTTP 伺服器投遞日誌時，請求中需要額外包含的頭部列表。列表中最多可以包含 10 個頭部。<br><br>如果該參數不指定，表示請求中不添加額外的頭部。 | |
|Key |String |否 |表示列表中一個頭部的 Key，長度不能超過 1,024 個字元。`Key` 不能是 `User-Agent`，也不能以 `x-bdcdn-` 開頭 |`mykey` |
|Value |String |否 |表示 `Key` 的值，長度不能超過 1,024 個字元。 |`myvalue` |
|SecretKey |String |否 |表示鑑權 Key，用於計算權杖。該參數的長度為 6\-40 個字元。<br><br>如果 `AuthMechanism` 為 `true`，`SecretKey` 必須指定。<br><br>關於更多關於鑑權流程與權杖演算法的資訊，參見 [建立日誌投遞任務](https://www.volcengine.com/docs/6454/1536426#http-%E6%9C%8D%E5%8A%A1%E5%99%A8)。 |`xxxxxxxxxx` |
|Url |String |否 |表示 HTTP 伺服器的存取點、連接埠以及日誌存放的路徑。連接埠是可選的。存取點必須以 `http://` 或者 `https://` 開頭，長度不能超過 1,024 個字元。 |`https://www.example.com:8080/cdn-logs` |
|SampleRate |Double |否 |表示日誌採樣率，範圍為 0.00 \- 100.00，精確到 2 位小數。<br><br>採樣率指的是投遞的日誌比例。例如，您設定採樣率為 10，則意味著在 CDN 節點上每採集 100 條日誌，CDN 會隨機選擇 10 條日誌投遞到您指定的位置。 |`50.55` |
|Sls |Object |否 |當 `TaskType` 為 `sls` 時，該結構體表示 SLS 側的相應配置。 | |
|AccessKeyId |String |否 |表示您阿里雲帳號的 AccessKey ID，長度不能超過 128 個字元。 |`xxxxxxxxxxxx` |
|AccessKeySecret |String |否 |表示您阿里雲帳號的 AccessKey Secret，長度不能超過 128 個字元。 |`xxxxxxxxx` |
|Endpoint |String |否 |表示 `Project` 的公網網域。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |否 |表示儲存日誌的 LogStore。 |`myStore` |
|Project |String |否 |表示 `LogStore` 所屬的日誌專案。該專案在 `Endpoint` 所對應的投遞地域下。 |`myProject` |
|Tls |Object |否 |當 `TaskType` 為 `tls` 時，該結構體表示 TLS 側的相應配置。 | |
|Endpoint |String |否 |表示 `Project` 的公網網域。該參數有以下取值，與 `Region` 的取值對應。<br><br><br>* `tls-cn-beijing.volces.com`<br><br>* `tls-cn-shanghai.volces.com`<br><br>* `tls-cn-guangzhou.volces.com`<br><br>* `tls-cn-hongkong.volces.com`<br><br>* `tls-ap-southeast-1.volces.com`<br><br>* `tls-ap-southeast-3.volces.com` |`tls-ap-southeast-1.volces.com` |
|ProjectID |String |否 |表示日誌主題所屬的日誌專案 ID。該專案在 `Endpoint` 所對應的投遞地域下。 |`a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747` |
|TopicName |String |否 |表示儲存日誌的日誌主題的名稱。如果該日誌主題不存在，CDN 會建立該主題。該參數的輸入要求如下：<br><br><br>* 長度為 3～64 個字元。<br><br>* 只能包含中文、小寫字母、數字、底線（_）和連字號（\-）。<br><br>* 不能以底線（_）或連字號（\-）開頭或結尾。<br><br>* 不能以 `tls_`、`tos_`、`tls-`、`volc_` 開頭。<br><br><br>说明<br><br>如果該日誌主題已在其他投遞任務中指定，您無法指定該日誌主題。<br><br>您可以呼叫 ListRealtimeLogDeliveryTask 判斷某個日誌主題是否已被其他任務指定。 |`test_topic` |
|Ttl |Long |否 |表示日誌的儲存時長，範圍為 1 \- 3649，單位是天。<br><br>如果您輸入 `3650`，表示日誌將永久保存。 |`3` |
|Splunk |Object |否 |當 `TaskType` 為 `splunk` 時，該結構體表示 Splunk 側的相應配置。 | |
|CompressType |String |否 |表示在 CDN 日誌投遞時，是否啟用 Gzip 壓縮。該參數有以下取值：<br><br><br>* `true`：表示啟用 Gzip 壓縮。<br><br>* `false`：表示不啟用 Gzip 壓縮。<br><br><br>該參數的預設值為 `false`。 |`true` |
|Token |String |是 |表示 HEC 鑑權 Token。 |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |是 |表示 HEC 介面位址。 |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |否 |當 `TaskType` 為 `bigquery` 時，該結構體表示 BigQuery 側的相應配置。<br><br>前提條件<br><br>在呼叫本 API 建立日誌投遞任務前，您必須先在 Google BigQuery 中建立目標資料表 (Table)，並為該表配置能夠接收 CDN 即時日誌標準欄位的表 Schema。<br><br>**配置方法**：在 BigQuery 主控台建立資料表時，請在 **Schema** 配置區域中，開啟 **Edit as text** 模式，然後將附件中的 JSON 程式碼貼至文字方塊中，以產生正確的表 Schema。<br><br> | |
|Authentication |String |否 |Google Cloud 服務帳號 (Service Account) 的 JSON 格式金鑰。該金鑰包含身分認證資訊，用於授權 BytePlus CDN 存取您的 BigQuery 資源並串流寫入日誌。<br><br>说明<br><br>您需要將 GCP JSON 金鑰檔案中的內容序列化為一個完整的單行字串作為 `Authentication` 參數的值，處理規則如下：<br><br><br>* 將 JSON 檔案中的所有雙引號 `"` 轉換為 `\"` 。<br><br>* 將換行符號轉換為 `\n`。 |`參見下方範例` |
|DatasetID |String |否 |您在 BigQuery 中建立的資料集 (Dataset) ID。 |`my_dataset` |
|ProjectID |String |否 |BigQuery 所在的 GCP 專案 (Project) ID。 |`my-project` |
|TableID |String |否 |您在 BigQuery 中建立的資料表 (Table) ID。 |`my_table` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|TaskID |String |表示任務的 ID。 |`b23298e8-c262-4cb6-8138-2c311230b972` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

**投遞目標為 HTTP 伺服器**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Domain": "img.example.com",
    "Desc": "mydesc",
    "HttpServer": {
        "Url": "http://www.example.com:8000/mylogs",
        "AuthMechanism": true,
        "SecretKey": "xxxxxxxxxx",
        "CompressType": "gzip",
        "RequestHeader": [
            {
                "key": "header1",
                "value": "value1"
            },
            {
                "key": "header2",
                "value": "value2"
            }
        ]
    },
    "SampleRate": 50.55,
    "TaskType": "http_server"
}
```


**投遞目標為 TLS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Desc": "myDesc",
    "Domain": "www.example.com,img.example.com",
    "SampleRate": 100,
    "TaskType": "tls",
    "Tls": {
        "Endpoint": "tls-ap-southeast-1.volces.com`",
        "ProjectID": "a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747",
        "TopicName": "topic2",
        "Ttl": 7
    }
}
```


**投遞目標為 SLS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Desc": "myDesc",
    "Domain": "www.example.com",
    "SampleRate": 100,
    "Sls": {
        "AccessKeyId": "xxxxxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxxxxxxx",
        "Endpoint": "ap-southeast-1.log.aliyuncs.com",
        "LogStore": "my_store",
        "Project": "my_project"
    },
    "TaskType": "sls"
}
```


**投遞目標為 Splunk**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Desc": "myDesc",
    "Domain": "www.example.com",
    "SampleRate": 100,
    "Splunk": {
        "Url": "https://192.168.1.100:8088/services/collector",
        "Token": "B5A79AAD-D822-46CC-80D1-819F80D7BFB0",
        "CompressType": "true"
    },
    "TaskType": "splunk"
}
```


**投遞目標為 BigQuery**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
  "Area": "outside_chinese_mainland",
  "Domain": "www.example.com",
  "TaskType": "bigquery",
  "Desc": "Test",
  "SampleRate": 100,
  "BigQuery": {
    "ProjectID": "your-project-id",
    "Authentication": "{\n  \"type\": \"service_account\",\n  \"project_id\": \"your-project-id\",\n  \"private_key_id\": \"your_private_key_id\",\n  \"private_key\": \"-----BEGIN PRIVATE KEY-----\\nYOUR_PRIVATE_KEY_CONTENT_HERE\\n-----END PRIVATE KEY-----\\n\",\n  \"client_email\": \"your-service-account@your-project-id.iam.gserviceaccount.com\",\n  \"client_id\": \"123456789012345678901\",\n  \"auth_uri\": \"https://accounts.google.com/o/oauth2/auth\",\n  \"token_uri\": \"https://oauth2.googleapis.com/token\",\n  \"auth_provider_x509_cert_url\": \"https://www.googleapis.com/oauth2/v1/certs\",\n  \"client_x509_cert_url\": \"https://www.googleapis.com/robot/v1/metadata/x509/your-service-account%40your-project-id.iam.gserviceaccount.com\",\n  \"universe_domain\": \"googleapis.com\"\n}",
    "DatasetID": "cdn_logs_dataset",
    "TableID": "access_logs"
  }
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20251030172232277BC0277930A92087E9",
        "Action": "CreateRealtimeLogDeliveryTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972"
    }
}
```


&nbsp;
