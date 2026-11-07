---
title: "nest upload"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-upload-cn-zh-tw"
---

將本地函數的程式碼上傳到遠端函數。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案。</div>



<span id="概要"></span>
## 概要

```shell
npx nest upload --no-build --create --function <function_id_or_name>
```


<span id="描述"></span>
## 描述


* `--no-build`：*boolean，optional*

   * 關閉最小化處理。邊緣函數 CLI 預設會對程式碼自動進行最小化處理

* `--create`：*boolean，optional*

   * 建立一個新的遠端函數。預設不建立新的遠端函數

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的函數還沒有函數 ID，邊緣函數 CLI 會提示您是否建立一個新的遠端函數
