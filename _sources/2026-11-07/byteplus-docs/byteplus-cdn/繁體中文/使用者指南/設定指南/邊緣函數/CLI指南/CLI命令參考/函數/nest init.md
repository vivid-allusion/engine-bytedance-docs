---
title: "nest init"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw"
---

在目前目錄建立一個函數專案並在函數專案中建立一個本地函數。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您無需設定 Access Key ID 和 Secret Access Key 就可以執行本指令。</div>


<span id="概要"></span>
## 概要

```shell
npx nest init <dir> --env --sync --function <function_id>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您也可以直接執行以下指令快速安裝邊緣函數 CLI 並建立本地函數。執行以下指令前無需安裝邊緣函數 CLI。</div>


<div data-tips="true" data-tips-type="tip">```shell
npx @byteplus/nest init --env --sync --function <function_id>
```
</div>


<div data-tips="true" data-tips-type="tip">該指令依序執行以下操作：</div>



1. <div data-tips="true" data-tips-type="tip">在目前目錄建立一個 Node.js 專案</div>


2. <div data-tips="true" data-tips-type="tip">在 Node.js 專案中安裝邊緣函數 CLI</div>


3. <div data-tips="true" data-tips-type="tip">執行邊緣函數 CLI 在目前目錄建立一個函數專案並在函數專案中建立一個本地函數</div>



<span id="描述"></span>
## 描述

npx 指令會在您執行 `npx nest init` 的目錄建立一個函數專案，然後提示您輸入函數名稱、選擇函數範本、入口檔案的位置和名稱、所屬 BytePlus 專案、函數描述等資訊。然後，邊緣函數 CLI 會根據您輸入的資訊建立一個本地函數。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">每個 BytePlus 帳號下的函數名稱需唯一。名稱的規則如下：</div>


   * <div data-tips="true" data-tips-type="tip">支援英文字母、數字和連字號（\-）</div>


   * <div data-tips="true" data-tips-type="tip">長度不超過 128 個字元</div>


* <div data-tips="true" data-tips-type="tip">您可以選擇的函數範本取決於您是否設定了 Access Key ID 和 Secret Access Key：</div>


   * <div data-tips="true" data-tips-type="tip">如果您沒有設定 Access Key ID 和 Secret Access Key，您只能使用 HelloWorld 範本</div>


   * <div data-tips="true" data-tips-type="tip">如果您設定了 Access Key ID 和 Secret Access Key ，您可以使用邊緣函數支援的所有範本</div>


* `<dir>`: *string，optional*

* 函數專案的建立目錄。預設為目前目錄。

* `--sync`：*boolean，optional*

   * 建立一個與當前專案關聯的遠端函數。預設不建立遠端函數

* `<function_id>`：*string，optional*

   * 遠端函數的函數 ID。如果您需要將本地函數與遠端函數關聯，可以透過該參數設定遠端函數的函數 ID

* `--env`：*boolean，optional*

   * 將 `<function_id>` 對應的遠端函數的環境變數同步到本地。預設不同步遠端函數的環境變數


一個函數專案下可以有多個本地函數。如果您需要在函數專案中建立新的本地函數，可以使用 [nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#create) 指令。
