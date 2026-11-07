---
title: "SubmitPreloadTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SubmitPreloadTask_zh-tw"
---

在 BytePlus CDN 中提交一個預取任務，將一個或者多個檔案提前快取到 CDN 的快取節點。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

預設情況下，每個 BytePlus 主帳號的任務額度如下：


* 每天最多預取 1,000 個 URL。

* 每個任務最多預取 100 個 URL。


<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=SubmitPreloadTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `SubmitPreloadTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|UrlList |String[] |否 |表示一個或多個檔案 URL。CDN 將這些檔案提前快取到快取節點。<br><br>说明<br><br>URL 中不能包含萬用網域名稱。如果您需要為一個萬用網域名稱下的多個子網域名稱提交一個預取任務，您必須對每個子網域名稱指定需要預取的那些 URL。 |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|Area |String |否 |表示一個加速區域。CDN 將 `Urls` 中的每個檔案提前快取到該區域下的那些快取節點。該參數有以下取值：<br><br><br>* `chinese_mainland`：表示中國內地。<br><br>* `outside_chinese_mainland`：表示全球，但不包含中國內地。<br><br>* `global`：表示全球。<br><br><br>如果不指定該參數，對於 `Urls` 中一個 URL，這個加速區域就是該 URL 所含網域名稱的加速區域。 |`outside_chinese_mainland` |
|ConcurrentLimit |Long |否 |表示 CDN 在執行預取任務時，每次向来源伺服器請求的最大檔案數量。預設值是 `10`，該參數的取值範圍是 1\-1000。 |`20` |
|Urls |String |否 |**不建議**使用該參數，請使用 `UrlList` 代替。<br><br>該參數的作用與 `UrlList` 相同。在 `Urls` 中指定多個 URL 時，URL 之間必須以 `\n` 分隔。<br><br>如果您同時指定了 `UrlList` 和 `Urls` ，僅 `UrlList` 生效。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|TaskID |String |表示該任務的 ID。您可以呼叫 [DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeContentTasks_zh-tw) 查看 `Urls` 中每個 URL 的預取結果。 |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=SubmitPreloadTask&Version=2021-03-01
{
    "UrlList": [
        "https://www.example.com/1.jpg",
        "https://www.example.com/2.jpg"
    ]
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202406300908245F2C63BC765D774F1CB0",
        "Action": "SubmitPreloadTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871"
    }
}
```


&nbsp;
