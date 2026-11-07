---
title: "ListSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListSharedConfig_zh-tw"
---

基於您指定的查詢條件，取得符合條件的全域配置清單。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=ListSharedConfig&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `ListSharedConfig`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ConfigName |String |否 |表示一個全域配置的名稱，用來取得精確匹配該名稱的全域配置。 |`my_list` |
|ConfigType |String |否 |指定一個全域配置的類型，取得該類型的全域配置清單。該參數有以下取值：<br><br><br>* `deny_ip_access_rule`：表示 IP 封鎖清單。<br><br>* `allow_ip_access_rule`：表示 IP 允許清單。<br><br>* `4xx_error_page`: 表示自訂錯誤頁面。<br><br>* `deny_referer_access_rule`：表示 Referer 封鎖清單。<br><br>* `allow_referer_access_rule`：表示 Referer 允許清單。<br><br>* `common_match_list`：表示通用清單。 |`allow_ip_access_rule` |
|PageNum |Long |否 |表示一個頁碼。CDN 根據 `PageSize`，對符合查詢條件的全域配置清單進行分頁。假設該 API 回傳的全域配置的數量是 100，`PageSize` 是 `10`，那麼這些全域配置分布在 10 個頁面上。CDN 預設展示第 1 頁上的全域配置。<br><br>該參數的預設值是 `1`。 |`1` |
|PageSize |Long |否 |指定每頁包含的全域配置數量。<br><br>該參數的取值範圍是 1\-1,000，預設值是 `10`。 |`10` |
|Project |String |否 |指定一個專案名稱，取得歸屬該專案的全域配置。 |`default` |
|ConfigTypeList |String[] |否 |指定一個或多個全域配置的類型，取得這些類型的全域配置清單。該參數值可以是 `ConfigType` 可用值的組合。`ConfigType` 與 `ConfigTypeList` 不能同時指定。 |`["allow_ip_access_rule","deny_ip_access_rule"]` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|ConfigData |Object[] |表示符合查詢條件的全域配置清單。 | |
|ConfigName |String |表示列表中的一個全域配置的名稱。 |`my_list` |
|ConfigType |String |表示該全域配置的類型。該參數有以下取值：<br><br><br>* `deny_ip_access_rule`：表示 IP 封鎖清單。<br><br>* `allow_ip_access_rule`：表示 IP 允許清單。<br><br>* `4xx_error_page`: 表示自訂錯誤頁面。<br><br>* `deny_referer_access_rule`：表示 Referer 封鎖清單。<br><br>* `allow_referer_access_rule`：表示 Referer 允許清單。<br><br>* `common_match_list`：表示通用清單。 |`deny_ip_access_rule` |
|DomainCount |Long |表示與該全域配置關聯的網域名稱的數量。 |`2` |
|Project |String |表示該全域配置所歸屬的專案。 |`default` |
|UpdateTime |Long |表示該全域配置的最近修改時間，單位是 Unix 時間戳記。 |`1655856000` |
|PageNum |Long |表示您在請求中指定的 `PageNum`。 |`1` |
|PageSize |Long |表示您在請求中指定的 `PageSize`。 |`10` |
|Total |Long |表示符合查詢條件的全域配置總數。 |`20` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=ListSharedConfig&Version=2021-03-01
{
    "ConfigType": "allow_ip_access_rule"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20240117195639014D4059167D42B2C640",
        "Action": "ListSharedConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ConfigData": [
            {
                "ConfigName": "deny_ip",
                "ConfigType": "deny_ip_access_rule",
                "DomainCount": 0,
                "Project": "default",
                "UpdateTime": 1705492181
            },
            {
                "ConfigName": "error_page",
                "ConfigType": "4xx_error_page",
                "DomainCount": 1,
                "Project": "default",
                "UpdateTime": 1705334019
            },
            {
                "ConfigName": "common_list",
                "ConfigType": "common_match_list",
                "DomainCount": 0,
                "Project": "default",
                "UpdateTime": 1705332721
            },
            {
                "ConfigName": "deny_referer",
                "ConfigType": "deny_referer_access_rule",
                "DomainCount": 3,
                "Project": "default",
                "UpdateTime": 1702484378
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 34
    }
}
```


&nbsp;
