---
title: "UpdateSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateSharedConfig_zh-tw"
---

修改一個全域設定。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=UpdateSharedConfig&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `UpdateSharedConfig`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ConfigName |String |是 |表示一個全域設定的名稱。<br><br>您可以呼叫 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListSharedConfig_zh-tw) 取得已有的全域設定名稱。 |`MySharedConfig` |
|AllowIpAccessRule |Object |否 |表示 IP 允許清單的設定，對應 `ConfigType` 是 `allow_ip_access_rule`。 | |
|Option |String |否 |表示修改操作的類型。該參數有以下取值：<br><br><br>1. `overlap`：表示全量覆蓋已有條目。<br><br>2. `add`：表示增加條目。<br><br>3. `delete`：表示刪除指定的條目。<br><br><br>該參數的預設值為 `overlap`。 |`add` |
|Rules |String[] |否 |表示一個條目列表。每個條目是一個 IP 位址或 CIDR 網段。IP 位址和網段可以是 IPv4 和 IPv6 格式。<br><br>列表的額度如下：<br><br><br>* 如果 `Option` 是 `overlap`，列表中條目的數量不能超過 30,000 個。<br><br>* 如果 `Option` 是 `add`，列表中條目與 `ConfigName` 中已有條目總計不能超過 30,000 個。您可以呼叫 [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeSharedConfig_zh-tw) 計算該全域設定中已有的條目數量。<br><br><br>當 CDN 在更新 `ConfigName` 時，會將列表中重複的條目刪除。重複條目不佔額度。 |`["xx.xxx.xxx.xx","xxx.xxx.xxx.xxx"]` |
|DenyIpAccessRule |Object |否 |表示 IP 封鎖清單的設定，對應的 `ConfigType` 是 `deny_ip_access_rule`。 | |
|Option |String |否 |該參數的說明與 IP 允許清單設定下 `Option` 的說明相同。 |`overlap` |
|Rules |String[] |否 |該參數的說明與 IP 允許清單設定下 `Rules` 的說明相同。 |`["xx.xxx.xxx.xx","xxx.xxx.xxx.xxx/24"]` |
|AllowRefererAccessRule |Object |否 |表示 Referer 允許清單的設定，對應的 `ConfigType` 是 `allow_referer_access_rule`。 | |
|AllowEmpty |Boolean |否 |表示 Referer 標頭為空（""）或請求不包含 Referer 標頭時，該請求是否會被列入允許清單。該參數有以下可選值：<br><br><br>* `true`：表示這類請求會被列入允許清單。<br><br>* `false`：表示這類請求不會被列入允許清單。<br><br>   該參數的預設值為 `false`。 |`true` |
|CommonType |Object |否 |表示該 Referer 允許清單的內容。 | |
|IgnoreCase |Boolean |否 |表示 `Rules` 中的條目是否區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。<br><br><br>該參數的預設值是 `true`。 |`true` |
|Option |String |否 |該參數的說明與 IP 允許清單設定下 `Option` 的說明相同。 |`overlap` |
|Rules |String[] |否 |表示一個條目列表。每個條目是一個 IP 位址或網域名稱。IP 位址可以是 IPv4 和 IPv6 格式，網域名稱可以是萬用字元網域名稱。<br><br>列表的額度如下：<br><br><br>* 如果 `Option` 是 `overlap`，列表中條目的數量不能超過 4,000 個。<br><br>* 如果 `Option` 是 `add`，列表中條目與 `ConfigName` 中已有條目總計不能超過 4,000 個。您可以呼叫 [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeSharedConfig_zh-tw) 計算該全域設定中已有的條目數量。<br><br><br>當 CDN 在更新 `ConfigName` 時，會將列表中重複的條目刪除。重複條目不占額度。 |`["xxx.xx.xx.xxx","*.example.com"]` |
|DenyRefererAccessRule |Object |否 |表示 Referer 封鎖清單的設定，對應的 `ConfigType` 是 `deny_referer_access_rule`。 | |
|AllowEmpty |Boolean |否 |表示 Referer 標頭為空（""）或請求不包含 Referer 標頭時，該請求是否會被列入封鎖清單。該參數有以下可選值：<br><br><br>* `true`：表示這類請求會被列入封鎖清單。<br><br>* `false`：表示這類請求不會被列入封鎖清單。<br><br>   該參數的預設值為 `false`。 |`true` |
|CommonType |Object |否 |表示該 Referer 封鎖清單的內容。 | |
|IgnoreCase |Boolean |否 |該參數的說明與 Referer 允許清單設定下 `IgnoreCase` 的說明相同。 |`true` |
|Option |String |否 |該參數的說明與 IP 允許清單設定下 `Option` 的說明相同。 |`overlap` |
|Rules |String[] |否 |該參數的說明與 Referer 允許清單設定下 `Rules` 的說明相同。 |`["xxx.xx.xx.xxx","*.example.com"]` |
|CommonMatchList |Object |否 |表示通用清單的設定，對應的 `ConfigType` 是 `common_match_list`。 | |
|CommonType |Object |否 |表示該通用清單的內容。 | |
|IgnoreCase |Boolean |否 |表示 `Rules` 中的項目是否區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。<br><br><br>該參數的預設值是 `true`。 |`false` |
|Option |String |否 |該參數的說明與 IP 允許清單設定下 `Option` 的說明相同。 |`overlap` |
|Rules |String[] |否 |表示一個項目清單。每個項目是一個字串。<br><br>清單的配額如下：<br><br><br>* 如果 `Option` 是 `overlap`，清單中項目的數量不能超過 4,000 個，所有項目的總長度不能超過 200,000 個字元。<br><br>* 如果 `Option` 是 `add`，清單中項目與 `ConfigName` 中已有項目總計不能超過 4,000 個。您可以呼叫 [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeSharedConfig_zh-tw) 計算該全域設定中已有的項目數量。<br><br><br>當 CDN 在更新 `ConfigName` 時，會將清單中重複的項目刪除。重複項目不佔用配額。 |`["param1","param2"]` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=UpdateSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List",
    "DenyRefererAccessRule": {
        "CommonType": {
            "Option": "add",
            "Rule": [
                "xx.xxx.xxx.xx",
                "xxx.xxx.xxx.xx"
            ]
        }
    }
}
```


&nbsp;
