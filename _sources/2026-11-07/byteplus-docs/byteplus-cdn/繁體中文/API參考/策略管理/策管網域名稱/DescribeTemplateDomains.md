---
title: "DescribeTemplateDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplateDomains_zh-tw"
---

取得符合篩選條件的網域名稱列表。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateDomains&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeTemplateDomains`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Filters |Object[] |否 |表示一組篩選條件，用於取得符合條件的網域名稱列表。如果您不指定任何篩選條件，該 API 則回傳所有您帳號下的網域名稱。<br><br>多個篩選條件之間是 "且" 的關係，即只有滿足所有篩選條件，一個網域名稱才會包含在該 API 回傳的網域名稱列表中。<br><br>在該 API 的回應中，實際回傳的網域名稱列表受 `PageNum` 和 `PageSize` 的影響。 | |
|Fuzzy |Boolean |否 |表示匹配方式。該參數有以下取值：<br><br><br>* `true`：表示模糊匹配。在網域名稱的匹配過程中，如果 `Name` 的對應值包含 `Value` 陣列中的任意值，該網域名稱就被認為是符合篩選條件。<br><br>* `false`：表示精確匹配。如果 `Name` 的對應值包含 `Value` 陣列中值相同，該網域名稱就被認為是符合篩選條件。<br><br><br>同時，您可以指定的 `Fuzzy` 值會受到 `Name` 值的影響。 參見 `Name` 的描述。<br><br>該參數的預設值是 `false`。 |`false` |
|Name |String |否 |表示篩選類型。該參數有以下取值：<br><br><br>* `TemplateTitle`：表示按綁定的策略的名稱對網域名稱進行篩選。<br><br>* `TemplateId`：表示按綁定的策略的 ID 對網域名稱進行篩選。對於該參數值，`Fuzzy` 的值只能是 `false`。<br><br>* `TemplateType`：表示按綁定的策略的類型對網域名稱進行篩選。對於該參數值，`Fuzzy` 的值只能是 `false`。<br><br>* `Domain`：表示按名稱對網域名稱進行篩選。<br><br>* `Status`：表示按狀態對網域名稱進行篩選。對於該參數值，`Fuzzy` 的值只能是 `false`。<br><br>* `HTTPSSwitch`：表示按 "HTTPS加密服務" 的狀態對網域名稱進行篩選。對於該參數值，`Fuzzy` 的值只能是 `false`。<br><br>* `WAFStatus`：表示按 "WAF防護" 的狀態對網域名稱進行篩選。對於該參數值，`Fuzzy` 的值只能是 `false`。<br><br><br>您可以同時指定多個篩選條件，但是不同篩選條件中的 `Name` 不能相同。 |`TemplateTitle` |
|Value |String[] |否 |表示 `Name` 對應的值，是一個陣列。陣列中的值用於與物件值匹配。如果物件值匹配陣列中的任意值，就被認為是匹配。參數值在匹配時區分大小寫。<br><br><br>* 當 `Name` 是 `TemplateTitle` 或 `Domain` 時，`Value` 中每個值的長度不能超過 100 個字元。另外，<br><br>   * 當 `Fuzzy` 是 `false` 時，`Value` 中可以包含多個值。<br><br>   * 當 `Fuzzy` 是 `true` 時，`Value` 中只能包含一個值。<br><br>* 當 `Name` 是 `TemplateId` 時，`Value` 中只能包含一個值。<br><br>* 當 `Name` 是 `TemplateType` 時，`Value` 中可以包含以下一個或者多個值：<br><br>   * `cipher`：表示加密策略。<br><br>   * `service`：表示分發策略。<br><br>* 當 `Name` 是 `Status` 時，`Value` 中可以包含以下某個值：<br><br>   * `online`：表示網域名稱的狀態是 "線上"。<br><br>   * `offline`：表示網域名稱的狀態是 "離線"。<br><br>   * `configuring`：表示網域名稱的狀態是 "配置中"。<br><br>* 當 `Name` 是 `HTTPSSwitch` 時，`Value` 中可以包含以下某個值：<br><br>   * `on`：表示 "HTTPS加密服務" 的狀態是啟用。<br><br>   * `off`：表示 "HTTPS加密服務" 的狀態是停用。<br><br>* 當 `Name` 是 `WAFStatus` 時，`Value` 中可以包含以某個值：<br><br>   * `on`：表示 "WAF防護" 的狀態是啟用。<br><br>   * `off`：表示 "WAF防護" 的狀態是停用。 |`["TestPolicy"]` |
|PageNum |Long |否 |對於回傳的結果集，此參數表示一個頁碼，該 API 實際回傳的網域名稱是該頁碼所指定的分頁上的那些網域名稱。<br><br>該 API 回傳的網域名稱是根據 `PageSize` 而分頁的。假設該 API 回傳的網域名稱數量是 100，您指定的 `PageSize` 是 `10`，那麼回傳的網域名稱大致分布在 10 個頁面上。如果您指定的 `PageNum` 是 `2`，表示取得第 2 頁上的那些網域名稱。<br><br>如果您指定的分頁上沒有網域名稱，則回傳結果中 `Domains` 參數的值為 `null`。<br><br>`PageNum` 的預設值是 1。 |`1` |
|PageSize |Long |否 |表示每個分頁包含的網域名稱數量。<br><br>此參數的取值範圍是 1\-200，預設值是 `10`。 |`10` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Domains |Object[] |表示該 API 回傳的網域名稱列表。<br><br>需要留意的是，列表中的網域名稱是請求參數 `PageNum` 所表示的分頁上的那些網域名稱，不一定是所有符合篩選條件的網域名稱。 | |
|CertInfo |Object |表示與 `Domain` 指定的網域名稱關聯的憑證的資訊。<br><br>如果 `HTTPSSwitch` 是 `off`，該參數值是 `null`。 | |
|CertId |String |表示與該網域名稱關聯的憑證的 ID。該憑證是託管在 BytePlus 憑證中心的。 |`cert-044833503b2349b4b42a5e80b0aa8c23` |
|Source |String |证书来源。enums: cert_center、cdn_cert_hosting | |
|Cname |String |表示 CDN 分配給該網域名稱的 CNAME。 |`www.example.com.bplslb.com` |
|Domain |String |表示 `Domains` 列表中的一個網域名稱。 |`www.example.com` |
|HTTPSSwitch |String |表示該網域名稱是否啟用了 "HTTPS加密服務"。該參數有以下取值：<br><br><br>* `on`：表示該服務已啟用。<br><br>* `off`：表示該服務已停用。 |`off` |
|LockStatus |String |表示該網域名稱是否被鎖定。該參數有以下取值：<br><br><br>* `on`：表示該網域名稱已被鎖定。此時，您無法使用 [UpdateTemplateDomain](https://docs.byteplus.com/byteplus-cdn/reference/reference-UpdateTemplateDomain_zh-tw) 修改該網域名稱的配置。<br><br>* `off`：表示該網域名稱未被鎖定。 |`off` |
|Remark |String |表示該網域名稱被鎖定的原因。<br><br><br>* 如果 `LockStatus` 是 `on`，該參數表示鎖定的原因。<br><br>* 如果 `LockStatus` 是 `off`，該參數值為空（""）。 |`This is a test.` |
|ServiceRegion |String |表示該網域名稱啟用的加速區域。該參數有以下取值<br><br><br>* `outside_chinese_mainland`：表示 "全球（不包含中國內地）"。<br><br>* `chinese_mainland`：表示 "中國內地"。<br><br>* `global`：表示 "全球"。 |`outside_chinese_mainland` |
|Status |String |表示該網域名稱的狀態。該參數有以下取值：<br><br><br>* `online`：表示狀態是 "線上"。<br><br>* `offline`：表示狀態是 "離線"。<br><br>* `configuring`：表示狀態是 "配置中"。 |`online` |
|Templates |Object[] |表示與該網域名稱綁定的策略列表。<br><br>一個網域名稱必須也只能與一個分發策略綁定，可選與一個加密策略綁定。 | |
|TemplateId |String |表示一個策略的 ID。 |`tpl-s2DVaW` |
|Title |String |表示該策略的名稱。 |`NetTVPlayer002` |
|Type |String |表示該策略的類型。該參數有以下取值：<br><br><br>* `cipher`：表示加密策略。<br><br>* `service`：表示分發策略。 |`service` |
|Exception |Boolean |表示該策略是否包含特殊配置。特殊配置指的是那些不由使用者，而是由 BytePlus 工程師操作的配置。該參數有以下取值：<br><br><br>* `true`：表示包含特殊配置。<br><br>* `false`：表示不包含特殊配置。 |`false` |
|ProdVersion |String |表示該策略已發布版本的版本號。 |`P-250804.86120` |
|WAFStatus |String |表示該網域名稱是否啟用了 "WAF防護"。該參數有以下取值：<br><br><br>* `on`：表示 "WAF防護" 已啟用。<br><br>* `off`：表示 "WAF防護" 已停用。 |`off` |
|Project |String |表示該網域名稱所歸屬的專案。 |`default` |
|Tags |Object[] |表示新增到 `Domain` 的標籤列表。標籤是一個鍵值對。如果 `Domain` 沒有標籤，該參數值是 `null`。 | |
|Key |String |表示列表中一個標籤的 key。 |`myKey` |
|Value |String |表示該標籤的值， |`myValue` |
|TotalCount |Long |表示符合篩選條件的網域名稱的數量。該參數值不受 `PageSize` 和 `PageNum` 的影響。 |`1` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateDomains&Version=2021-03-01
{
    "Filters": [
        {
            "Name": "Domain",
            "Value": [
                "example"
            ],
            "Fuzzy": true
        },
        {
            "Name": "TemplateTitle",
            "Value": [
                "NetTVPlayer"
            ],
            "Fuzzy": true
        },
        {
            "Name": "TemplateId",
            "Value": [
                "tpl-s2DVaW"
            ],
            "Fuzzy": false
        },
        {
            "Name": "TemplateType",
            "Value": [
                "service",
                "cipher"
            ],
            "Fuzzy": false
        },
        {
            "Name": "HTTPSSwitch",
            "Value": [
                "off"
            ],
            "Fuzzy": false
        },
        {
            "Name": "WAFStatus",
            "Value": [
                "off"
            ]
        },
        {
            "Name": "Status",
            "Value": [
                "online"
            ],
            "Fuzzy": false
        }
    ]
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20240305044725DD2386782EADAD775440",
        "Action": "DescribeTemplateDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "CertInfo": null,
                "Cname": "www.example.com.bplslb.com",
                "Domain": "www.example.com",
                "HTTPSSwitch": "off",
                "LockStatus": "off",
                "Project": "default",
                "Remark": "",
                "ServiceRegion": "outside_chinese_mainland",
                "Status": "online",
                "Templates": [
                    {
                        "Exception": false,
                        "TemplateId": "tpl-s2DVaW",
                        "Title": "NetTVPlayer002",
                        "Type": "service"
                    }
                ],
                "WAFStatus": "off",
                "Tags": [
                    {
                        "Key": "myKey1",
                        "Value": "myValue1"
                    },
                    {
                        "Key": "myKey2",
                        "Value": "myValue2"
                    }
                ]
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
