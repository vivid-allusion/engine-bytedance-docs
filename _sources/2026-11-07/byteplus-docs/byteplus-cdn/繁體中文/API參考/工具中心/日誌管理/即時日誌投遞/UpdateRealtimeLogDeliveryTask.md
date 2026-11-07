---
title: "UpdateRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRealtimeLogDeliveryTask_zh-tw"
---

修改一個即時日誌投遞任務的配置。

在呼叫該 API 時，


* 您需要指定 `HttpServer`、`Sls`、`Tls`、`Splunk`、`BigQuery` 這五個結構體中的一個。

* 如果某個參數未指定，該參數將被設定為預設值。


<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=UpdateRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `UpdateRealtimeLogDeliveryTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Area |String |是 |該參數值只能是 `chinese_mainland`，表示中國內地。 |`outside_chinese_mainland` |
|Domain |String |是 |表示該任務所關聯的網域列表。<br><br><br>* 如果您要關聯帳號下的所有網域，請傳入`*`。這裡，所有網域涵蓋您後續在 CDN 中新增的網域。<br><br>* 如果您要關聯指定的網域，請傳入待關聯的網域列表，列表中最多可以包含 200 個網域，多個網域之間以逗號（,）分隔。<br><br><br>注意<br><br>如果已存在關聯指定網域的其他任務，您無法指定 `Domain` 為 `*`。<br><br>您可以呼叫 ListRealtimeLogDeliveryTask 並指定該網域作為過濾條件，以查看該網域是否已與某個任務關聯。 |`www.example.com,img.example.com` |
|TaskID |String |是 |表示一個待修改任務的 ID。 |`b23298e8-c262-4cb6-8138-2c311230b972` |
|Desc |String |否 |表示任務的描述。該參數的輸入要求如下：<br><br><br>* 長度為 3 \- 64 個字元，可以包含中文、字母、數字、底線（_）和連字號（\-）。中文佔 3 個字元。<br><br>* 不能以連字號（\-）或底線（_）開頭或結尾。 |`newDesc` |
|HttpServer |Object |否 |當 `TaskType` 為 `http_server` 時，該結構體表示 HTTP 伺服器側的相應配置。<br><br>如果您指定了 `HttpServer`，對於該結構體下的參數，除了特別指明，必須都被指定。 | |
|AuthMechanism |Boolean |否 |表示 HTTP 伺服器是否啟用了鑑權。該參數有以下取值：<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |否 |表示在 CDN 投遞日誌時所啟用壓縮類型。該參數有以下取值：<br><br><br>* `gzip`：表示 Gzip 壓縮。<br><br><br>如果該參數不指定，表示不啟用壓縮。 |`gzip` |
|RequestHeader |Object[] |否 |表示 CDN 在向 HTTP 伺服器投遞日誌時，請求中需要額外包含的頭部列表。列表中最多可以包含 10 個頭部。<br><br>如果該參數不指定，表示請求中不添加額外的頭部。 | |
|Key |String |否 |表示列表中一個頭部的 Key，長度不能超過 1,024 個字元。`Key` 不能是 `User-Agent`，也不能以 `x-bdcdn-` 開頭 |`mykey` |
|Value |String |否 |表示 `Key` 的值，長度不能超過 1,024 個字元。 |`myvalue` |
|SecretKey |String |否 |表示鑑權 Key，用於計算權杖。該參數的長度為 6\-40 個字元。<br><br>如果 `AuthMechanism` 為 `true`，`SecretKey` 必須指定。<br><br>關於更多關於鑑權流程與權杖演算法的資訊，參見 [建立日誌投遞任務](https://www.volcengine.com/docs/6454/1536426#http-%E6%9C%8D%E5%8A%A1%E5%99%A8)。 |`xxxxxxxxx` |
|Url |String |否 |表示 HTTP 伺服器的存取點、連接埠以及日誌存放的路徑。連接埠是可選的。存取點必須以 `http://` 或者 `https://` 開頭，長度不能超過 1,024 個字元。 |`https://img.example.com:8090/cdn-logs` |
|SampleRate |Double |否 |表示日誌採樣率，範圍為 0.00 \- 100.00，精確到 2 位小數。<br><br>採樣率指的是投遞的日誌比例。例如，您設定採樣率為 10，則意味著在 CDN 節點上每採集 100 條日誌，CDN 會隨機選擇 10 條日誌投遞到您指定的位置。 |`70` |
|Sls |Object |否 |表示 SLS 側的相應配置。 | |
|AccessKeyId |String |否 |表示您阿里雲帳號的 AccessKey ID，長度不能超過 128 個字元。 |`xxxxxxxxxxxx` |
|AccessKeySecret |String |否 |表示您阿里雲帳號的 AccessKey Secret，長度不能超過 128 個字元。 |`xxxxxxxxx` |
|Endpoint |String |否 |表示 `Project` 的公網網域。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |否 |表示儲存日誌的 LogStore。 |`myStore` |
|Project |String |否 |表示 `LogStore` 所屬的日誌專案。該專案在 `Endpoint` 所對應的投遞地域下。 |`myProject` |
|Tls |Object |否 |表示 TLS 側的相應配置。 | |
|Ttl |Long |否 |表示日誌的儲存時長，範圍為 1 \- 3649，單位是天。<br><br>如果您輸入 `3650`，表示日誌將永久保存。 |`3` |
|Splunk |Object |否 |表示 Splunk 側的相應配置。 | |
|CompressType |String |否 |表示在 CDN 日誌投遞時，是否啟用 Gzip 壓縮。該參數有以下取值：<br><br><br>* `true`：表示啟用 Gzip 壓縮。<br><br>* `false`：表示不啟用 Gzip 壓縮。<br><br><br>該參數的預設值為 `false`。 |`true` |
|Token |String |是 |表示 HEC 鑑權 Token。 |`B5A79AAD-D822-46CC-80D1-819F80D7BFB0` |
|Url |String |是 |表示 HEC 介面位址。 |`https://192.168.1.100:8088/services/collector` |
|BigQuery |Object |否 |表示 BigQuery 側的相應配置。 | |
|Authentication |String |否 |Google Cloud 服務帳號 (Service Account) 的 JSON 格式金鑰。該金鑰包含身分認證資訊，用於授權 BytePlus CDN 存取您的 BigQuery 資源並串流寫入日誌。<br><br>说明<br><br>您需要將 GCP JSON 金鑰檔案中的內容序列化為一個完整的單行字串作為 `Authentication` 參數的值，處理規則如下：<br><br><br>* 將 JSON 檔案中的所有雙引號 `"` 轉換為 `\"` 。<br><br>* 將換行符號轉換為 `\n`。 | |
|DatasetID |String |否 |您在 BigQuery 中建立的資料集 (Dataset) ID。 |`my_dataset` |
|ProjectID |String |否 |BigQuery 所在的 GCP 專案 (Project) ID。 |`my-project` |
|TableID |String |否 |您在 BigQuery 中建立的資料表 (Table) ID。 |`my_table` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=UpdateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "TaskID": "6af98494-c4fd-4c1b-bc36-88c4de0b5b9e",
    "Domain": "www.example.com",
    "Sls": {
        "AccessKeyId": "yyyyyyyyyyyyyyyyyy",
        "AccessKeySecret": "yyyyyyyyyy",
        "Endpoint": "ap-southeast-1.log.aliyuncs.com",
        "LogStore": "my_store",
        "Project": "my_project"
    }
}
```


&nbsp;
