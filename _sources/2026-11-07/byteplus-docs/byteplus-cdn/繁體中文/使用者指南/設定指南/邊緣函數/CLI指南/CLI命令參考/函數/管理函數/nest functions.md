---
title: "nest functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw"
---

對本地函數或遠端函數進行新增/刪除/修改/查詢操作。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案。</div>



<span id="子指令"></span>
## 子指令

<span id="get"></span>
### get

```shell
npx nest functions get <function_id_or_name> 

npx nest functions get --remote <function_id> 
```


取得本地函數或遠端函數的資訊。


* `<function_id_or_name>`：*string，required*

   * 本地函數的 ID 或名稱

* `--remote`：*boolean，optional*

   * 取得遠端函數的資訊。預設取得本地函數的資訊：

      * 您可以透過 `<function_id>` 或 `<function_name>` 取得本地函數的資訊

      * 您只能透過 `<function_id>` 取得遠端函數的資訊


<span id="list"></span>
### list

```shell
npx nest functions list --page <page_number> --desc -s <status> --remote
```


取得函數清單。


* `<page_number>`：*integer，optional*

   * 清單分頁顯示的頁碼。預設為 1

* `--desc`：*boolean，optional*

   * 按函數 ID 降冪排序。預設為按函數 ID 升冪排序

* `<status>`：*string，optional*

   * 函數的狀態：

      * running：運行中

      * unassociated：未關聯網域名稱

      * configuring：設定中

* `--remote`：*boolean，optional*

   * 清單僅包含遠端函數。預設僅包含本地函數


```shell
npx nest functions list
+----+------+------+--------------+--------------------------+---------+-------------+---------+
| ID | NAME | TYPE |    ENTRY     |          REGION          | PROJECT | DESCRIPTION | DEFAULT |
+----+------+------+--------------+--------------------------+---------+-------------+---------+
|    | test | js   | src/index.js | Outside Chinese Mainland |         |             | true    |
+----+------+------+--------------+--------------------------+---------+-------------+---------+
```


<span id="create"></span>
### create

```shell
npx nest functions create --name <function_name> --description <function_description> --entry <path_to_entry_file> --project <project> --sync
```


在函數專案中建立一個函數。您執行該指令時，邊緣函數 CLI 會提示您輸入函數名稱、選擇函數範本、入口檔案的位置和名稱、所屬 BytePlus 專案、函數描述等資訊。然後，邊緣函數 CLI 會根據您輸入的資訊建立一個本地函數。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">每個 BytePlus 帳號下的函數名稱需唯一。名稱的規則如下：</div>


   * <div data-tips="true" data-tips-type="tip">支援英文字母、數字和連字號(\-)</div>


   * <div data-tips="true" data-tips-type="tip">長度不超過 128 個字元</div>


* <div data-tips="true" data-tips-type="tip">您可以選擇的函數範本取決於您是否設定了 Access Key ID 和 Secret Access Key：</div>


   * <div data-tips="true" data-tips-type="tip">如果您沒有設定 Access Key ID 和 Secret Access Key，您只能使用 HelloWorld 範本</div>


   * <div data-tips="true" data-tips-type="tip">如果您設定了 Access Key ID 和 Secret Access Key ，您可以使用邊緣函數支援的所有範本</div>


* `<function_name>`：*string，required*

   * 函數名稱

* `<function_description>`：*string，optional*

   * 函數描述

* `<path_to_entry_file>`：*string，required*

   * 入口檔案的路徑。入口檔案是本地函數執行的起點。該參數指定的入口檔案必須存在

* `<project>`：*string，optional*

   * 函數所屬的專案。預設為 `default`

* `--sync`：*boolean，optional*

   * 同時建立對應的遠端函數。預設不建立對應的遠端函數


```shell
$ npx nest functions create --name test0111 --entry src/index.js
==> [info]: Creating a new function test0111 locally.✔
```


<span id="update"></span>
### update

```shell
npx nest functions update <function_id_or_name> --new-name <new_function_name> --new-description <new_function_description> --new-id <new_function_id> --new-entry <path_to_entry_file> --sync
```


按函數 ID 或名稱修改函數名稱和描述。


* `<function_id_or_name>`：*string，required*

   * 本地函數的 ID 或名稱

* `<new_function_name>`：*string，optional*

   * 新的函數名稱

* `<new_function_description>`：*string，optional*

   * 新的函數描述

* `<path_to_entry_file>`：*string，optional*

   * 入口檔案的路徑。入口檔案是本地函數執行的起點。預設為專案設定檔中的入口檔案路徑

* `--sync`：*boolean，optional*

   * 同時更新對應的遠端函數。預設不更新對應的遠端函數

* `--default`：*boolean，optional*

   * 將本函數設為預設函數。預設不將本函數設為預設函數。在一個函數專案中，預設函數只能有一個

* `<new_function_id>`：*boolean，optional*

   * 新的函數 ID


<span id="pull"></span>
### pull

```shell
npx nest functions pull <function_id> --env
```


將遠端函數的程式碼同步到本地函數。


* `<function_id>`：*string，required*

   * 函數 ID

* `--env`：*boolean，optional*

   * 將遠端函數的環境變數同步到本地函數。預設不同步遠端函數的環境變數


<span id="delete"></span>
### delete

```shell
npx nest functions delete <function_id> --sync
```


按函數 ID 刪除本地函數。該指令會刪除專案設定檔中 `functions` 欄位下關於指定函數 ID 的設定資訊，但不會刪除本地函數的程式碼。


* `<function_id>`：*string，required*

   * 函數 ID

* `--sync`：*boolean，optional*

   * 同時刪除對應的遠端函數。預設不刪除對應的遠端函數
