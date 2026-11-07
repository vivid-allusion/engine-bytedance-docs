---
title: "DuplicateTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DuplicateTemplate_zh-tw"
---

透過複製一個已有策略來建立一個配置相同、類型相同的策略。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DuplicateTemplate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DuplicateTemplate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ReferredTemplateId |String |是 |表示一個待複製的策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw) 取得您想要複製的策略的 ID。 |`tpl-sZRpwq` |
|Message |String |否 |表示建立的策略的描述，長度不能超過 120 個字元。 |`This is a dup policy.` |
|Title |String |否 |表示建立的策略的名稱，長度不能超過 100 個字元。<br><br>如果該參數未指定，CDN 會產生一個隨機名稱。 |`Dup_Policy` |
|Project |String |否 |表示建立的策略所歸屬的專案。<br><br>該參數的預設值是 `default`，表示 Default 專案。 |`default` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|TemplateId |String |表示建立的策略的 ID。 |`tpl-s2N4rW` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DuplicateTemplate&Version=2021-03-01
{
    "ReferredTemplateId": "tpl-sZRpwq",
    "Title": "Dup_Policy",
    "Message": "This is a dup policy."
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2024030403552737EB957CFE0697DBB981",
        "Action": "DuplicateTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TemplateId": "tpl-s2N4rW"
    }
}
```


&nbsp;
