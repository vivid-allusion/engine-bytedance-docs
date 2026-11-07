---
title: "nest versions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-version-cn-zh-tw"
---

取得本地函數程式碼已發佈的版本。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a></div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案</div>


* <div data-tips="true" data-tips-type="tip">本地函數的發佈歷史不保存在本地。邊緣函數 CLI 在邊緣函數服務端管理本地函數的發佈歷史。因此，在執行本指令時，請確保您的本地函數需要有一個函數 ID</div>



<span id="子指令"></span>
## 子指令

<span id="list"></span>
### list

```shell
npx nest versions list --function <function_id_or_name> --page <page_number>
```


查看本地函數已發佈的程式碼版本清單


* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`

* `<page_number>`：*integer，optional*

   * 清單分頁顯示的頁碼。預設為 1


```shell
$ npx nest versions list
+---------+------+------------+-------------+----------------------+------------------+---------------------+
| VERSION | TYPE |   STATUS   | DESCRIPTION |       CREATOR        | PREVIOUS VERSION |     CREATETIME      |
+---------+------+------------+-------------+----------------------+------------------+---------------------+
| 1.0.2   | Full | Publishing |             | ******************** | 1.0.1            | 2025-01-08 17:35:40 |
| 1.0.1   | Full | Success    |             | ******************** |                  | 2025-01-08 00:55:42 |
+---------+------+------------+-------------+----------------------+------------------+---------------------+
```


<span id="view"></span>
### view

```shell
npx nest versions view <version> -f <function_id>
```


查看指定版本的函數程式碼


* `<version>`：*string，required*

   * 函數程式碼的版本。您可以透過 `npx nest versions list` 取得函數程式碼的版本

* `<function_id>`：*string，optional*

   * 函數 ID。預設為當前本地函數的函數 ID


```shell
$ npx nest versions view 1.0.1
/**
 * Add the necessary event listener
 * @param {Event} fetch event, {Function} async function
 */
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
})

/**
 * Make a response to client
 * @param {Request} request
 */
async function handleRequest(request) {
  return new Response('Hello World!', { status: 200 });
}
```
