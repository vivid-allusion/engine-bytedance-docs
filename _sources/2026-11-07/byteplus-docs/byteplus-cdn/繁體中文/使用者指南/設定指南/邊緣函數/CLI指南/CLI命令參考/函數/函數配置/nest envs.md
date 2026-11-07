---
title: "nest envs"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-env-cn-zh-tw"
---

管理本地函數的環境變數。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a></div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案</div>


* <div data-tips="true" data-tips-type="tip">本地函數的環境變數不保存在本地。邊緣函數 CLI 在邊緣函數服務端管理本地函數的環境變數。因此，在執行本指令時，請確保您的本地函數需要有一個函數 ID</div>



<span id="子指令"></span>
## 子指令

<span id="list"></span>
### list

```shell
npx nest envs list --function <function_ID_or_name> --save-dev
```


取得本地函數的環境變數清單


* `<function_id>`：*string，optional*

   * 函數 ID。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數

* `<--save-dev>`：*boolean，optional*

   * 是否把環境變數保存到本地用於偵錯。預設不保存到本地


```shell
$ npx nest envs list
+------+--------+
| KEY  | VALUE  |
+------+--------+
| key1 | value1 |
| key2 | value2 |
+------+--------+
```


<span id="set"></span>
### set

```shell
npx nest envs set <key> <value> --function <function_id_or_name>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您對環境變數的增刪改操作在函數被再次發佈後才會生效</div>


設定環境變數的值


* `<key>`：*string，required*

   * 環境變數的鍵

* `<value>`：*string，required*

   * 環境變數的值

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`


<span id="delete"></span>
### delete

```shell
npx nest envs set <key> --function <function_id_or_name>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您對環境變數的增刪改操作在函數被再次發佈後才會生效</div>


刪除環境變數


* `<key>`：*string，required*

   * 環境變數的鍵

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`
