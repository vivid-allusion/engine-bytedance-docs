---
title: "DescribeDistrictData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeDistrictData_zh-tw"
---

<span id="api-說明"></span>
## API 說明

基於 CDN 收到的使用者請求，該 API 對一個指標統計各時間點的指標細分資料。

要呼叫該 API，您需要指定一個指標，一個統計時間段和一個時間粒度。您還可以指定多個過濾條件對使用者請求進行過濾。您最多能查詢過去 92 天的資料。

資料穩定性：受網路波動影響，邊緣伺服器上統計的指標資料可能會發生變化。大多數情況下，指標資料會在 12 小時內逐步穩定下來。因此，該 API 傳回的網域指標資料並非帳單中顯示的用量，僅供參考。實際用量請以帳單為準。

資料時效性：指標資料可能會有 5 分鐘左右的延遲。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您剛接觸 CDN 的統計 API，請務必先閱讀以下文件，這將有助於您理解該 API 文件。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw">統計時間段說明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition_zh-tw">指標的定義以及統計方式</a></div>



<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeDistrictData&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeDistrictData`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Metric |String |是 |表示一個指標。該參數有以下取值：<br><br><br>* `in_traffic`：表示使用者向 CDN 傳輸的資料量，單位是 bytes。<br><br>* `in_bandwidth`：表示基於使用者向 CDN 傳輸的資料量而計算的頻寬，單位是 bps。<br><br>* `out_traffic`：表示 CDN 向使用者傳輸的資料量，單位是 bytes。<br><br>* `out_bandwidth`：表示基於 CDN 向使用者傳輸的資料量而計算的頻寬，單位是 bps。<br><br>* `requests`：表示 CDN 收到的所有使用者請求的數量。<br><br>* `dynamic_requests`：對於 CDN 收到的使用者請求，該指標表示滿足以下所有條件的使用者請求數量。<br><br>   * 請求方法既不是 GET，也不是 HEAD。<br><br>   * CDN 的回應狀態碼不是 405。<br><br>* `static_requests`：對於 CDN 收到的使用者請求，該指標表示滿足以下所有條件的使用者請求數量。<br><br>   * 請求方法是 GET 或者 HEAD。<br><br>   * CDN 的回應狀態碼不是 405。<br><br>* `qps`：表示 CDN 收到的使用者請求的 QPS。<br><br>* `response_time`：表示 CDN 回應使用者請求所耗費的平均時間，單位是毫秒（ms）。<br><br>* `avg_speed`：表示 CDN 在回應使用者請求時的平均資料傳輸速度，單位是 Bps。該指標的資料是對回應狀態碼是 2xx 的使用者請求統計的。<br><br>* `status_all`：在 CDN 對使用者請求的回應中，該參數表示以下類別的狀態碼數量：<br><br>   * 所有狀態碼的數量。<br><br>   * 2xx 狀態碼的數量。<br><br>   * 3xx 狀態碼的數量。<br><br>   * 4xx 狀態碼的數量。<br><br>   * 5xx 狀態碼的數量。<br><br>   * 每個狀態碼的數量。<br><br>* `status_2xx`：表示 2xx 狀態碼的數量以及該類別下每個狀態碼的數量。<br><br>* `status_3xx`：表示 3xx 狀態碼的數量以及該類別下每個狀態碼的數量。<br><br>* `status_4xx`：表示 4xx 狀態碼的數量以及該類別下每個狀態碼的數量。<br><br>* `status_5xx`：表示 5xx 狀態碼的數量以及該類別下每個狀態碼的數量。<br><br><br>關於每個指標的詳情以及統計方式，參見 [指標的定義以及統計方式](https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition_zh-tw)。<br><br>说明<br><br>如果您指定 `Metric` 為 `response_time` 或者 `avg_speed`，請務必指定 `Protocol`。參見 `Protocol` 參數的描述。 |`traffic` |
|StartTime |Long |是 |表示統計時間段的開始時間，格式是 Unix 時間戳，精度是秒。`StartTime` 必須早於或者等於 `EndTime`。同時，`StartTime` 與 `EndTime` 所表示的統計時間段不能超過 31 天。 |`1710259200` |
|EndTime |Long |是 |表示統計時間段的結束時間，格式是 Unix 時間戳，精度是秒。 |`1710836303` |
|Interval |String |否 |表示一個時間粒度。該 API 基於 `Interval` 將 `StartTime` 和 `EndTime` 所表示的統計時間段拆分成一系列的時間區間，然後對每個時間區間統計 `Metric` 資料。<br><br>關於 `Interval` 參數是如何用來拆分統計時間段，參考 [統計時間段說明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw)。<br><br>該參數有以下取值：<br><br><br>* `1min`：表示時間粒度是 1 分鐘。<br><br>* `5min`：表示時間粒度是 5 分鐘。<br><br>* `hour`：表示時間粒度是 1 小時。<br><br>* `day`：表示時間粒度是 1 天。<br><br><br>您可以指定的時間粒度受 `StartTime` 和 `EndTime` 所表示的時間範圍的影響。<br><br><br>* 如果時間範圍 <= 1 天，您可以指定的時間粒度包含 `1min`、`5min`、`hour`。<br><br>* 如果 1 天 < 時間範圍 <= 3 天，您可以指定的時間粒度包含 `5min`、`hour`、`day`。<br><br>* 如果 3 天 < 時間範圍 <= 31 天，您可以指定的時間粒度包含 `hour`、`day`。<br><br><br>該參數的預設值是 `5min`。如果預設值不匹配時間範圍，API 請求會失敗。 |`hour` |
|Project |String |否 |表示一個專案。<br><br><br>* 如果您指定了 `Domain`，該 API 對所有您指定的網域名稱統計 `Metric` 資料。<br><br>* 如果您指定了 `Project` ，但未指定 `Domain`，該 API 對您指定的專案統計 `Metric` 資料。參見 [專案資料是如何統計的](https://docs.byteplus.com/en/docs/18/36658#%E5%B0%88%E6%A1%88%E8%B3%87%E6%96%99%E6%98%AF%E5%A6%82%E4%BD%95%E7%B5%B1%E8%A8%88%E7%9A%84)。<br><br>* 如果您既未指定 `Project` ，也未指定 `Domain`，該 API 對所有網域名稱統計 `Metric` 資料。 |`my_project` |
|Domain |String |否 |表示一個或多個網域名稱，用於對使用者請求進行過濾。該 API 對您指定的每個網域名稱統計 `Metric` 資料。您最多可以指定 50 個網域名稱。多個網域名稱之間使用逗號（,）分隔。如果不指定 `Domain`，表示不使用該參數對請求進行過濾。<br><br>如果您指定了 `Project`，您指定的網域名稱必須是屬於該 `Project` 的。<br><br>说明<br><br>當子使用者呼叫該 API 時，請留意以下說明：<br><br><br>* 子使用者只能指定其有權限存取的網域名稱。子使用者可以呼叫 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplateDomains_zh-tw) 獲取其有權限存取的網域名稱。<br><br>* 如果不指定該參數，表示所有該子使用者有權限存取的那些網域名稱。 |`www.example.com,www.test.com,img.example.com` |
|Location |String |否 |表示國家和地區的代碼，用於對使用者請求進行過濾。您可以指定一個或者多個代碼，CDN 對來自這些國家和地區的使用者請求統計 `Metric` 資料。多個國家和地區代碼之間使用逗號（,）分隔。您最多可以指定 30 個國家和地區。<br><br><br>* 如果您指定了 `Location`，就不能指定 `Province`，反之亦然。<br><br>* 如果您不指定 `Location`，表示不使用該參數對請求進行過濾。<br><br><br>您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 獲取代碼與國家和地區的對應表。 |`CHN,AZE` |
|Province |String |否 |表示中國省級行政區的代碼，用於對使用者請求進行過濾。您可以指定一個或者多個代碼，CDN 對來自這些省級行政區的使用者請求統計 `Metric` 資料。多個代碼之間使用逗號（,）分隔。您最多可以指定 10 個代碼。<br><br>如果您不指定 `Province`，表示不使用該參數對請求進行過濾。<br><br>您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 獲取代碼與中國省級行政區的對應表。 |`AH,BJ,CQ,FJ` |
|Isp |String |否 |表示請求所使用的中國網路營運商的代碼，用於對使用者請求進行過濾。例如，`CT` 表示中國電信。您可以指定一個或者多個代碼，CDN 對使用這些網路營運商的使用者請求統計 `Metric` 資料。多個代碼之間使用逗號（,）分隔。您最多可以指定 5 個代碼。<br><br><br>* 當 `Location` 是 `CHN` 或者您指定了 `Province` 時，您才能指定 `Isp`。<br><br>* 當您不指定 `Isp` 時，表示不使用該參數對請求進行過濾。<br><br><br>您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 獲取代碼與網路營運商的對應表。 |`CT,CM,CU,GWBN` |
|Protocol |String |否 |表示請求使用的一個應用層協議，用於對使用者請求進行過濾。該參數的可用值如下：<br><br><br>* `http`：表示 HTTP 協議。<br><br>* `https`：表示 HTTPS 協議。<br><br>* `quic`：表示 QUIC 協議。<br><br>* `websocket`：表示 WebSocket 協議。<br><br>* `non-websocket`：表示 HTTP 協議， HTTPS 協議和 QUIC 協議。<br><br><br>如果不指定 `Protocol`，表示不使用該參數對請求進行過濾。<br><br>说明<br><br>如果 `Metric` 是 `response_time` 或者 `avg_speed`，請指定 `Protocol` 以過濾掉 WebSocket 協議。因為對於 WebSocket 請求，這兩個指標的資料不準確。 |`https` |
|IpVersion |String |否 |表示請求使用的一個網路層協議，用於對使用者請求進行過濾。該參數的可用值如下：<br><br><br>* `IPv4`：表示 IPv4 協議。<br><br>* `IPv6`：表示 IPv6 協議。<br><br><br>如果不指定 `IpVersion`，表示不使用該參數對請求進行過濾。 |`IPv4` |
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
|MetricDataList |Object[] |表示該 API 返回的結果資料。 | |
|Metric |String |表示請求參數 `Metric` 所指定的指標。 |`traffic` |
|Values |Object[] |表示基於 `Interval` 統計出的一組 `Metric` 資料物件。 | |
|TimeStamp |Long |表示 `Value` 所對應的時間區間的開始時間，格式是 Unix 時間戳，精度是秒。參見 [統計時間段說明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-tw). |`1710273600` |
|Value |Double |表示一個 `Metric` 細分資料。 |`4567` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDistrictData&Version=2021-03-01
{
    "Domain": "www.example.com,www.test.com,img.example.com",
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "day",
    "IpVersion": "IPv4",
    "Isp": "CT,CM,CU,GWBN",
    "Metric": "out_traffic",
    "Project": "my_project",
    "Protocol": "https",
    "Province": "AH,BJ,CQ,FJ"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2024031916110305F6D27733C2CA667E04",
        "Action": "DescribeDistrictData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "Metric": "out_traffic",
                "Values": [
                    {
                        "TimeStamp": 1710201600,
                        "Value": 31667254.3
                    },
                    {
                        "TimeStamp": 1710288000,
                        "Value": 35425907
                    },
                    {
                        "TimeStamp": 1710374400,
                        "Value": 33508322.1
                    },
                    {
                        "TimeStamp": 1710460800,
                        "Value": 29844611.5
                    },
                    {
                        "TimeStamp": 1710547200,
                        "Value": 19993227.1
                    },
                    {
                        "TimeStamp": 1710633600,
                        "Value": 19567554.6
                    },
                    {
                        "TimeStamp": 1710720000,
                        "Value": 32469929.8
                    },
                    {
                        "TimeStamp": 1710806400,
                        "Value": 30702487.2
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
