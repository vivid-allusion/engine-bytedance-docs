---
title: "DescribeContentTasks"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeContentTasks_zh-tw"
---

取得過去 7 天內提交的清除快取和預取任務，細分到這些任務中的每個 URL。返回結果展示了每個任務的詳細資訊，包括任務的執行結果。您可以使用多個過濾選項對任務清單進行過濾。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeContentTasks&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeContentTasks`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|UrlList |String[] |否 |表示一個 URL 清單，用於對查詢結果進行過濾，以取得清單中每個任務詳細資訊。每個 URL 都必須以 `http://` 或 `https://` 開頭。<br><br>該參數是一個字串陣列。<br><br>如果您同時指定了 `Url`，則 `Url` 不生效。 |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|DomainName |String |否 |表示一個網域名稱，用於對查詢結果進行過濾，以取得 URL 中包含該網域名稱的任務。 |`www.example.com` |
|TaskID |String |否 |表示一個任務 ID，用以取得該 ID 的所有任務。 |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |
|TaskType |String |是 |表示一個任務類型，用於對查詢結果進行過濾，以取得該類型任務。該參數的可用值如下：<br><br><br>* `refresh_file`：表示 URL 清除快取任務。<br><br>* `refresh_dir`：表示目錄清除快取任務。<br><br>* `preload`：表示 URL 預取任務。<br><br>* `refresh_regex`：表示正規表示式清除快取任務。 |`preload` |
|Status |String |否 |表示一個任務狀態，用於對查詢結果進行過濾，以取得該狀態下任務。該參數的可用值如下：<br><br><br>* `complete`：表示已完成的任務。<br><br>* `running`：表示執行中的任務。<br><br>* `failed`：表示執行失敗的任務。<br><br><br>如果不指定該參數，則表示不使用該參數對任務清單進行過濾。 |`complete` |
|StartTime |Long |否 |表示一個開始時間，格式是 Unix 時間戳記，以取得提交時間晚於或等於該時間的任務。需要留意的是，您無法查詢 7 天前提交的任務。<br><br>您必須同時指定 `StartTime` 和 `EndTime`，或者兩個參數都不指定。如果兩個參數都不指定，則取得過去 7 天內提交的任務。 |`1641844915` |
|EndTime |Long |否 |表示一個結束時間，格式是 Unix 時間戳記，以取得提交時間早於或等於該時間的任務。 |`1641845373` |
|PageNum |Long |否 |表示一個頁碼，用以取得該頁面上的任務。該參數的預設值為 `1`。<br><br>CDN 對符合過濾條件的任務進行分頁。您可以根據回應本文中的 `Total` 和 `PageSize` 參數的值計算頁數。 |`1` |
|PageSize |Long |否 |表示每頁包含的任務數量。該參數的取值範圍是 1\-1000，預設值是 `50`。 |`10` |
|Url |String |否 |**不建議**使用該參數，請使用 `UrlList` 代替。<br><br>該參數的作用與 `UrlList` 相同。在 `Urls` 中指定多個 URL 時，URL 之間必須以 `\n` 分隔。<br><br>如果您同時指定了 `UrlList` 和 `Urls`，僅 `UrlList` 生效。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Total |Long |表示符合過濾條件的任務總數。 |`2` |
|PageNum |Long |表示請求本文中的 `PageNum`。 |`1` |
|PageSize |Long |表示請求本文中的 `PageSize`。 |`100` |
|Data |Object[] |表示 `PageNum` 上的 URL 任務列表。如果 `PageNum` 所表示頁碼不存在或者該頁上沒有任務，該參數值為 `null`。 | |
|Url |String |表示清單中一個任務所操作的 URL。 |`https://www.example.com/1.jpg` |
|Status |String |表示該任務的狀態。該參數有以下取值：<br><br><br>* `complete`：表示任務已完成。<br><br>* `running`：表示任務正在執行中。<br><br>* `failed`：表示任務執行失敗。 |`complete` |
|TaskType |String |表示該任務的類型。該參數有以下取值：<br><br><br>* `refresh_file`：表示 URL 清除快取任務。<br><br>* `refresh_dir`：表示目錄清除快取任務。<br><br>* `preload`：表示 URL 預取任務。<br><br>* `refresh_regex`：表示正規表示式清除快取任務。 |`preload` |
|RefreshPrefix |Boolean |表示該任務中是否有 "前綴清除快取" 這個配置。僅當 `TaskType` 是 `refresh_dir` 時，該參數有效。該參數有以下取值：<br><br><br>* `true`：表示該任務中有這個配置。<br><br>* `false`：表示該任務中沒有這個配置。<br><br><br>如果 `TaskType` 不是 `refresh_dir`，該參數值始終是 `false`。 |`true` |
|CreateTime |Long |表示該任務的提交時間，格式是 Unix 時間戳記。 |`1601371409` |
|TaskID |String |表示該任務的 ID。 |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |
|Process |String |表示該任務的進度，以百分比表示。 |`70%` |
|Delete |Boolean |表示該任務是否指定了刪除快取中的檔案。該參數僅當 `TaskType` 是 `refresh_dir` 時有效。該參數有以下取值：<br><br><br>* `true`：表示刪除快取中的檔案。<br><br>* `false`：表示不刪除快取中的檔案，僅標記這些檔案為過期。<br><br><br>當 `TaskType` 不是 `refresh_dir` 時，`Delete` 的值始終是 `false`。 |`false` |
|Remark |String |表示該 URL 任務失敗的原因。該參數僅當 `Status` 是 `failed` 時有效。如果 `Status` 不是 `failed`，`Remark` 的值始終是空（""）。 |`origin_error` |
|StatusCode |Long |* 如果 `Remark` 不是空（""），該參數值表示來源伺服器的回應狀態碼。狀態碼為 4xx 或者 5xx。<br><br>* 如果 `Remark` 是空（""），該參數不會出現。 | |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeContentTasks&Version=2021-03-01
{
    "StartTime": 1625587200,
    "EndTime": 1625673600,
    "TaskType": "preload",
    "PageSize": 10,
    "PageNum": 1
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202406301133492C6A5B1ABB315058A120",
        "Action": "DescribeContentTasks",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "CreateTime": 1719738505,
                "Process": "100%",
                "Remark": "origin_error",
                "Status": "failed",
                "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871",
                "TaskType": "preload",
                "Url": "https://www.example.com/2.txt"
            },
            {
                "CreateTime": 1719738505,
                "Process": "100%",
                "Remark": "",
                "Status": "complete",
                "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871",
                "TaskType": "preload",
                "Url": "https://www.example.com/1.txt"
            }
        ],
        "PageNum": 1,
        "PageSize": 50,
        "Total": 2
    }
}
```


&nbsp;
