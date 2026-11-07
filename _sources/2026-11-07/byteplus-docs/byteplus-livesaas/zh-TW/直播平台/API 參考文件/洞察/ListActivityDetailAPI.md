---
title: "ListActivityDetailAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivitydetailapi-zh-TW"
---

呼叫此 API 以取得關鍵指標，例如特定直播間在指定時間範圍內的總直播時長、平均觀看時長、唯一觀眾（UV）及最高同時在線人數（PCU）。

<span id="0d7f64af"></span>
## 要求


* 配額：每個帳戶每分鐘 100 次查詢

* 資料延遲：5 分鐘


<span id="f713d23f"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=ListActivityDetailAPI&Version=2020-06-01`

* 方法：GET


<span id="3442b2a9"></span>
## 請求參數

下列表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="0a89855a"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`ListActivityDetailAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="0aee7785"></span>
### Body


|名稱 |資料型別 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|PageNumber |Integer |否 |`1` |要返回的頁碼。<br><br>預設值：`1`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此 API 操作最多支持返回 10,000 個結果，這表示 <code>PageNumber</code> × <code>PageSize</code> 必須小於或等於 10,000。</div><br> |
|PageSize |Integer |否 |`10` |每頁返回的結果數量。<br><br>預設值：`10`。<br><br>值範圍：[1,100]<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此 API 操作最多支持返回 10,000 個結果，這表示 <code>PageNumber</code> × <code>PageSize</code> 必須小於或等於 10,000。</div><br> |
|SortMode |String |否 |`desc` |排序方式。<br><br>預設值：`desc`。<br><br>有效值：<br><br><br>* `asc`：升序排列。<br><br>* `desc`：降序排列。 |
|SortField |String |否 |`LiveTime` |指定排序資料的維度。<br><br>預設值：`LiveTime`。<br><br>有效值：<br><br><br>* `LiveTime`：直播間的直播時間，可能不是直播實際開始的時間。<br><br>* `LiveDuration`：直播間的總直播時長。<br><br>* `PCU`：直播間的最高同時在線人數。<br><br>* `UV`：直播間的唯一觀眾或訪客數。<br><br>* `PV`：直播間的總觀看或訪問次數。<br><br>* `CommentCount`：直播間的評論數。<br><br>* `WatchDurationPerPeople`：直播間的平均觀看或訪問時長。 |
|ActivityName |String |否 |`直播間 A` |篩選名稱包含此值的直播間。 |
|StartLiveTime |Long |是 |`1692339016` |時間範圍的起始時間，Unix 時間戳格式。單位：秒。<br><br>將返回此時間範圍內的資料。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">時間範圍不可超過 365 天（31,536,000 秒）。</div><br> |
|EndLiveTime |Long |是 |`1700115016` |時間範圍的結束時間，Unix 時間戳格式。單位：秒。<br><br>將返回此時間範圍內的資料。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">時間範圍不可超過 365 天（31,536,000 秒）。</div><br> |
|PlayStatus |Integer |是 |`11` |指定要返回哪些資料。有效值：<br><br><br>* `1`：返回直播間處於「直播」狀態時產生的資料。<br><br>* `2`：返回直播間處於「預覽」狀態時產生的資料，即使觀看頁面未播放預覽。<br><br>* `3`：返回直播間處於「回放」狀態時產生的資料，即使觀看頁面未播放回放。<br><br>* `10`：當您的直播間處於 **直播**、**預覽**、**回放**或 **結束** 狀態時產生的資料將被返回，即使觀看頁面未播放預覽或回放。<br><br>* `11`：當您的直播間處於 **直播**、**預覽**或 **回放** 狀態時產生的資料將被返回，即使觀看頁面未播放預覽或回放。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若值為 <code>1</code>、 <code>2</code>、 <code>3</code>或 <code>11</code>，則返回總瀏覽量、唯一觀看者數、平均觀看時長及總觀看時長。若值為 <code>10</code>，則返回總訪問量、唯一訪客數、平均訪問時長及總訪問時長。</div><br> |


<span id="c24c437f"></span>
## 回應參數


|名稱 |資料型別 |範例值 |描述 |
|---|---|---|---|
|PageNumber |Integer |`1` |返回的頁碼。 |
|PageSize |Integer |`10` |每頁返回的結果數量。 |
|總數 |Integer |`1` |找到的符合條件的結果總數。 |
|活動列表 |陣列[活動列表](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi-zh-TW#305f7323) |`-` |返回的直播間資料。 |


<span id="305f7323"></span>
### 活動列表


|名稱 |資料型別 |範例值 |描述 |
|---|---|---|---|
|活動 ID |Long |`17218346****` |直播間的活動 ID。 |
|活動名稱 |String |`直播間 A` |直播間名稱。 |
|直播時間 |Long |`1692559016` |直播預定開始時間，Unix 時間戳格式。單位：秒。<br><br>此時間可能與實際開始時間不同。 |
|直播時長 |Long |`899` |直播總時長。單位：秒。 |
|PV |Long |`412` |總瀏覽量或訪問量。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若觀眾或訪客刷新觀看頁面一次，瀏覽量或訪問量會增加 1。</div><br> |
|UV |Long |`286` |唯一觀看者或訪客數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">具有相同設備 ID 的設備視為同一設備，使用同一設備的觀眾或訪客僅計為一人。</div><br> |
|PCU |Long |`47` |同時在線人數峰值。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">具有相同設備 ID 的設備視為同一設備，使用同一設備的訪客僅計為一人。</div><br> |
|評論數 |Long |`403` |直播間內由主播、觀眾及嘉賓發送的評論數，包括已刪除評論及審核中的評論。 |
|人均觀看時長 |Long |`476` |平均觀看或訪問時長。單位：分鐘。 |
|總觀看時長 |Long |`800` |總觀看或訪問時長。單位：分鐘。 |


<span id="c97117a2"></span>
## 範例

<span id="38c2a2ea"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListActivityDetailAPI&Version=2020-06-01&StartLiveTime=1692339016&EndLiveTime=1700115016
```


<span id="ae83324e"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "Action": "ListActivityDetailAPI",
        "Region": "ap-singapore-1",
        "RequestId": "202201201826170101501312091D1C09D2",
        "Service": "livesaas",
        "SystemTime": 1700125016,
        "Version": "2020-06-01"
    },
    "Result": {
        "Activities": [
          {
            "ActivityId": 17218346****,
            "ActivityName": "Live room A",
            "LiveTime": 1692559016,
            "LiveDuration": 899,
            "PV": 412,
            "UV": 286,
            "PCU": 47,
            "WatchDurationPerPeople": 476,
            "ViewDurationTotal": 800,
            "CommentCount": 403
          }
        ],
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1
  }
}
```


<span id="fa56be7f"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
