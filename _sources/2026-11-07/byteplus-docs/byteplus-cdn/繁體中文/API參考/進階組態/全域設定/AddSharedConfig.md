---
title: "AddSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-AddSharedConfig_zh-tw"
---

建立一個全域設定。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=AddSharedConfig&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `AddSharedConfig`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ConfigName |String |是 |表示全域設定的名稱。名稱有以下要求：<br><br><br>* 名稱可以包含漢字、字母、數字、底線（_），長度在 3\-45 個字元之間。一個漢字占 3 個字元。<br><br>* 名稱不能與主帳戶下某個已有的全域設定的名稱相同。 |`my_list` |
|ConfigType |String |是 |表示該全域設定的類型。該參數有以下取值：<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名單。<br><br>* `allow_ip_access_rule`：表示 IP 白名單。<br><br>* `deny_referer_access_rule`：表示 Referer 黑名單。<br><br>* `allow_referer_access_rule`：表示 Referer 白名單。<br><br>* `common_match_list`：表示通用列表。 |`allow_ip_access_rule` |
|AllowIpAccessRule |Object |否 |表示一個 IP 白名單的設定，對應 `ConfigType` 是 `allow_ip_access_rule`。 | |
|Rules |String[] |否 |表示一個項目列表，列表中的每個項目是一個 IP 位址或 CIDR 網段。IP 位址和網段可以是 IPv4 和 IPv6 格式。<br><br>列表的配額如下：<br><br><br>* 列表最多可以包含 30,000 個項目。<br><br><br>CDN 在建立該全域設定時，會將列表中重複的項目刪除。重複項目不佔用配額。 |`["x.x.x.x","xx.xx.xx.xx/24"]` |
|AllowRefererAccessRule |Object |否 |表示一個 Referer 白名單的設定，對應 `ConfigType` 是 `allow_referer_access_rule`。 | |
|AllowEmpty |Boolean |否 |表示是否不允許 Referer 標頭為空（""）或者不包含 Referer 標頭的請求。該參數有以下取值：<br><br><br>* `true`：表示不允許。如果請求的 Referer 標頭為空（""）或者不包含 Referer 標頭，CDN 拒絕請求。<br><br>* `false`：表示允許。<br><br><br>該參數的預設值是 `false`。 |`false` |
|CommonType |Object |否 |表示該 Referer 白名單的內容。 | |
|IgnoreCase |Boolean |否 |表示 `Rules` 中的項目是否區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。<br><br><br>該參數的預設值是 `true`。 |`true` |
|Rules |String[] |否 |表示一個項目列表，列表中的每個項目是一個網域名稱或 IP 位址。網域名稱可以是萬用字元網域名稱，IP 位址可以是 IPv4 和 IPv6 格式。<br><br>列表的配額如下：<br><br><br>* 列表最多可以包含 4,000 個項目。<br><br><br>CDN 在建立該全域設定時，會將列表中重複的項目刪除。重複項目不佔用配額。 |`["xx.xx.xx.xx","*.example.com"]` |
|DenyIpAccessRule |Object |否 |表示一個 IP 黑名單的設定，對應 `ConfigType` 是 `deny_ip_access_rule`。 | |
|Rules |String[] |否 |該參數的說明與 IP 白名單下 `Rules` 的說明相同。 |`["x.x.x.x","xx.xx.xxx.xx"]` |
|DenyRefererAccessRule |Object |否 |表示一個 Referer 黑名單的設定，對應 `ConfigType` 是 `deny_referer_access_rule`。 | |
|AllowEmpty |Boolean |否 |表示是否允許 Referer 標頭為空（""）或者不包含 Referer 標頭的請求。該參數有以下取值：<br><br><br>* `true`：表示允許。<br><br>* `false`：表示不允許。如果請求的 Referer 標頭為空（""）或者不包含 Referer 標頭，內容傳遞網路拒絕請求。<br><br><br>該參數的預設值是 `true`。 |`true` |
|CommonType |Object |否 |表示該 Referer 黑名單的內容。 | |
|IgnoreCase |Boolean |否 |該參數的說明與 Referer 白名單下 `IgnoreCase` 的說明相同。 |`true` |
|Rules |String[] |否 |該參數的說明與 Referer 白名單下 `Rules` 的說明相同。 |`["x.x.x.xxx","*.example.com"]` |
|Project |String |否 |表示該全域設定所歸屬的專案名稱，預設值是 `default`。<br><br>您可以訪問 [專案管理](https://console.byteplus.com/iam/resourcemanage/project) 查看已建立的專案以及每個專案包含的資源。 |`default` |
|CommonMatchList |Object |否 |表示一個通用列表的設定，對應 `ConfigType` 是 `common_match_list`。 | |
|CommonType |Object |否 |表示該通用列表的內容。 | |
|IgnoreCase |Boolean |否 |表示 `Rules` 中的項目是否區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。<br><br><br>該參數的預設值是 `true`。 |`true` |
|Rules |String[] |否 |表示一個項目列表，列表中的每個項目是一個字串。<br><br>列表的配額如下：<br><br><br>* 列表最多可以包含 4,000 個項目。<br><br>* 所有項目的總長度不能超過 200,000 個字元。<br><br><br>CDN 在建立該全域設定時，會將列表中重複的項目刪除。重複項目不佔用配額。 |`["param1","param2"]` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=AddSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List",
    "ConfigType": "allow_referer_access_rule",
    "AllowRefererAccessRule": {
        "CommonType": {
            "Rules": [
                "xxx.xx.xxx.xxx",
                "www.example.com",
                "abc.example.com"
            ]
        }
    }
}
```


&nbsp;
