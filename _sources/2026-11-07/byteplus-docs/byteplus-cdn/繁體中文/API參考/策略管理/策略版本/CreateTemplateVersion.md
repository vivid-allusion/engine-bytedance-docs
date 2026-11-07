---
title: "CreateTemplateVersion"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateTemplateVersion_zh-tw"
---

為策略建立一個草稿版本。


* 預設情況下，該 API 會基於目前已發布的版本來建立草稿版本，對應控制台上的「建立版本」操作。建立的草稿版本與目前已發布的版本具有相同的設定。

* 您也可以指定一個現有版本來建立一個草稿版本，對應控制台上的「複製版本」操作。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您不能對一個已包含草稿版本的策略呼叫該 API。</div>


<div data-tips="true" data-tips-type="tip">要判斷指定的策略是否包含草稿版本，您可以對指定的策略呼叫 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-tw">DescribeTemplateReleaseVersions</a>。在 API 返回的版本清單中，查看 <code>Status</code> 為 <code>draft</code> 的版本是否存在。</div>


<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=CreateTemplateVersion&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `CreateTemplateVersion`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示需要建立草稿版本的策略 ID。 |`tpl-s18ynd9` |
|Message |String |否 |表示該草稿版本的描述。 |`my desc` |
|ReferredVersion |String |否 |表示一個現有版本的 ID，該 API 基於該版本而建立草稿版本。<br><br>該參數的值不能是 `draft`，預設值是目前發布版本的 ID。<br><br>您可以呼叫 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-tw) 獲取該策略下的所有版本。 |`P-250414.89520` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=CreateTemplateVersion&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "Message": "Hello World",
    "ReferredVersion": "P-250414.89520"
}
```


&nbsp;
