---
title: "DescribeUserData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeUserData_zh-tw"
---

<span id="api-說明"></span>
## API 說明

基於 CDN 收到的使用者請求，該 API 統計各時間點的獨立客戶端 IP 位址數量。

要呼叫該 API，您需要指定一個網域名稱、一個統計時間段和一個時間粒度。您還可以指定多個過濾條件對使用者請求進行過濾。您最多能查詢過去 92 天的資料。

資料穩定性：受網路波動影響，邊緣伺服器上統計的指標資料可能會發生變化。大多數情況下，指標資料會在 12 小時內逐步穩定下來。

資料時效性：獨立訪客數量是基於按小時粒度統計的指標資料。因此，資料統計可能會有 2 小時左右的延遲。例如，對於 09:00 至 10:00 這個時間段的獨立訪客數量，您可以在 11:00 左右獲取到準確的結果。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您是剛開始使用資料統計的 API，請務必先閱讀以下文件，這將有助於您理解該 API 文件。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw">統計時間段說明</a></div>



<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeUserData&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeUserData`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示一個網域名稱，用於對使用者請求進行過濾。<br><br>说明<br><br>當子帳號呼叫該 API 時，請留意以下說明：<br><br><br>* 子帳號可以指定的網域名稱是該子帳號有權限存取的那些網域名稱。子帳號可以呼叫 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplateDomains_zh-tw) 獲取其有權限存取的網域名稱。 |`www.example.com` |
|EndTime |Long |是 |表示統計時間段的結束時間，格式是 Unix 時間戳，精度是秒。 |`1710836303` |
|Interval |String |是 |表示一個時間粒度。該 API 基於 `Interval` 將 `StartTime` 和 `EndTime` 所表示的統計時間段拆分成一系列的時間區間，然後對每個時間區間統計獨立客戶端 IP 位址數量。<br><br>關於 `Interva`參數是如何用來拆分統計時間段，參考 [統計時間段說明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw)。<br><br>該參數有以下取值：<br><br><br>* `hour`：表示時間粒度是 1 小時。<br><br>* `day`：表示時間粒度是 1 天。 |`hour` |
|StartTime |Long |是 |表示統計時間段的開始時間，格式是 Unix 時間戳，精度是秒。`StartTime` 必須早於或者等於 `EndTime`。同時，`StartTime` 與 `EndTime` 所表示的統計時間段不能超過 31 天。 |`1710259200` |
|IpVersion |String |否 |表示請求使用的一個網路層協議，用於對使用者請求進行過濾。該參數的可用值如下：<br><br><br>* `IPv4`：表示 IPv4 協議。<br><br>* `IPv6`：表示 IPv6 協議。<br><br><br>如果不指定 `IpVersion`，表示不使用該參數對請求進行過濾。 |`IPv4` |
|Location |String |否 |表示一個國家或地區的代碼，用於對使用者請求進行過濾。CDN 對來自這些國家和地區的使用者請求統計客戶端 IP 位址的數量。<br><br><br>* 如果您指定了 `Location`，就不能指定 `Province`，反之亦然。<br><br>* 如果您不指定 `Location`，表示不使用該參數對請求進行過濾。<br><br><br>您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 獲取代碼與國家和地區的對應表。 |`AZE` |
|Province |String |否 |表示一個中國省級行政區的代碼，用於對使用者請求進行過濾。CDN 對來自這些省級行政區的使用者請求統計客戶端 IP 位址的數量。<br><br>如果您不指定 `Province`，表示不使用該參數對請求進行過濾。<br><br>您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 獲取代碼與中國省級行政區的對應表。 |`AH` |
|TimeZone |String |否 |指定一个时区参数。 | |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|MetricDataList |Object[] |表示一組資料物件，包含每個時間點的獨立客戶端 IP 位址數量。 | |
|TimeStamp |Long |表示一個時間點，格式時 Unix 時間戳，精度是秒。參見 [統計時間段說明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw)。 |`1710950400` |
|Value |Double |表示該 `TimeStamp` 時間點的獨立客戶端 IP 位址數量。該資料的時區是 UTC+08:00。 |`42` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeUserData&Version=2021-03-01
{
    "Domain": "www.example.com",
    "StartTime": 1710950400,
    "EndTime": 1710998170,
    "Interval": "hour",
    "IpVersion": "IPv4",
    "Province": "AH"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202403220141458C564C77FA147001D2E1",
        "Action": "DescribeUserData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "TimeStamp": 1710950400,
                "Value": 421
            },
            {
                "TimeStamp": 1710954000,
                "Value": 428
            },
            {
                "TimeStamp": 1710957600,
                "Value": 439
            },
            {
                "TimeStamp": 1710961200,
                "Value": 436
            },
            {
                "TimeStamp": 1710964800,
                "Value": 435
            },
            {
                "TimeStamp": 1710968400,
                "Value": 446
            },
            {
                "TimeStamp": 1710972000,
                "Value": 433
            },
            {
                "TimeStamp": 1710975600,
                "Value": 430
            },
            {
                "TimeStamp": 1710979200,
                "Value": 428
            },
            {
                "TimeStamp": 1710982800,
                "Value": 412
            },
            {
                "TimeStamp": 1710986400,
                "Value": 423
            },
            {
                "TimeStamp": 1710990000,
                "Value": 417
            },
            {
                "TimeStamp": 1710993600,
                "Value": 394
            },
            {
                "TimeStamp": 1710997200,
                "Value": 407
            }
        ]
    }
}
```


&nbsp;
