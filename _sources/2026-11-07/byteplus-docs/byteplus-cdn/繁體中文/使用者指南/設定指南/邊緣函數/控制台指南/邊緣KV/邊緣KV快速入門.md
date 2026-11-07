---
title: "邊緣KV快速入門"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-EdgeKV-overview-cn-zh-tw"
---

本教學基於簡單的示例場景介紹如何在邊緣函數中使用邊緣 KV。

邊緣 KV 服務是在 BytePlus 的全球邊緣伺服器上的分散式鍵值儲存服務。一個鍵值對透過邊緣函數控制台、OpenAPI 或執行時期 API 被寫入邊緣 KV 後，會自動被同步到所有邊緣伺服器。函數透過執行時期 API 可以快速讀取位於同邊緣伺服器的鍵值對。

<span id="示例場景"></span>
## 示例場景

您的網站支援 A/B 測試功能，可以根據用戶端的地理位置返回不同版本的網頁。版本切換的配置資訊儲存在邊緣 KV 中。您希望可以從函數的程式碼中讀取版本切換的配置資訊。在本教學中，假設配置資訊如下：

```json
{
  "us": "versionA",
  "eu": "versionB",
  "asia": "versionA"
}
```


<span id="操作步驟"></span>
## 操作步驟

您需要完成以下步驟實現示例場景。


1. 建立一個儲存空間。

2. 在儲存空間中建立一個鍵值對。

3. 在函數程式碼中讀取鍵值對的值。


<span id="步驟一：建立一個儲存空間"></span>
### 步驟一：建立一個儲存空間

參見以下步驟建立一個儲存空間。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您只能使用控制台、OpenAPI 或 CLI 建立儲存空間。您無法使用執行時期 API 建立儲存空間。</div>



1. 開啟 [邊緣KV](https://console.byteplus.com/cdn/edge-function/list) 頁面。

2. 在 **邊緣KV** 頁面，點擊 **建立儲存空間**。

3. 在 **建立儲存空間** 對話方塊中，設定以下參數，然後點擊 **儲存** 。

   
   |參數 |描述 |
   |---|---|
   |名稱 |設定為 `abtest_config`。 |
   |描述 |設定為 `demo`。 |
   |專案 |設定為 `default`。 |
   


<span id="步驟二：在儲存空間中建立一個鍵值對"></span>
### 步驟二：在儲存空間中建立一個鍵值對

參見以下步驟在儲存空間中建立一個鍵值對。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以使用控制台、OpenAPI 或執行時期 API 建立鍵值對。</div>



1. 開啟 [邊緣KV](https://console.byteplus.com/cdn/edge-function/list) 頁面。

2. 找到您建立的 `abtest_config` 儲存空間，點擊該儲存空間的名稱。

3. 點擊 **新增資料**。

4. 在彈出的 **新增資料** 對話方塊中，設定資料的相關參數，然後點擊 **儲存**。

   
   |參數 |描述 |
   |---|---|
   |鍵 |設定為 `config_key`。 |
   |值 |設定為示例場景中的 JSON 值 `{"us":"versionA","eu":"versionB","asia":"versionA"}`。 |
   |TTL |設定為 **永久儲存**。 |
   


<span id="步驟三：在函數程式碼中讀取鍵值對的值"></span>
### 步驟三：在函數程式碼中讀取鍵值對的值

參見以下步驟在函數程式碼中讀取鍵值對的值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以使用控制台、OpenAPI 或執行時期 API 讀取鍵值對的值。</div>


在函數程式碼中，您呼叫 [KV.get()](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-EdgeKV-RuntimeAPI-cn-zh-tw) 獲取鍵值對的值。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">邊緣函數的偵錯環境暫不支援執行 <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-EdgeKV-RuntimeAPI-cn-zh-tw">邊緣 KV 的執行時期 API</a>。邊緣 KV 的執行時期 API 只能在正式環境執行。</div>


```JavaScript
const config = await KV.get("abtest_config","config_key",{type:"string"});
```
