---
title: "DescribeStatisticalRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeStatisticalRanking_zh-tw"
---

<span id="api-說明"></span>
## API 說明

基於 CDN 收到的使用者請求，該 API 按熱門物件類型對一系列的指標資料進行彙總，並對這些彙總資料按從大到小排序，最後返回這些熱門物件。熱門物件類型包括請求客戶端所在的國家和地區、請求 URL、Referer 網域名稱、UA 字串中的物件、獨立客戶端 IP 位址的數量。

在呼叫該 API 時，您需要指定一個指標，一個熱門物件類型，一個統計時間段和一個時間粒度。您還可以指定多個過濾條件對使用者請求進行過濾。您最多能查詢過去 92 天的資料。

資料穩定性：受網路波動影響，邊緣伺服器上統計的指標資料可能會發生變化。大多數情況下，指標資料會在 12 小時內逐步穩定下來。

資料時效性：熱門物件是基於按小時粒度統計的指標資料。因此，資料統計可能會有 2 小時左右的延遲。例如，對於 09:00 至 10:00 這個時間段的熱門物件，您可以在 11:00 左右獲取到準確的結果。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeStatisticalRanking&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeStatisticalRanking`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示一個網域名稱，用於對使用者請求進行過濾。<br><br>说明<br><br>當子使用者呼叫該 API 時，請留意以下說明：<br><br><br>* 子使用者只能指定一個其有權限存取的網域名稱。子使用者可以呼叫 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplateDomains_zh-tw) 獲取其有權限存取的網域名稱。 |`www.example.com` |
|EndTime |Long |是 |表示統計時間段的結束時間，格式是 Unix 時間戳，精度是秒。 |`1710998170` |
|Item |String |是 |表示一個熱門物件的類型作為分組和排序條件。 該 API 按 `Item` 對 `Metric` 資料進行彙總並對這些彙總資料進行排序。該參數有以下取值：<br><br><br>* `region`：表示請求客戶端所在的國家或地區。<br><br>* `url`：表示請求 URL 中的路徑。<br><br>* `referer`：表示請求中的 `Referer` 網域名稱。<br><br>* `ua`：表示請求中的 `User-Agent` 字串。<br><br>* `clientip`：表示客戶端的 IP 位址。<br><br><br>说明<br><br><br>* 當 `Item` 是 `ua` 時，您還需要指定 `UaType` 作為一個補充分組條件。<br><br>* 當 `Item` 是 `region` 時，您還需要指定 `Area` 作為一個補充分組條件。 |`region` |
|Metric |String |是 |表示一個指標。該參數的可用值受 `Item` 的影響。<br><br><br>* 當 `Item` 是 `referer`、`ua` 或 `clientip` 時，該參數有以下取值：<br><br>   * `in_traffic`：表示使用者向 CDN 傳輸的資料量，單位是 bytes。<br><br>   * `out_traffic`：表示 CDN 向使用者傳輸的資料量，單位是 bytes。<br><br>   * `requests`：表示 CDN 收到的使用者請求的數量。<br><br>   * `dynamic_requests`：表示 CDN 收到的滿足以下所有條件的使用者請求數量。<br><br>      * 請求方法既不是 GET，也不是 HEAD。<br><br>      * CDN 的回應狀態碼不是 405。<br><br>   * `static_requests`：表示 CDN 收到的滿足以下所有條件的使用者請求數量。<br><br>      * 請求方法是 GET 或者 HEAD。<br><br>      * CDN 的回應狀態碼不是 405。<br><br>* 當 `Item` 是 `url` 時，該參數有以下取值：<br><br>   * `in_traffic`<br><br>   * `out_traffic`<br><br>   * `requests`<br><br>   * `dynamic_requests`<br><br>   * `static_requests`<br><br>   * `status_2xx`：在 CDN 對使用者請求的回應中，該參數表示 2xx 狀態碼的數量。<br><br>   * `status_3xx`：表示 3xx 狀態碼的數量。<br><br>   * `status_4xx`：表示 4xx 狀態碼的數量。<br><br>   * `status_5xx`：表示 5xx 狀態碼的數量。<br><br>* 當 `Item` 是 `region` 時，該參數有以下取值。<br><br>   * `clientip`：表示獨立客戶端 IP 位址的數量。<br><br>   當 `Item` 是 `region` 時，該參數有預設值 `clientip`，並且可以不指定。 |`traffic` |
|StartTime |Long |是 |表示統計時間段的開始時間，格式是 Unix 時間戳，精度是秒。`StartTime` 必須早於或者等於 `EndTime`。同時，`StartTime` 和 `EndTime` 所表示的統計時間段不能超過 31 天。<br><br>说明<br><br><br>* `StartTime` 和 `EndTime` 指定了統計時間段。但是實際統計時間段的開始時間和結束時間都是小時級別的。<br><br>   例子：`StarTime` 表示的時間是 15:07，`EndTime` 表示的時間是 15:21，那麼實際的統計時間段是 [15:00,16:00）。<br><br>   需要留意的是，如果 `EndTime` 正好是整點，則實際的統計時間段還要再往後延長 1 小時。假設 `StartTime` 表示的時間是 15:07，`EndTime` 表示的時間是 16:00，那麼實際的統計時間段是 [15:00,17:00)。 |`1710950400` |
|Area |String |否 |表示一個地域類型。該參數僅當 `Item` 是 `region` 時有效，作為一個補充分組條件，用於獲取客戶端 IP 位址數量的地區分布。該參數有以下取值：<br><br><br>* `Global`：表示全球國家和地區。<br><br>* `China`：表示中國省級行政區。<br><br><br>说明<br><br><br>* 如果您不指定 `Metric`，`Area` 可以不被指定。<br><br>   * 如果不指定 `Area`，該 API 將返回按國家、地區、中國省級行政區域分布的獨立客戶端 IP 位址數量。<br><br>* 如果您指定了 `Metric`，`Area` 必須指定。 |`global` |
|UaType |String |否 |表示 User\-Agent 字串中的一個物件類型。當 `Item` 是 `ua` 時，該參數必須指定，作為一個補充分組條件。當 `Item` 不是 `ua` 時，該參數無效。<br><br>該參數有以下取值：<br><br><br>* `browser`：表示 `User-Agent` 字串中的瀏覽器類型。<br><br>* `system`：表示 `User-Agent` 字串中的作業系統類型。<br><br>* `equipment`：表示 `User-Agent` 字串中客戶端設備的類型。 |`system` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Item |String |表示請求參數 `Item` 所指定的熱門物件類型。 |`region` |
|Metric |String |表示請求參數 `Metric` 所指定的指標。 |`traffic` |
|RankingDataList |Object[] |表示一組熱門物件詳情的列表。 | |
|ItemKey |String |表示一個熱門物件。<br><br><br>* 當 `Item` 是 `url` 時，該熱門物件是一個請求 URL 中的路徑。<br><br>* 當 `Item` 是 `referer` 時，該熱門物件是一個 `Referer` 網域名稱。<br><br>* 當 `Item` 是 `region` 時，該熱門物件是一個地區代碼。<br><br>* 當 `Item` 是 `clientip` 時，該熱門物件是一個國家，地區，或者中國省級行政區的代碼。<br><br>* 當 `Item` 是 `ua` 時，<br><br>   * 如果 `UaType` 是 `equipment`，該熱門物件是某種設備類型。<br><br>   * 如果 `UaType` 是 `system`，該熱門物件是某種作業系統。<br><br>   * 如果 `UaType` 是 `browser`，該熱門物件是某種瀏覽器。 |`GS` |
|ItemKeyCN |String |* 當 `Item` 是 `region` 和 `clientip` 時，`ItemKeyCN` 是 `ItemKey` 所對應地區的中文名稱。<br><br>* 當 `Item` 是 `url` 時，`ItemKeyCN` 是 `ItemKey` 所對應的路徑。<br><br>* 當 `Item` 是 `ua`、`referer`、`url` 或 `referer` 時，`ItemKeyCN` 與 `ItemKey` 相同。 |`甘肃` |
|Value |Double |表示該 `ItemKey` 的彙總 `Metric` 資料。`Value` 的時區是 UTC+08:00。 |`777` |
|UaType |String |表示請求參數中 `UaType` 所指定的物件類型。如果請求參數中不包含 `UaType`，該參數不會在返回結果中出現。 |`system` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeStatisticalRanking&Version=2021-03-01
{
    "Area": "Global",
    "Domain": "www.example.com",
    "StartTime": 1720614677,
    "EndTime": 1721478677,
    "Item": "region",
    "Metric": "clientip"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202407221231341976A83AF08B9822FD8F",
        "Action": "DescribeStatisticalRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "region",
        "Metric": "clientip",
        "RankingDataList": [
            {
                "ItemKey": "USA",
                "ItemKeyCN": "美国",
                "Value": 2857990
            },
            {
                "ItemKey": "IND",
                "ItemKeyCN": "印度",
                "Value": 744081
            },
            {
                "ItemKey": "BRA",
                "ItemKeyCN": "巴西",
                "Value": 695588
            },
            {
                "ItemKey": "FRA",
                "ItemKeyCN": "法国",
                "Value": 454253
            },
            ...
        ]
    }
}
```


&nbsp;
