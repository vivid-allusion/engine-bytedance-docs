---
title: "ListUserBehaviorDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listuserbehaviordataapi-zh-TW"
---

取得直播間的觀眾行為數據。您可以查詢過去 90 天的數據。

<span id="3ae19eb3"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="f60263b8"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=ListUserBehaviorDataAPI&Version=2020-06-01`

* 方法：GET


<span id="e0042409"></span>
## 請求參數

以下表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="2e36fb97"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`ListUserBehaviorDataAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218346****` |直播間的活動 ID。您可以透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|PageNo |Integer |否 |`1` |要返回的頁碼。<br><br>預設值：`1`。<br><br>若為滾動查詢，`PageNo` 的值可從 1 到 2^64。若非滾動查詢，API 最多可返回 10,000 筆結果，因此 `PageNo` 與 `PageItemCount` 的乘積不得超過 10,000。更多關於滾動查詢的資訊，請參見查詢參數 `ScrollId`。 |
|PageItemCount |Integer |否 |`10` |每頁返回的結果數。<br><br>預設值：`10`。<br><br>數值範圍：[1,500]。 |
|ScrollId |String |否 |`klTVnVZdFk3bWg4YVQwdwAAAAAASn****xybkZ1el` |滾動查詢 ID。<br><br>滾動查詢適用於需返回超過 10,000 筆結果的場景。執行滾動查詢時，請確保符合以下要求。<br><br><br>* 首次呼叫 API 時，請將 `ScrollId` 參數值設為空。第二次呼叫 API 時，請將參數值設為第一次呼叫返回的 `ScrollId` 值。第三次呼叫 API 時，請將參數值設為第二次呼叫返回的 `ScrollId` 值，依此類推。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若 <code>IsMerge</code> 或 <code>IsMergeUserId</code> 的值設為 <code>1</code>，則進行滾動查詢時 <code>ScrollId</code> 的值必須始終為空。   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">回應中的 <code>ScrollId</code> 值在 API 呼叫後 20 分鐘會失效，屆時無法再用該值進行下一次滾動查詢。   </div><br>   <br><br>* 首次呼叫 API 時，請將 `PageNo` 參數值設為 `1`，第二次呼叫設為 `2`，依此類推。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>PageNo</code> 的值必須依序遞增且不可重複。   </div><br>   <br><br>* 請保持 `IsMerge` 與 `IsMergeUserId` 的值不變。 |
|Name |String |否 |`Viewer A` |暱稱。返回暱稱包含此值的觀眾行為數據。 |
|StartTime |Long |否 |`1642070520` |開始時間（Unix 時間戳格式）。返回於此時間或之後進入直播間的觀眾行為數據。單位：秒。 |
|EndTime |Long |否 |`1642070920` |結束時間（Unix 時間戳格式）。返回於此時間或之前離開直播間的觀眾行為數據。單位：秒。 |
|IsMerge |Integer |否 |`0` |指定是否根據裝置 ID，合併同一裝置多次進出直播間的觀眾行為數據。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：不合併數據。<br><br>* `1`：合併數據。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若觀眾可在未登入直播間的情況下觀看預覽、直播和回放，建議以此方式合併資料，以獲得更精確的數據。</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>IsMerge</code> 和 <code>IsMergeUserId</code> 不可同時設為 <code>1</code>。</div><br> |
|Source |Integer |否 |`0` |返回此來源的數據。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `-1`：返回所有地址的數據。<br><br>* `0`：返回預設地址的數據。<br><br>* `1`：返回地址 A 的數據。<br><br>* `2`：返回地址 B 的數據。<br><br>* `3`：將返回來自地址 C 的資料。<br><br>* `4`：將返回來自地址 D 的資料。 |
|PlayStatus |整數 |否 |`1` |指定統計維度。預設值：`10`。<br><br>有效值：<br><br><br>* `1`：返回觀看直播影片的觀眾資料。<br><br>* `2`：返回觀看預覽的觀眾資料。<br><br>* `3`：返回觀看回放的觀眾資料。<br><br>* `10`：返回訪問觀看頁面的觀眾資料。<br><br>* `11`：返回觀看直播、預覽及回放的觀眾資料。 |
|IsMergeUserId |整數 |否 |`0` |根據用戶 ID，指定是否合併多次進出直播間的觀眾行為資料。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：不合併資料。<br><br>* `1`：合併資料。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若觀眾必須登入直播間才能觀看預覽、直播和回放，建議以此方式合併資料，以獲得更精確的數據。</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>IsMerge</code> 和 <code>IsMergeUserId</code> 不可同時設為 <code>1</code>。</div><br> |
|Extra |字串 |否 |`行銷部門` |同步至 BytePlus Live 的額外參數，可用於與觀眾關聯。例如，您可以將觀眾的部門從自有帳號系統同步至 BytePlus Live。 |


<span id="924e5e72"></span>
## 回應參數


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|TotalItemCount |整數 |`1` |返回結果總數。 |
|Data |陣列[UserBehaviorData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi-zh-TW#d456d258) |`-` |觀眾詳細行為資料。 |
|ScrollId |字串 |`IN1ZTTzdZN3J3AAAAAAA****WTFdZalFSaGt` |滾動 ID。 |


<span id="d456d258"></span>
### UserBehaviorData


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|UserId |長整數 |`172741906088****` |觀眾在 BytePlus Live 的唯一識別碼。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若觀眾未透過輸入暱稱或其他方式登入直播間，則該觀眾的用戶 ID 為 0。</div><br> |
|UserName |字串 |`觀眾 A` |觀眾暱稱。 |
|Region |字串 |`新加坡` |觀眾所在區域。 |
|IP |字串 |`4.**.**.89` |觀眾的 IP 位址。若在請求中將 `IsMerge` 或 `IsMergeUserId` 設為 `1`，則此參數值可能包含多個以空格分隔的 IP 位址。 |
|JoinAt |整數陣列 |`1714653969` |觀眾進入直播間的時間（Unix 時間戳格式）。單位：秒。 |
|leaveAt |整數陣列 |`1714668359` |觀眾離開直播間的時間（Unix 時間戳格式）。單位：秒。 |
|WatchTime |整數 |`239` |觀眾觀看時長。單位：分鐘。 |
|UserTel |字串 |`1560000****` |觀眾電話號碼。 |
|InviteCode |字串 |`2711****` |觀眾使用的邀請碼。 |
|AccessTime |字串 |`playing before` |表示觀眾進入直播間相對於直播的時間點。<br><br>有效值：<br><br><br>* `playing`：直播期間。<br><br>* `playing before`：直播開始前。<br><br>* `playing post`：直播結束後。 |
|UserDevice |字串陣列 |`Windows 10` |觀眾使用的裝置類型。 |
|Extra |字串 |`行銷部門` |同步至 BytePlus Live 的額外參數，可用於與觀眾關聯。例如，您可以將觀眾的部門從自有帳號系統同步至 BytePlus Live。 |
|ExternalUserId |字串 |`403343425511****` |觀眾在第三方平台的唯一識別碼。您可以使用此關聯用戶 ID 來識別觀眾在組織內的身份，並根據需求進行用戶洞察與資料分析。<br><br>觀眾的關聯用戶 ID 會根據其登入直播間的方式而有所不同。<br><br><br>* 自定帳號：自定登入時透過 `UserId` 參數傳遞的值。更多資訊請參見 [自訂驗證登入](https://docs.byteplus.com/docs/byteplus-livesaas/zi-ding-yan-zheng-deng-ru-zh-TW)。<br><br>* 電話號碼：當觀眾使用電話號碼註冊 BytePlus Live 時所生成的 `passport_id`。<br><br>* OAuth 2.0：對應於你自有帳戶系統中用戶 ID 的欄位。<br><br>* Allowlist：觀眾輸入的 allowlist 驗證資訊。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當觀眾以上述方式登入直播間時，此參數才會有值。</div><br> |
|SilenceStatus |整數 |`1` |表示觀眾是否被靜音。<br><br><br>* `1`：已靜音。<br><br>* 其他值：未靜音。 |
|CommentCounts |整數 |`5` |觀眾發送的評論數量。 |


<span id="735d1510"></span>
## 範例

<span id="d820d185"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListUserBehaviorDataAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageItemCount=10&ScrollId=klTVnVZdFk3bWg4YVQwdwAAAAAASn****xybkZ1el&Source=0&IsMerge=0&IsMergeUserId=0
```


<span id="5eba56c8"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "ListUserBehaviorDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714673762
    },
    "Result": {
        "TotalItemCount": 1,
        "Data": [
            {
                "UserName": "Viewer A",
                "Region": "Singapore",
                "IP": "4.**.**.89",
                "JoinAt": [
                    1714653969
                ],
                "leaveAt": [
                    1714668359
                ],
                "UserId": 172741906088****,
                "UserTel": "-",
                "InviteCode": "-",
                "WatchTime": 239,
                "CommentCounts": 5,
                "AccessTime": "playing before",
                "Extra": "",
                "UserDevice": [
                    "Windows 10"
                ],
                "ExternalUserId": "",
                "SilenceStatus": 1
            }
        ],
        "ScrollId": "IN1ZTTzdZN3J3AAAAAAA****WTFdZalFSaGt"
    }
}
 
```


<span id="UserBehaviorData"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
