---
title: "SubmitRefreshTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-SubmitRefreshTask_zh-tw"
---

在 BytePlus CDN 中提交一個清除快取任務。如果在任務中指定檔案 URL，CDN 執行任務時會刪除這些檔案。如果在任務中指定目錄，CDN 預設會標記這些目錄中的檔案為過期。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

預設情況下，每個 BytePlus 主帳號的清除快取額度如下：


* 每天最多清除快取 10,000 個 URL。

* 每天最多清除快取 50 個目錄。

* 每個任務可以包含最多 100 個 URL 或 50 個目錄。


<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=SubmitRefreshTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `SubmitRefreshTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Type |String |否 |表示一個清除快取類型。該參數有以下取值：<br><br><br>* `file`：表示 URL 清除快取，對一個或者多個檔案執行清除快取操作。<br><br>* `dir`：表示目錄清除快取，對一個或者多個目錄下的所有檔案，包括子目錄下的檔案執行清除快取操作。<br><br>* `regex`：表示正規表示式清除快取。指定一個或多個正規表示式，對與正規表示式相符的檔案 URL 執行清除快取操作。若要使用正規表示式清除快取，請 [提交工單](https://console.byteplus.com/workorder/create)。關於正規表示式清除快取的介紹和 URL 規範，參見 [正規表示式清除快取](https://docs.byteplus.com/en/docs/byteplus-cdn/purge-cache_zh-tw#%E8%A6%8F%E5%89%87%E9%81%8B%E7%AE%97%E5%BC%8F%E6%B8%85%E9%99%A4%E5%BF%AB%E5%8F%96)。<br><br><br>該參數的預設值為 `file`。 |`file` |
|Prefix |Boolean |否 |表示是否使用前綴清除快取。該參數僅當 `Type` 是 `dir` 時有效，有以下取值：<br><br><br>* `true`：表示使用前綴清除快取，對以指定前綴開頭的目錄下的所有檔案執行清除快取操作。<br><br>* `false`：表示不使用前綴清除快取。<br><br><br>該參數的預設值是 `false`。 |`true` |
|UrlList |String[] |否 |表示一個待清除快取的 URL 清單。每個 URL 必須以 `http://` 或 `https://` 開頭。<br><br><br>* 當 `Type` 是 `file` 時，您指定的是檔案 URL。<br><br>* 當 `Type` 是 `dir` 時，<br><br>   * 如果 `Prefix` 是 `false`，您指定的是以 `/` 結尾的目錄，例如 `http://www.example.com/image/`。<br><br>   * 如果 `Prefix` 是 `true`，您指定的是目錄前綴。例如 `http://www.example.com/im` 可以匹配 `http://www.example.com/image/` 與 `http://www.example.com/ime/` 這兩個目錄。<br><br>* 當 `Type` 是 `regex` 時，您指定的是用來匹配檔案 URL 的正規表示式。參見 [正規表示式清除快取](https://docs.byteplus.com/en/docs/byteplus-cdn/purge-cache_zh-tw#%E8%A6%8F%E5%89%87%E9%81%8B%E7%AE%97%E5%BC%8F%E6%B8%85%E9%99%A4%E5%BF%AB%E5%8F%96)。要指定該參數值，請 [提交工單](https://console.byteplus.com/workorder/create)。<br><br><br>说明<br><br>您不能直接對泛網域下的檔案和目錄執行清除快取操作，而是要對每個子網域進行這些操作。 |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|Delete |Boolean |否 |表示是否從快取中刪除 `Urls` 指定的檔案。該參數僅當 `Type` 是 `dir` 時有效。要使用該參數，請 [提交工單](https://console.byteplus.com/workorder/create)。<br><br>該參數有以下取值：<br><br><br>* `true`：表示刪除這些檔案。之後，如果收到了這些檔案的請求，CDN 會向來源伺服器請求這些檔案。<br><br>* `false`：表示不刪除這些檔案，僅標記這些檔案為已過期。之後，如果收到了這些檔案的請求，CDN 會執行 [源伺服器請求驗證](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules_zh-tw#%E4%BE%86%E6%BA%90%E4%BC%BA%E6%9C%8D%E5%99%A8%E6%A0%A1%E9%A9%97)。<br><br><br>該參數的預設值是 `false`。 |`false` |
|Urls |String |否 |**不建議**使用該參數，請使用 `UrlList` 代替。<br><br>該參數的作用與 `UrlList` 相同。在 `Urls` 中指定多個 URL 時，URL 之間必須以 `\n` 分隔。<br><br>如果您同時指定了 `UrlList` 和 `Urls` ，僅 `UrlList` 生效。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |
|RequestHeaderInstances |Object[] |否 |指定待清除快取檔案在快取鍵中必須包含的請求頭。只有當快取檔案的快取鍵中完全包含了此處指定的請求頭時，該檔案才會被比對並清除快取。<br><br>列表中最多包含 10 個請求頭。 | |
|Key |String |否 |表示列表中一個請求頭的名稱。名稱有以下要求：<br><br><br>* 名稱不能是 `User-Agent`。<br><br>* 名稱不能以 `x-bdcdn-` 或者 `Volc-Cdn` 開頭。<br><br>* 名稱不能超過 1,024 個字元。 |`header1` |
|Value |String |否 |表示該請求頭的值，長度不能超過 1,024 個字元。 |`value1` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|TaskID |String |表示該任務的 ID。您可以呼叫 [DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeContentTasks_zh-tw) 查看 `Urls` 列表中每個物件的清除快取結果。 |`refresh_url_bbd36e1cb5154f52b648b07ee119223e2971399f5a1075c0` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=SubmitRefreshTask&Version=2021-03-01
{
    "Type": "file",
    "UrlList": [
        "https://www.example.com/1.txt",
        "https://www.example.com/2.txt"
    ],
    "RequestHeaderInstances": [
        {
            "Key": "header1",
            "Value": "value1"
        },
        {
            "Key": "header2",
            "Value": "value2"
        }
    ]
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202201141648440102100180260E003ABA",
        "Action": "SubmitRefreshTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "refresh_url_bbd36e1cb5154f52b648b07ee119223e2971399f5a1075c0"
    }
}
```


&nbsp;
