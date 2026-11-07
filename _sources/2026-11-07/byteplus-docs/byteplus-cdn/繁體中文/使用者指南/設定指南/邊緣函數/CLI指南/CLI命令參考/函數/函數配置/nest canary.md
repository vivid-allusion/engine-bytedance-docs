---
title: "nest canary"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-canary-cn-zh-tw"
---

管理本地函數的金絲雀環境。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a></div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案</div>


* <div data-tips="true" data-tips-type="tip">本地函數的環境變數不保存在本地。邊緣函數 CLI 在邊緣函數服務端管理本地函數的環境變數。因此，在執行本指令時，請確保您的本地函數需要有一個函數 ID</div>



<span id="子指令"></span>
## 子指令

<span id="list"></span>
### list

```shell
npx nest canary list --canary --continents <continent1,continent2,...> --countries <country1,country2,...> --function <function_id_or_name>
```


取得金絲雀環境中的邊緣節點


* `--canary`：*boolean，optional*

   * 是否僅展示金絲雀環境中的邊緣節點。預設為否

* `<continent1,continent2,...>`：*string，optional*

   * 邊緣節點所在的大洲。多個大洲的名稱之間用英文逗號間隔。例如 `Asia,Europe`

* `<country1,country2,...>`：*string，optional*

   * 邊緣節點所在的國家或地區。多個國家或地區的名稱之間用英文逗號間隔。例如 `China,France`

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`


```shell
$ npx nest canary list
+---------+-----------+--------+
| COUNTRY | CONTINENT | CANARY |
+---------+-----------+--------+
| China   | Asia      | NO     |
+---------+-----------+--------+
```


<span id="add"></span>
### add

```shell
npx nest canary add --countries <country1,country2,...> --function <function_id_or_name>
```


將位於指定國家或地區的邊緣節點新增到金絲雀環境


* `<country1,country2,...>`：*string，required*

   * 邊緣節點所在的國家或地區。多個國家或地區的名稱之間用英文逗號間隔。例如 `China,France`

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`


<span id="delete"></span>
### delete

```shell
npx nest canary delete --countries <country1,country2,...> --function <function_id_or_name>
```


從金絲雀環境中刪除位於指定國家或地區的邊緣節點


* `<country1,country2,...>`：*string，required*

   * 邊緣節點所在的國家或地區。多個國家或地區的名稱之間用英文逗號間隔。例如 `China,France`

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`
