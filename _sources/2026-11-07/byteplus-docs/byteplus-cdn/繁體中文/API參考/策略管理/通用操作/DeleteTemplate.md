---
title: "DeleteTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DeleteTemplate_zh-tw"
---

刪除一個策略或者策略的某個版本。

**刪除策略**

如果一個策略被刪除，該策略的所有版本都會被刪除。

要刪除一個策略，該策略必須未綁定任何網域。您可以呼叫 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw) 了解一個策略是否已與某個網域綁定。只有當該策略的 `BoundDomains` 是 `null` 時，您才可以刪除該策略。

假設一個策略已綁定了一個或者多個網域。如果您需要將其與這些網域解綁，請參見 [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateTemplateDomain_zh-tw) 中的相關描述。

**刪除策略的版本**

您只能刪除未發布的策略版本，也就是說，您只能刪除策略下 `Status` 為 `draft` 或者 `stop` 的版本。要獲取策略下的所有版本以及每個版本的狀態，請參見 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-tw)。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DeleteTemplate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DeleteTemplate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要刪除的策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw) 取得您想要刪除的策略的 ID。 |`tpl-s2N4rW` |
|TemplateVersion |String |否 |表示要刪除的版本。該版本的狀態不能是 `running`。<br><br>您可以呼叫 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-tw) 獲取該策略下的所有的版本以及版本的狀態。 |`P-250414.89520` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DeleteTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-sqdYQ2",
    "TemplateVersion": "P-250414.89520"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202508251227583CD38EED31C8FCA7FF07",
        "Action": "DeleteTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
