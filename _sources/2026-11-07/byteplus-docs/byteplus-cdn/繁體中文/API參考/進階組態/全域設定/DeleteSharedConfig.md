---
title: "DeleteSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DeleteSharedConfig_zh-tw"
---

刪除一個已有的全域設定。

<span id="前提條件"></span>
## 前提條件

在刪除一個全域設定前，請確保其未與任何網域名稱關聯。要刪除一個全域設定，參照以下步驟：


1. 調用 [DescribeDomainShared](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeDomainShared_zh-tw) 獲取該全域設定關聯的網域名稱。

2. 對於與該全域設定關聯的**每個**網域名稱，執行以下步驟：

   1. 調用 [DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DuplicateTemplate_zh-tw) 複製與網域名稱綁定的分發策略。

   2. 對於新建立的策略，調用 [UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateServiceTemplate_zh-tw) 對該策略進行修改，確保相關的 CDN 功能設定中沒有引用該全域設定。您可以參考 [全域設定](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_zh-tw) 了解可以引用全域設定的那些 CDN 功能。

   3. 調用 [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-UpdateTemplateDomain_zh-tw) 將新建立的分發策略與該網域名稱綁定。

3. 調用 DeleteSharedConfig 刪除該全域設定。


如果子帳戶在調用該 API 時收到了 `該設定存在關聯網域名稱，不允許刪除` 的錯誤，並且子帳戶調用 [DescribeDomainShared](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeDomainShared_zh-tw) 時並未發現任何關聯的網域名稱，那麼有可能子帳戶沒有權限訪問該全域設定所關聯的網域名稱。在這個情況下，需要主帳戶來解除該全域設定與網域名稱的關聯，然後子帳戶就可以刪除該全域設定了。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DeleteSharedConfig&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DeleteSharedConfig`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ConfigName |String |是 |表示一個全域設定的名稱。參見 [前提條件](https://docs.byteplus.com/en/docs/18/36630#%E5%89%8D%E6%8F%90%E6%A2%9D%E4%BB%B6)。 |`my_list` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DeleteSharedConfig&Version=2021-03-01
{
    "ConfigName": "my_list"
}
```


&nbsp;
