---
title: "AddTemplateDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-AddTemplateDomain_zh-tw"
---

在 BytePlus CDN 中增加一個或多個網域名稱。在增加網域名稱時，您必須指定一個已發布的分發策略，並可選擇性地指定一個已發布的加密策略和規則引擎策略。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=AddTemplateDomain&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `AddTemplateDomain`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示要增加的一個或多個網域名稱。您最多可以指定 50 個網域名稱，多個網域名稱之間請使用逗號 (,) 分隔。您新增的網域名稱必須滿足以下所有條件：<br><br><br>* 長度不超過 100 個字元。<br><br>* 不能包含大寫字母。<br><br>* 不包含任意這些後綴：`zjgslb.com`，`yangyi19.com`，`volcgslb.com`，`veew-alb-cn1.com`，`bplgslb.com`，`bplslb.com`，`ttgslb.com`。<br><br><br>说明<br><br>需要留意的是，當您將您的網域名稱與一個分發策略綁定時，策略中指定的回源地址不能與您的網域名稱相同。 |`www.example.com` |
|ServiceTemplateId |String |是 |表示需要與該網域名稱繫結的一個分發策略。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/reference-DescribeTemplates_zh-tw) 獲取您想要繫結的分發策略的 ID。 |`tpl-s2Q4mq` |
|CertId |String |否 |表示一個憑證的 ID。該憑證是存放在 BytePlus 憑證中心的，將與該網域名稱關聯。<br><br><br>* 如果 `HTTPSSwitch` 是 `on`，該參數必填。在使用該 API 前，您需要先授予 CDN 存取憑證中心的權限，然後將您的憑證上傳到 BytePlus 憑證中心以獲取該憑證的 ID。推薦您使用主帳號授權 CDN 存取憑證中心。<br><br>   您可以使用 [ListCertInfo](https://docs.byteplus.com/byteplus-cdn/reference/reference-ListCertInfo_zh-tw) 獲取您想要關聯的憑證的 ID。<br><br>* 如果 `HTTPSSwitch` 是 `off`，該參數無效。 |`cert-044833503b2349b4b42c2e80b0aa8c23` |
|CipherTemplateId |String |否 |表示需要與該網域名稱繫結的一個加密策略。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/reference-DescribeTemplates_zh-tw) 獲取您想要繫結的加密策略的 ID。<br><br>如果不指定該參數，表示當前不會將該網域名稱與任何加密策略繫結。 |`tpl-cqgRvW` |
|HTTPSSwitch |String |否 |表示是否為該網域名稱啟用 "HTTPS加密服務"。該參數有以下取值：<br><br><br>* `on`：表示啟用該服務。<br><br>* `off`：表示不啟用該服務。<br><br><br>該參數的預設值是 `off`。 |`on` |
|Project |String |否 |表示該網域名稱所歸屬的專案，預設值是 `default`。 |`default` |
|ServiceRegion |String |否 |表示為該網域名稱啟用的服務區域。該參數有以下取值：<br><br><br>* `outside_chinese_mainland`：表示 "全球（不包含中國大陸）"。<br><br>* `chinese_mainland`：表示 "中國大陸"。<br><br>* `global`：表示 "全球"。<br><br><br>該參數的預設值是 `outside_chinese_mainland`。<br><br>需要留意的是，預設情況下 `chinese_mainland` 和 `global` 是不可用的。要使這兩個服務區域可用，請 [提交工單](https://console.byteplus.com/workorder/create)。同時，由於這兩個區域包含中國大陸，您必須額外完成以下操作：<br><br><br>* 對您的 BytePlus 帳號進行 [實名認證](https://docs.byteplus.com/en/byteplus-platform/docs/real-name-registration)<br><br>* 為您的網域名稱進行 ICP 備案。 |`global` |
|Tags |Object[] |否 |表示一個標籤列表。這些標籤會被新增到 `Domain`。列表中最多可以包含 10 個標籤。標籤是一個鍵值對。 | |
|Key |String |否 |表示列表中一個標籤的 key，長度範圍是 1\-128 個字元。Key 是大小寫敏感的，可以包含 Unicode 字母、Unicode 數字、空格以及以下任意字元：<br><br><br>* _./=+\-@ |`myKey` |
|Value |String |否 |表示該標籤的值，長度範圍是 1\-256 個字元。該參數也是大小寫敏感的，可以包含 Unicode 字母、Unicode 數字、空格以及以下任意字元：<br><br><br>* _./=+\-@ |`myValue` |
|RuleTemplateIds |String[] |否 |表示需要與該網域名稱繫結的一個規則引擎策略。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/reference-DescribeTemplates_zh-tw) 獲取您想要繫結的規則引擎策略的 ID。<br><br>如果不指定該參數，表示當前不會將該網域名稱與任何規則引擎策略繫結。 |`tpl-r18yoko` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|ResourceIds |String[] |表示已增加的網域名稱清單。 |`"www.example.com","img.example.com"]` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=AddTemplateDomain&Version=2021-03-01
{
    "Domain": "www.example.com,img.example.com",
    "CipherTemplateId": "tpl-cqgRvW",
    "HTTPSSwitch": "on",
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceTemplateId": "tpl-s2Q4mq",
    "CertId": "cert-044833503b2349b4b42c2e80b0aa8c23",
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
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2025082209311384D275C0D56FB6A17884",
        "Action": "AddTemplateDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ResourceIds": [
            "www.example.com",
            "img.example.com"
        ]
    }
}
```


&nbsp;
