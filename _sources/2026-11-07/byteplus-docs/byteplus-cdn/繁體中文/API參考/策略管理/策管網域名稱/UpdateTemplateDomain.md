---
title: "UpdateTemplateDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateTemplateDomain_zh-tw"
---

指定一個網域名稱列表，修改列表中的網域名稱配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">對於 <code>HTTPSwitch</code> 為 <code>on</code> 的網域名稱，您一次只能修改一個。也就是說，您指定的網域名稱列表中只能包含一個網域名稱。</div>


* <div data-tips="true" data-tips-type="tip">如果您要同時修改多個網域名稱的配置，必須滿足以下所有條件：</div>


   * <div data-tips="true" data-tips-type="tip">在這些網域名稱的當前配置中，<code>HTTPSSwitch</code> 都為 <code>off</code>。</div>


   * <div data-tips="true" data-tips-type="tip">在修改時不指定 <code>HTTPSSwitch</code> 或者在修改後的配置中，<code>HTTPSSwitch</code> 必須為 <code>off</code>。</div>


* <div data-tips="true" data-tips-type="tip">在使用該 API 時，如果您沒有指定某個參數，在您提交 API 請求後，該參數的已有配置不會改變。</div>



<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 XX 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=UpdateTemplateDomain&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">對於 Body 列表中的參數，如果您不指定某個參數，表示不修改指定網域名稱的相應配置。</div>


<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `UpdateTemplateDomain`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domains |String[] |是 |表示一個網域名稱列表，修改它們的配置。<br><br>如果滿足以下任意條件，您在列表中只能指定一個網域名稱。<br><br><br>* 待修改的網域名稱中存在一個網域名稱，其已有的 `HTTPSSwitch` 設置為 `on`。<br><br>* 在呼叫該 API 時，您不指定 `HTTPSSwitch` 參數或者指定 `HTTPSSwitch` 為 `on`。 |`["www.example.com","abc.test.com"]` |
|CertId |String |否 |表示需要與 `Domains` 中的那個網域名稱關聯的憑證的資訊。<br><br><br>* 如果 `HTTPSSwitch` 是 `on`，該參數必填，表示需要與 `Domains` 中的那個網域名稱關聯的憑證的 ID。該憑證是存放在 BytePlus 憑證中心的。<br><br>&nbsp;<br><br>   您可以使用 [ListCertInfo](https://docs.byteplus.com/byteplus-cdn/reference/reference-ListCertInfo_zh-tw) 獲取您想要關聯的憑證的 ID。<br><br>* 如果 `HTTPSSwitch` 是 `off`，該參數無效。 |`cert-044833503b2349b4b42c2e80b0aa8c23` |
|CipherTemplateId |String |否 |表示一個加密策略。該加密策略會與 `Domains` 中的網域名稱綁定。如果在呼叫該 API 時，`Domains` 中的網域名稱已經綁定了加密策略，那麼這些網域名稱會先與已綁定的加密策略解綁，然後再與 `CipherTemplateId` 指定的加密策略綁定。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/reference-DescribeTemplates_zh-tw) 獲取您想要綁定的加密策略的 ID。 |`tpl-cqgRvW` |
|HTTPSSwitch |String |否 |表示是否對 `Domains` 中的網域名稱啟用 "HTTPS加密服務"。該參數有以下取值：<br><br><br>* `on`：表示該服務已啟用。<br><br>* `off`：表示該服務已停用。<br><br><br>如果 `Domains` 中包含多個網域名稱，`HTTPSSwitch` 必須為 `off`。 |`on` |
|ServiceRegion |String |否 |表示對 `Domains` 中的網域名稱啟用的服務區域。該參數有以下取值：<br><br><br>* `outside_chinese_mainland`：表示 "全球（不包含中國內地）"。<br><br>* `chinese_mainland`：表示 "中國內地"。<br><br>* `global`："表示 "全球"。<br><br><br>需要留意的是，`chinese_mainland` 和 `global` 預設不可用。要使用這兩個服務區域，請 [提交工單](https://console.byteplus.com/workorder/create) 。同時，由於這兩個區域包含中國內地，您必須額外完成以下操作：<br><br><br>* 對您的 BytePlus 帳號進行 [實名認證](https://docs.byteplus.com/en/byteplus-platform/docs/real-name-registration)<br><br>* 為您的網域名稱進行 ICP 備案。 |`outside_chinese_mainland` |
|ServiceTemplateId |String |否 |表示一個分發策略。該分發策略會與 `Domains` 中的網域名稱綁定。如果在呼叫該 API 時，`Domains` 中的網域名稱已經綁定了某個分發策略，那麼這些網域名稱會先與已綁定的分發策略解綁，然後再與 `ServiceTemplateId` 指定的分發策略綁定。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/reference-DescribeTemplates_zh-tw) 獲取您想要綁定的分發策略的 ID。 |`tpl-s2Q4mq` |
|SparrowRules |Object[] |否 |表示一組邊緣函數的轉發規則。每條規則包含篩選條件配置以及操作配置。 | |
|Condition |Object |否 |表示當前規則中的篩選條件配置。 | |
|ConditionRule |Object[] |是 |表示一組篩選條件，用於對使用者請求進行篩選。目前，您只能指定一個篩選條件。 | |
|Object |String |是 |表示篩選類型。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `Directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示完整的請求 URL。 |`path` |
|Operator |String |是 |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 與請求中的 `Object` 相同，這個請求就符合該篩選條件。 |`match` |
|Type |String |是 |表示 `Object` 所屬的物件。目前，該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或多個篩選值，總長度不能超過 1,024 個字元。多個篩選值之間使用分號（;）分隔。篩選值不能包含以下字元：<br><br><br>* 連續斜線（//）、空格、美元符號（$）、問號（?）、Delete（ASCII code 127）。<br><br><br>此外，<br><br><br>* 如果 `Object` 是 `filetype`，每個篩選值表示一個請求 URL 後綴，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個篩選值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個篩選值表示一個 URL 路徑，以斜線（/）開頭。每個篩選值中可以包含萬用字元（\*）表示一個或多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`/chs/foods/local*sets;/us/birds/chickadee` |
|Connective |String |是 |表示 `ConditionRule` 中各篩選條件之間的邏輯關係。目前，由於您只能指定一個篩選條件，該參數沒有實際意義。 |`OR` |
|SparrowAction |Object |否 |表示當使用者請求滿足 `Condition` 時，CDN 所執行的操作的配置。 | |
|Action |String |否 |表示 CDN 執行的操作。當前，該參數值只能是 `Bypass`，表示 CDN 將使用者請求交給 `SparrowID` 所指定的函數來處理。<br><br>該參數的預設值是 `Bypass`。 |`Bypass` |
|IgnoreCase |Boolean |否 |表示 `ConditionRule` 中的 `Value` 是否是大小寫敏感的。該參數有以下取值：<br><br><br>* `true`：表示 `Value` 是大小寫不敏感的。<br><br>* `false`：表示 `Value` 是大小寫敏感的。<br><br><br>該參數的預設值是 `true`。 |`true` |
|SparrowID |String |否 |表示處理使用者請求的函數的 ID。您可以呼叫 [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw) 獲取 ID。 |`96ec5429956c42f79a717a4649f3d455` |
|SparrowSwitch |String |否 |表示是否啟用 "邊緣函數" 功能。如果您設置該參數，您在 `Domains` 中只能指定一個網域名稱。<br><br>該參數有以下取值：<br><br><br>* `on`：表示啟用該功能。<br><br>* `off`：表示不啟用該功能。<br><br><br>該參數的預設值是 `off`。 |`on` |
|RuleMode |String |否 |规则策略修改模式，enums, append/override/delete，append表示追加，override表示覆盖, unbind表示解绑 | |
|RuleTemplateIds |String[] |否 |规则策略模板id列表 | |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=UpdateTemplateDomain&Version=2021-03-01
{
    "Domains": [
        "www.example.com"
    ],
    "CipherTemplateId": "tpl-cqgRvW",
    "HTTPSSwitch": "on",
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceTemplateId": "tpl-s2Q4mq",
    "CertId": "cert-044833503b2345b4b42c2e81z0aa5c23",
    "SparrowRules": [
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Object": "filetype",
                        "Operator": "match",
                        "Type": "url",
                        "Value": "asp;php;jsp;ashx;aspx;do"
                    }
                ],
                "Connective": "OR"
            },
            "SparrowAction": {
                "Action": "bypass",
                "IgnoreCase": true,
                "SparrowID": "96ec5429956c42f79a717a4649f3d455"
            }
        }
    ],
    "SparrowSwitch": "on"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "UpdateTemplateDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
