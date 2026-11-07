---
title: "DescribeSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeSharedConfig_zh-tw"
---

取得一個全域設定的設置。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeSharedConfig&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeSharedConfig`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ConfigName |String |否 |表示一個全域設定的名稱。 |`my_list` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|AllowIpAccessRule |Object |表示 IP 允許清單的設定，對應的 `ConfigType` 是 `allow_ip_access_rule`。 | |
|Rules |String[] |表示該 IP 允許清單中的項目。 |`["xx.xx.xx.xx","xxx.xxx.x.x"]` |
|AllowRefererAccessRule |Object |表示 Referer 允許清單的設定，對應的 `ConfigType` 是 `allow_referer_access_rule`。 | |
|AllowEmpty |Boolean |表示是否不允許 Referer 標頭為空（""）或者不包含 Referer 標頭的請求。該參數有以下取值：<br><br><br>* `true`：表示不允許。如果請求的 Referer 標頭為空（""）或者不包含 Referer 標頭，CDN 會拒絕請求。<br><br>* `false`：表示允許。 |`true` |
|CommonType |Object |表示該 Referer 允許清單的內容。 | |
|IgnoreCase |Boolean |表示 `Rules` 中的項目是否區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。 |`true` |
|Rules |String[] |表示該 Referer 允許清單中的項目。 |`["x.x.x.x","*.example.com","www.example.com"]` |
|ConfigName |String |表示該全域設定的名稱。 |`my_list` |
|ConfigType |String |表示該全域設定的類型。該參數有以下取值：<br><br><br>* `deny_ip_access_rule`：表示 IP 封鎖清單。<br><br>* `allow_ip_access_rule`：表示 IP 允許清單。<br><br>* `deny_referer_access_rule`：表示 Referer 封鎖清單。<br><br>* `allow_referer_access_rule`：表示 Referer 允許清單。<br><br>* `common_match_list`：表示通用清單。<br><br>* `4xx_error_page`: 表示自訂錯誤頁面。 |`allow_ip_access_rule` |
|DenyIpAccessRule |Object |表示 IP 封鎖清單的設定，對應的 `ConfigType` 是 `deny_ip_access_rule`。 | |
|Rules |String[] |表示該 IP 封鎖清單中的項目。 |`["xx.xx.xx.xx","xxx.xxx.x.x"]` |
|DenyRefererAccessRule |Object |表示 Referer 封鎖清單的設定，對應的 `ConfigType` 是 `deny_referer_access_rule`。 | |
|AllowEmpty |Boolean |表示是否允許 Referer 標頭為空（""）或者不包含 Referer 標頭的請求。該參數有以下取值：<br><br><br>* `true`：表示允許。<br><br>* `false`：表示不允許。如果請求的 Referer 標頭為空（""）或者不包含 Referer 標頭，CDN 會拒絕請求。 |`true` |
|CommonType |Object |表示該 Referer 封鎖清單的內容。 | |
|IgnoreCase |Boolean |該參數的說明與 Referer 允許清單下 `IgnoreCase` 的說明相同。 |`true` |
|Rules |String[] |表示該 Referer 封鎖清單中的項目。 |`["x.x.x.x","*.example.com","www.example.com"]` |
|Project |String |表示該全域設定所歸屬的專案名稱。 |`default` |
|CommonMatchList |Object |表示通用清單的設定，對應的 `ConfigType` 是 `common_match_list`。 | |
|CommonType |Object |表示該通用清單的內容。 | |
|IgnoreCase |Boolean |該參數的說明與 Referer 允許清單下 `IgnoreCase` 的說明相同。 |`true` |
|Rules |String[] |表示該通用清單中的項目。 |`["abc","param"]` |
|ErrorPageRule |Object |表示自訂錯誤頁面的設定。 | |
|RuleContent |String |表示該自訂錯誤頁面的 HTML 程式碼。 |`<html><head><title>Test</title></head><body><h1>Header</h1>Hello World</body></html>` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20241209082302440129758BDA68D5D9AF",
        "Action": "DescribeSharedConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AllowRefererAccessRule": {
            "AllowEmpty": false,
            "CommonType": {
                "IgnoreCase": true,
                "Rules": [
                    "xxx.xx.xxx.xxx",
                    "www.example.com",
                    "abc.example.com"
                ]
            }
        },
        "CommonMatchList": null,
        "ConfigName": "My_List",
        "ConfigType": "allow_referer_access_rule",
        "Project": "default"
    }
}
```


&nbsp;
