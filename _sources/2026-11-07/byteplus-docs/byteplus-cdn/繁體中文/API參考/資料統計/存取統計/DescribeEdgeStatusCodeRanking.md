---
title: "DescribeEdgeStatusCodeRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeEdgeStatusCodeRanking_zh-tw"
---

<span id="api-說明"></span>
## API 說明

基於 CDN 收到的使用者請求，該 API 按網域名稱對一系列的指標資料進行彙總，並對這些彙總資料按從大到小排序。

要呼叫該 API，您需要指定一個狀態碼指標，一個統計時間段和一個時間粒度。您還可以指定多個過濾條件對使用者請求進行過濾。您最多能查詢過去 92 天的資料。

資料穩定性：受網路波動影響，邊緣伺服器上統計的指標資料可能會發生變化。大多數情況下，指標資料會在 12 小時內逐步穩定下來。

資料時效性：指標資料可能會有 5 分鐘左右的延遲。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您是剛開始使用資料統計的 API，請務必先閱讀以下文件，這將有助於您理解該 API 文件。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw">統計時間段說明</a></div>



<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeEdgeStatusCodeRanking&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeEdgeStatusCodeRanking`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Item |String |是 |表示一個分組條件。當前，該參數值只能是 `domain`，表示按 `Domain` 對 `Metric` 資料進行彙總。 |`domain` |
|Metric |String |是 |對於 CDN 對使用者請求的回應，該參數表示以下某個類別的狀態碼數量：<br><br><br>* `status_2xx`：表示 2xx 狀態碼數量。<br><br>* `status_3xx`：表示 3xx 狀態碼數量。<br><br>* `status_4xx`：表示 4xx 狀態碼數量。<br><br>* `status_5xx`：表示 5xx 狀態碼數量。 |`status_4xx` |
|EndTime |Long |是 |表示統計時間段的結束時間，格式是 Unix 時間戳，精度是秒。 |`1710836303` |
|StartTime |Long |是 |表示統計時間段的開始時間，格式是 Unix 時間戳，精度是秒。`StartTime` 必須早於或者等於 `EndTime`。同時，`StartTime` 和 `EndTime` 所表示的統計時間段不能超過 31 天。 |`1710259200` |
|Domain |String |否 |表示一個或多個網域名稱，用於對使用者請求進行過濾。該 API 對您指定的每個網域名稱統計 `Metric` 資料。您最多可以指定 50 個網域名稱。多個網域名稱之間使用逗號（,）分隔。如果不指定 `Domain`，表示不使用該參數對請求進行過濾。<br><br>如果您指定了 `Project`，您指定的網域名稱必須是屬於該 `Project` 的。<br><br>说明<br><br>當子使用者呼叫該 API 時，請留意以下說明：<br><br><br>* 子使用者只能指定其有權限存取的網域名稱。子使用者可以呼叫 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplateDomains_zh-tw) 獲取其有權限存取的網域名稱。<br><br>* 如果不指定該參數，表示所有該子使用者有權限存取的那些網域名稱。 |`www.example.com,www.test.com,img.example.com` |
|Interval |String |否 |表示一個時間粒度。該 API 基於 `Interval` 將 `StartTime` 和 `EndTime` 所表示的統計時間段拆分成一系列的時間區間，然後對每個時間區間統計 `Metric` 的資料。<br><br>關於 `Interval` 參數是如何用來拆分統計時間段，參考 [統計時間段說明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw)。<br><br>該參數有以下取值：<br><br><br>* `1min`：表示時間粒度是 1 分鐘。<br><br>* `5min`：表示時間粒度是 5 分鐘。<br><br><br>您可以指定的時間粒度受 `StartTime` 和 `EndTime` 所表示的時間範圍的影響。<br><br><br>* 如果時間範圍 <= 1 天，您可以指定的時間粒度有 `1min`、`5min`。<br><br>* 如果 1 天 < 時間範圍 <= 31 天，您可以指定的時間粒度有 `5min`。<br><br><br>該參數的預設值是 `5min`。如果預設值不匹配時間範圍，API 請求會失敗。 |`1min` |
|Project |String |否 |表示一個專案。<br><br><br>* 如果您指定了 `Domain`，該 API 對所有您指定的網域名稱統計 `Metric` 資料。<br><br>* 如果您指定了 `Project` ，但未指定 `Domain`，該 API 對您指定的專案統計 `Metric` 資料。參見 [專案資料是如何統計的](https://docs.byteplus.com/en/docs/18/36649#%E5%B0%88%E6%A1%88%E8%B3%87%E6%96%99%E6%98%AF%E5%A6%82%E4%BD%95%E7%B5%B1%E8%A8%88%E7%9A%84)。<br><br>* 如果您既未指定 `Project` ，也未指定 `Domain`，該 API 對所有網域名稱統計 `Metric` 資料。 |`my_project` |
|TimeZone |String |否 |表示 `Metric` 資料的時區。該參數有以下取值：<br><br><br>* `Etc/GMT`：表示的時區是 UTC+00:00。<br><br>* `Etc/GMT-1`、`Etc/GMT-2`、...、`Etc/GMT-12`：表示的時區分別是 UTC+01:00、UTC+02:00、...、UTC+12:00。<br><br>* `Etc/GMT+1`、`Etc/GMT+2`、...、`Etc/GMT+12`：表示的時區分別是 UTC\-01:00、UTC\-02:00、...、UTC\-12:00。<br><br><br>該參數的預設值是 `Etc/GMT-8`。 |`Etc/GMT-8` |


<span id="專案資料是如何統計的"></span>
### 專案資料是如何統計的

在對一個專案統計指標資料時，CDN 統計的是專案內網域名稱的資料。


* 如果統計時間段內有一個網域名稱轉出該專案，該專案的指標資料不會包含轉出後該網域名稱的資料。

* 如果統計時間段內有一個網域名稱轉入該專案，該專案的指標資料會包含轉入後該網域名稱的資料。


**示例**

考慮以下場景：


* 您指定的統計時間段是某天的 8:00\-10:00。

* 網域名稱X 在 9:00 從另一個專案轉移到專案A。網域名稱Y 一直在專案A 中。


在這個場景中，如果您對專案A 統計指標資料，則指標資料涵蓋：


* 網域名稱X 在 9:00 至 10:00 之間的指標資料。

* 網域名稱Y 在 8:00 至 10:00 之間的指標資料。


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Item |String |表示請求參數 `Item` 所指定的分組條件。 |`domain` |
|Metric |String |表示請求參數 `Metric` 所指定的指標。 |`status_4xx` |
|TopDataDetails |Object[] |表示一組資料物件，包含由 `Item` 彙總的 `Metric` 資料的詳情。每個資料物件包含每個類別下狀態碼的數量和占比。這些資料物件按指定的 `Metric` 從大到小排序。 | |
|ItemKey |String |表示 `Domain` 列表中的一個網域名稱。 |`www.example.com` |
|Status2xx |Double |表示對於該 `ItemKey`，2xx 狀態碼的數量。 |`45678` |
|Status2xxRatio |Double |表示對於該 `ItemKey`，2xx 狀態碼的數量占比。 |`0.47` |
|Status3xx |Double |表示對於該 `ItemKey`，3xx 狀態碼的數量。 |`0` |
|Status3xxRatio |Double |表示對於該 `ItemKey`，3xx 狀態碼的數量占比。 |`0` |
|Status4xx |Double |表示對於該 `ItemKey`，4xx 狀態碼的數量。 |`3` |
|Status4xxRatio |Double |表示對於該 `ItemKey`，4xx 狀態碼的數量占比。 |`0.0001` |
|Status5xx |Double |表示對於該 `ItemKey`，5xx 狀態碼的數量。 |`0` |
|Status5xxRatio |Double |表示對於該 `ItemKey`，5xx 狀態碼的數量占比。 |`0` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeEdgeStatusCodeRanking&Version=2021-03-01
{
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Metric": "status_2xx",
    "Item": "domain",
    "Project": "my_project",
    "Domain": "www.example.com,www.test.com,img.example.com"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20240319234228A07998A9B5FFC309EB82",
        "Action": "DescribeEdgeStatusCodeRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "domain",
        "Metric": "status_2xx",
        "TopDataDetails": [
            {
                "ItemKey": "img.example.com.com",
                "Status2xx": 22428898,
                "Status2xxRatio": 0.61,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 333,
                "Status4xxRatio": 0.0001,
                "Status5xx": 34,
                "Status5xxRatio": 0
            },
            {
                "ItemKey": "www.test.com",
                "Status2xx": 9470608,
                "Status2xxRatio": 0.37,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 2380317,
                "Status4xxRatio": 0.6019,
                "Status5xx": 324607,
                "Status5xxRatio": 0.0109
            },
            {
                "ItemKey": "www.example.com",
                "Status2xx": 3069749,
                "Status2xxRatio": 0.02,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 7,
                "Status4xxRatio": 0,
                "Status5xx": 0,
                "Status5xxRatio": 0
            }
        ]
    }
}
```


&nbsp;
