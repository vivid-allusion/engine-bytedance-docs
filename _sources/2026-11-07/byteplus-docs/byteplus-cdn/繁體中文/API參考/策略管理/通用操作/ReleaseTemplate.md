---
title: "ReleaseTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ReleaseTemplate_zh-tw"
---

發布一個策略的指定版本。


* 如果待發布版本的狀態是 `draft`，該 API 操作對應控制台上的「發布」操作。

* 如果待發布版本的狀態是 `stop`，該 API 操作對應控制台上的「回復」操作。


<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=ReleaseTemplate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `ReleaseTemplate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示要發布的版本所在的策略 ID。 |`tpl-s18ynd9` |
|Env |String |否 |表示發布環境。目前，該參數值只能是 `prod`，表示線上環境。該參數的預設值也是 `prod`。 |`prod` |
|Message |String |否 |表示發布操作的描述。 |`My Desc` |
|TemplateVersion |String |否 |表示待發布的版本號。該參數的預設值是 `draft`。 |`P-250411.16282` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=ReleaseTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "TemplateVersion": "P-250411.16282"
}
```


&nbsp;
