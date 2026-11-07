---
title: "nest rollback"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-rollback-cn-zh-tw"
---

將本地函數的程式碼回滾到您指定的版本。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a></div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案</div>


* <div data-tips="true" data-tips-type="tip">本地函數的發佈歷史不保存在本地。邊緣函數 CLI 在邊緣函數服務端管理本地函數的發佈歷史。因此，在執行本指令時，請確保您的本地函數需要有一個函數 ID</div>



<span id="概述"></span>
## 概述

```shell
npx nest rollback <version> --canary -d <description> -f <function_id> 
```


<span id="描述"></span>
## 描述


* `<version>`：*string，required*

   * 函數程式碼的版本。您可以透過 [nest versions](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-version-cn-zh-tw) 取得函數程式碼的版本

* `--canary`：*boolean，optional*

   * 回滾的程式碼僅發佈到金絲雀環境。預設為全量環境

* `<description>`：*string，optional*

   * 版本描述

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`
