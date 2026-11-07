---
title: "CLI概覽"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-function-cli-overview-cn-zh-tw"
---

除了控制台和 OpenAPI 之外，您還可以使用邊緣函數 CLI 管理函數和邊緣 KV。與控制台和 OpenAPI 相比，邊緣函數 CLI 還支援以下額外功能：


* 建立一個或多個本地函數

* 編輯和偵錯本地函數程式碼

* 對一個或多個本地函數進行增刪改查和發佈操作

* 同步本地函數與遠端函數


邊緣函數 CLI 使您可以在本地編寫和偵錯函數程式碼，並把本地的函數程式碼發佈到邊緣函數服務端。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ce10bdc6fec1bd4a8f76370054340caa.png) </span>

<span id="基本概念"></span>
## 基本概念

在使用邊緣函數 CLI 之前，建議您先了解下面的基本概念。

<span id="遠端函數"></span>
### 遠端函數

您在邊緣函數服務端建立的函數。每個遠端函數都有一個函數 ID 作為該函數的唯一識別碼。

<span id="本地函數"></span>
### 本地函數

您在函數專案中建立的函數。本地函數可以沒有函數 ID。您可以為本地函數關聯一個遠端函數的函數 ID。

<span id="函數專案"></span>
### 函數專案

包含函數專案設定檔（nest.json）的 Node.js 專案，用於管理本地函數。您使用 [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw) 建立一個函數專案。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 還會在該函數專案中建立一個本地函數。</div>


一個函數專案可以包含一個或多個本地函數，但只能有一個本地函數是預設函數。您可以使用 [nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#create) 在函數專案中建立一個本地函數。

<span id="專案設定"></span>
### 專案設定

專案設定包含了函數專案的工作目錄、入口程式碼檔案目錄、函數專案下所有本地函數的資訊及邊緣 KV 資料等資訊。專案設定可以被分類為函數專案設定和全域專案設定。


* **函數專案設定**：儲存在每個函數專案根目錄下的 `nest.json` 檔案。函數專案設定檔適用於當前專案。

* **全域專案設定**：儲存在 `~/.nest.json` 檔案。全域專案設定檔適用於所有函數專案。


邊緣函數 CLI 優先從函數專案設定檔中獲取專案設定。如果專案設定獲取失敗，邊緣函數 CLI 從全域專案設定檔中獲取專案設定。
