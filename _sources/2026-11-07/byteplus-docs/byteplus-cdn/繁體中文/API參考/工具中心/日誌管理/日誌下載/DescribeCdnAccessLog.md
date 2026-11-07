---
title: "DescribeCdnAccessLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnAccessLog_zh-tw"
---

獲取指定網域名稱的訪問日誌。該 API 返回的是這些訪問日誌的下載 URL。BytePLus CDN 按小時在整點對訪問日誌進行打包。

資料保留期限：在呼叫該 API 時，建議您指定時間段的時間跨度不超過 30 天，否則可能由於日誌數量龐大導致 API 呼叫超時。

日誌延遲：CDN 預設以每小時為單位，在整點對過去一小時內收集到的日誌進行打包，產生日誌包。日誌包大約在產生後的 3 小時可以被下載。由於網路延遲等因素，CDN 收集到的日誌可能會有最長 24 小時的延遲。對於收集到的延遲日誌，CDN 會將其追加到相對應的日誌包中。因此，日誌包在產生後的 24 小時內可能會有日誌的追加。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 XX 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeCdnAccessLog&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeCdnAccessLog`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示一個網域名稱。該 API 獲取的是該網域名稱的訪問日誌。 |`www.example.com` |
|ServiceRegion |String |否 |表示一個服務區域，用於對訪問日誌進行過濾。該參數有以下取值：<br><br><br>* `chinese_mainland`：表示 **中國大陸**。<br><br>* `global`：表示 **全球**。<br><br>* `outside_chinese_mainland`：表示 **全球（不包含中國大陸）** 。<br><br><br>該參數的預設值是 `global`。 |`global` |
|StartTime |Long |是 |表示日誌統計時間段的開始時間，時間格式是 Unix 時間戳。需要留意的是，`StartTime` 並非日誌統計時間段的實際開始時間。<br><br>實際開始時間為 `StartTime` 在小時粒度的向後取整。<br><br>例子：<br><br><br>* 您指定的 `StartTime` 所表示的時間是 15:07。則實際開始時間是 16:00。<br><br>* 您指定的 `StartTime` 所表示的時間是 15:00。則實際開始時間是 15:00。 |`1641844915` |
|EndTime |Long |是 |表示日誌統計時間段的結束時間，時間格式是 Unix 時間戳。需要留意的是，`EndTime` 並非日誌統計時間段的實際結束時間。<br><br>實際結束時間為 `EndTime` 在小時粒度的向後取整。 |`1641953589` |
|PageNum |Long |否 |表示一個頁碼。該 API 返回的是該頁碼所指定的分頁上的那些日誌包。<br><br>該 API 返回的日誌包是根據 `PageSize` 而分頁的。假設該 API 返回的日誌包數量是 100，您指定的 `PageSize` 是 `10`，那麼返回的日誌包是分布在 10 個頁上。如果您指定的 `PageNum` 是 `2`，表示獲取第 2 頁上的那些日誌包。<br><br>如果您指定的分頁上沒有日誌包，則返回結果中 `DomainLogDetails` 參數的值為 `null`。<br><br>`PageNum` 的預設值是 `1`。 |`1` |
|PageSize |Long |否 |表示每個分頁包含的日誌包數量。<br><br>該參數的取值範圍是 1\-100，預設值是 `10`。 |`1` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Domain |String |表示請求參數中的 `Domain`。 |`www.a.com` |
|PageSize |Long |表示請求參數中的 `PageSize`。 |`100` |
|PageNum |Long |表示請求參數中的 `PageNum`。 |`1` |
|TotalCount |Long |表示符合過濾條件的日誌包數量。 |`100` |
|DomainLogDetails |Object[] |表示該 API 返回的日誌包列表。 | |
|LogName |String |表示列表中一個日誌包的名稱。名稱的命名規範是 <*Domain*\>_<*Start_Time*\>_<*End_Time*\>.gz。<br><br>说明<br><br>在日誌包名稱中，`Start_Time` 和 `End_Time` 的時區是 UTC+08:00。 |`www.example.com_20210707100000_20210707110000.gz` |
|StartTime |Long |表示該日誌包所對應的日誌統計時間段的實際開始時間，格式是 Unix 時間戳。<br><br>`StartTime` 與 `EndTime` 之間的時間間隔是 1 小時。 |`1642392000` |
|EndTime |Long |表示該日誌包所對應的日誌統計時間段的實際結束時間，格式是 Unix 時間戳。 |`1642395600` |
|LogPath |String |表示日誌包的下載 URL。下載 URL 的有效期為 24 小時。 |`URL1` |
|LogSize |Long |表示日誌包的大小，單位為 `bytes`。<br><br>说明<br><br>由於日誌包在產生後的 24 小時內可能會有延遲日誌追加，每次呼叫該 API 取得的日誌包大小可能會有變化。請以最新取得的日誌包大小為準。 |`9107` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnAccessLog&Version=2021-03-01
{
    "PageSize": 10,
    "PageNum": 1,
    "Domain": "www.example.com",
    "StartTime": 1672963200,
    "EndTime": 1672990980,
    "ServiceRegion": "global"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202406031008365F2C63BC765D774E4A8C",
        "Action": "DescribeCdnAccessLog",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore"
    },
    "Result": {
        "Domain": "perfops2.byte-test.com",
        "DomainLogDetails": [
            {
                "EndTime": 1717401600,
                "LogName": "www.example.com_20240603150000_20240603160000_outsideChineseMainland.gz",
                "LogPath": "URL1",
                "LogSize": 4009503,
                "StartTime": 1717398000
            },
            {
                "EndTime": 1717398000,
                "LogName": "www.example.com_20240603140000_20240603150000.gz",
                "LogPath": "URL2",
                "LogSize": 849,
                "StartTime": 1717394400
            },
            {
                "EndTime": 1717398000,
                "LogName": "www.example.com_20240603140000_20240603150000_outsideChineseMainland.gz",
                "LogPath": "URL3",
                "LogSize": 3616460,
                "StartTime": 1717394400
            },
            {
                "EndTime": 1717394400,
                "LogName": "www.example.com_20240603130000_20240603140000.gz",
                "LogPath": "URL4",
                "LogSize": 1163,
                "StartTime": 1717390800
            },
            {
                "EndTime": 1717394400,
                "LogName": "www.example.com_20240603130000_20240603140000_outsideChineseMainland.gz",
                "LogPath": "URL5",
                "LogSize": 2958868,
                "StartTime": 1717390800
            },
            {
                "EndTime": 1717390800,
                "LogName": "www.example.com_20240603120000_20240603130000.gz",
                "LogPath": "URL6",
                "LogSize": 269,
                "StartTime": 1717387200
            },
            {
                "EndTime": 1717390800,
                "LogName": "www.example.com_20240603120000_20240603130000_outsideChineseMainland.gz",
                "LogPath": "URL7",
                "LogSize": 2630368,
                "StartTime": 1717387200
            },
            {
                "EndTime": 1717387200,
                "LogName": "www.example.com_20240603110000_20240603120000_outsideChineseMainland.gz",
                "LogPath": "URL8",
                "LogSize": 2584924,
                "StartTime": 1717383600
            },
            {
                "EndTime": 1717383600,
                "LogName": "www.example.com_20240603100000_20240603110000_outsideChineseMainland.gz",
                "LogPath": "URL9",
                "LogSize": 3587479,
                "StartTime": 1717380000
            },
            {
                "EndTime": 1717380000,
                "LogName": "www.example.com_20240603090000_20240603100000.gz",
                "LogPath": "URL10",
                "LogSize": 592,
                "StartTime": 1717376400
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "TotalCount": 50
    }
}
```


&nbsp;
