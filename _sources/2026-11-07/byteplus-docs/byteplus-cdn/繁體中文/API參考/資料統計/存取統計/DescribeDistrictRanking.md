---
title: "DescribeDistrictRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeDistrictRanking_zh-tw"
---

<span id="api-說明"></span>
## API 說明

基於 CDN 收到的使用者請求，該 API 按分組對一系列的指標資料進行彙總，並對這些彙總資料按從大到小排序。分組條件包括國家和地區、中國省級行政區和中國網路營運商。

要呼叫該 API，您需要指定一個指標，一個分組條件，一個統計時間段和一個時間粒度。您還可以指定多個過濾條件對使用者請求進行過濾。您最多能查詢過去 92 天的資料。

資料穩定性：受網路波動影響，邊緣伺服器上統計的指標資料可能會發生變化。大多數情況下，指標資料會在 12 小時內逐步穩定下來。

資料時效性：指標資料可能會有 5 分鐘左右的延遲。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您是剛開始使用資料統計的 API，請務必先閱讀以下文件，這將有助於您理解該 API 文件。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw">統計時間段說明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition_zh-tw">指標的定義以及統計方式</a></div>



<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeDistrictRanking&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeDistrictRanking`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Item |String |是 |表示一個分組條件，用於對 `Metric` 資料進行彙總。該參數有以下取值：<br><br><br>* `location`：表示使用者請求來自的國家和地區。<br><br>* `province`：表示使用者請求來自的中國省級行政區。<br><br>* `isp`：表示使用者請求使用的中國網路營運商。<br><br><br>當 `Item` 是 `province` 或 `isp` 時，`Metric` 資料是基於來自中國的請求而統計的。 |`location` |
|Metric |String |是 |表示一個指標。該參數有以下取值：<br><br><br>* `in_traffic`：表示使用者向 CDN 傳輸的資料量，單位是 bytes。<br><br>* `in_bandwidth`：表示基於使用者向 CDN 傳輸的資料量而計算的頻寬峰值，單位是 bps。<br><br>* `out_traffic`：表示 CDN 向使用者傳輸的資料量，單位是 bytes。<br><br>* `out_bandwidth`：表示基於 CDN 向使用者傳輸的資料量而計算的頻寬峰值，單位是 bps。<br><br>* `requests`：表示 CDN 收到的使用者請求的數量。<br><br>* `dynamic_requests`：對於 CDN 收到的使用者請求，該指標表示滿足以下所有條件的使用者請求數量。<br><br>   * 請求方法既不是 GET，也不是 HEAD。<br><br>   * CDN 的回應狀態碼不是 405。<br><br>* `static_requests`：對於 CDN 收到的使用者請求，該指標表示滿足以下所有條件的使用者請求數量。<br><br>   * 請求方法是 GET 或者 HEAD。<br><br>   * CDN 的回應狀態碼不是 405。<br><br><br>關於每個指標的詳情以及統計方式，參見 [指標的定義以及統計方式](https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition_zh-tw)。 |`traffic` |
|EndTime |Long |是 |表示統計時間段的結束時間，格式是 Unix 時間戳，精度是秒。 |`1710836303` |
|StartTime |Long |是 |表示統計時間段的開始時間，格式是 Unix 時間戳，精度是秒。`StartTime` 必須早於或者等於 `EndTime`。同時，`StartTime` 和 `EndTime` 所表示的統計時間段不能超過 31 天。 |`1710259200` |
|Domain |String |否 |表示一個或多個網域名稱，用於對使用者請求進行過濾。該 API 對您指定的每個網域名稱統計 `Metric` 資料。您最多可以指定 50 個網域名稱。多個網域名稱之間使用逗號（,）分隔。如果不指定 `Domain`，表示不使用該參數對請求進行過濾。<br><br>如果您指定了 `Project`，您指定的網域名稱必須是屬於該 `Project` 的。<br><br>说明<br><br>當子使用者呼叫該 API 時，請留意以下說明：<br><br><br>* 子使用者只能指定其有權限存取的網域名稱。子使用者可以呼叫 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplateDomains_zh-tw) 獲取其有權限存取的網域名稱。<br><br>* 如果不指定該參數，表示所有該子使用者有權限存取的那些網域名稱。 |`www.example.com,www.test.com,img.example.com` |
|Interval |String |否 |表示一個時間粒度。該 API 基於 `Interval` 將 `StartTime` 和 `EndTime` 所表示的統計時間段拆分成一系列的時間區間，然後對每個時間區間統計 `Metric` 資料。<br><br>關於 `Interval` 參數是如何用來拆分統計時間段，參考 [統計時間段說明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw)。<br><br>該參數有以下取值：<br><br><br>* `1min`：表示時間粒度是 1 分鐘。<br><br>* `5min`：表示時間粒度是 5 分鐘。<br><br><br>您可以指定的時間粒度受 `StartTime` 和 `EndTime` 所表示的時間範圍的影響。<br><br><br>* 如果時間範圍 <= 1 天，您可以指定的時間粒度有 `1min`、`5min`。<br><br>* 如果 1 天 < 時間範圍 <= 31 天，您可以指定的時間粒度只能是 `5min`。<br><br><br>該參數的預設值是 `5min`。如果預設值不匹配時間範圍，API 請求會失敗。 |`5min` |
|Project |String |否 |表示一個專案。<br><br><br>* 如果您指定了 `Domain`，該 API 對所有您指定的網域名稱統計 `Metric` 資料。<br><br>* 如果您指定了 `Project` ，但未指定 `Domain`，該 API 對您指定的專案統計 `Metric` 資料。參見 [專案資料是如何統計的](https://docs.byteplus.com/en/docs/18/36659#%E5%B0%88%E6%A1%88%E8%B3%87%E6%96%99%E6%98%AF%E5%A6%82%E4%BD%95%E7%B5%B1%E8%A8%88%E7%9A%84)。<br><br>* 如果您既未指定 `Project` ，也未指定 `Domain`，該 API 對所有網域名稱統計 `Metric` 資料。 |`my_project` |
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
|Item |String |表示請求參數 `Item` 所指定的分組條件。 |`location` |
|TopDataDetails |Object[] |表示該 API 返回的結果資料。 | |
|Metric |String |表示請求參數 `Metric` 所指定的指標。 |`traffic` |
|ValueDetails |Object[] |表示一組資料物件，包含由 `Item` 彙總的 `Metric` 資料的詳情。這些資料物件按照 `Value` 從大到小排序。 | |
|ItemKey |String |表示屬於 `Item` 的一個值。<br><br><br>* 當 `Item` 是 `location` 時，`ItemKey` 是一個國家或地區的代碼。<br><br>* 當 `Item` 是 `isp` 時，`ItemKey` 是一個中國營運商的代碼。<br><br>* 當 `Item` 是 `province` 時，`ItemKey` 是一個中國省級行政區的代碼。<br><br><br>您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 獲取代碼與對應實體的對應表。 |`CHN` |
|Ratio |Double |表示該 `ItemKey` 的 `Value` 在所有 `ItemKey` 的 `Value` 總和中的占比。<br><br>需要留意的是，當 `Metric` 是 `bandwidth` 時，該參數無效，其值始終是 `0`。 |`0.9527` |
|Timestamp |Long |表示 `Value` 的時間點，單位是 Unix 時間戳，精度是秒。該參數僅當 `Metric` 是 `bandwidth` 時才有效，表示頻寬峰值的時間。如果 `Metric` 不是 `bandwidth`，該參數無效，其值始終是 `0`。 |`1710419700` |
|Value |Double |表示該 `ItemKey` 的彙總 `Metric` 資料。 |`95270` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDistrictRanking&Version=2021-03-01
{
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "5min",
    "Metric": "out_traffic",
    "Item": "location",
    "Project": "my_project",
    "Domain": "www.example.com,www.test.com,img.example.com"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202404230647543E4BBB2C9D0C1FB4346B",
        "Action": "DescribeDistrictRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "location",
        "TopDataDetails": [
            {
                "Metric": "out_traffic",
                "ValueDetails": [
                    {
                        "ItemKey": "USA",
                        "Ratio": 0.5199,
                        "Timestamp": 0,
                        "Value": 196605899287.6
                    },
                    {
                        "ItemKey": "BRA",
                        "Ratio": 0.181,
                        "Timestamp": 0,
                        "Value": 68452858987.7
                    },
                    {
                        "ItemKey": "OTHERS",
                        "Ratio": 0.0008,
                        "Timestamp": 0,
                        "Value": 296736667.7
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
