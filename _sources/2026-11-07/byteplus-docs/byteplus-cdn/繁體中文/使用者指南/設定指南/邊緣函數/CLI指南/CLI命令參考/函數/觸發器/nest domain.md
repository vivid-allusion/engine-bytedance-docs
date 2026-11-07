---
title: "nest domain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-cn-zh-tw"
---

管理本地函數關聯的網域名稱。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a></div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案</div>


* <div data-tips="true" data-tips-type="tip">本地函數所關聯的網域名稱資訊不保存在本地。邊緣函數 CLI 在邊緣函數服務端管理本地函數關聯的網域名稱。因此，在執行本指令時，請確保您的本地函數需要有一個函數 ID</div>



<span id="描述"></span>
## 描述

當使用者透過 HTTP 或 HTTPS 請求存取函數關聯的網域名稱，且使用者請求與網域名稱的轉發規則匹配時，網域名稱觸發器會觸發函數程式碼中的 fetch 事件。您需要在程式碼中監聽並處理 fetch 事件

一個函數可以關聯一個或多個網域名稱。每個網域名稱也可以關聯多個函數。參見 [使用限制](https://docs.byteplus.com/docs/byteplus-cdn/functions-usage-limits-zh-tw)

<span id="子指令"></span>
## 子指令

<span id="list"></span>
### list

```shell
npx nest domain list --all --function <function_id> -page <page_number> --desc
```


查看本地函數關聯的網域名稱


* `--all`：*boolean，optional*

   * 查看所有網域名稱。預設僅查看本地函數已關聯的網域名稱

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`

* `<page_number>`：*integer，optional*

   * 清單分頁顯示的頁碼。預設為 1

* `--desc`：*boolean，optional*

   * 按網域名稱降冪排序。預設為按網域名稱升冪排序


您執行 `npx nest domain list` 後，可以查看網域名稱、狀態和轉發規則的資訊

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
| a.example.com               | Online | directory | /welcome/ | false      |
+-----------------------------+--------+-----------+-----------+------------+
```


您執行 `npx nest domain list --all` 後，可以在 STATUS 欄查看網域名稱是否可以被函數關聯

```shell
$ npx nest domain list --all

+--------------------------------------+-----------------+
|                DOMAIN                |     STATUS      |
+--------------------------------------+-----------------+
| a.example.com                        | Can be Bound    |
| a.example.org                        | Cannot be Bound |
+--------------------------------------+-----------------+
```


<span id="bind"></span>
### bind

```shell
npx nest domain bind <domain_name> --function <function_id> --url-directory <url_directory> --ignore-case

npx nest domain bind <domain_name> --function <function_id> --url-ext <url_ext> --ignore-case

npx nest domain bind <domain_name> --function <function_id> --url-match <url> --ignore-case
```


為本地函數關聯一個網域名稱

您可以使用以下參數為網域名稱設定轉發規則。只有匹配轉發規則的使用者請求才能被轉發到邊緣函數。參見 [網域名稱觸發器](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-domain-triggers-cn-zh-tw) 了解如何設定轉發規則


* `<domain_name>`：*string，required*

   * 網域名稱

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`

* `<url_directory>`：*string，optional*

   * 規則類型是 URL 目錄。規則應用於指定目錄下的所有檔案。您必須設定 `<url_directory>`、`<url_ext>` 或 `<url>` 其中之一

* `<url_ext>`：*string，optional*

   * 規則類型是檔案副檔名。規則應用於具有指定副檔名的所有檔案。您必須設定 `<url_directory>`、`<url_ext>` 或 `<url>` 其中之一

* `<url>`：*string，optional*

   * 規則類型是 URL 完整路徑。規則應用於指定檔案。您必須設定 `<url_directory>`、`<url_ext>` 或 `<url>` 其中之一

* `--ignore-case`：*boolean，optional*

   * 忽略大小寫。預設不忽略大小寫


例如，下面的指令為本地函數關聯網域名稱 `www.example.com`，並將轉發規則的類型設定為 URL 目錄。如果使用者請求的 URL 目錄是 `/welcome/`，例如 `https://www.example.com/welcome/a.png`，則該請求匹配轉發規則

```shell
npx nest domain bind www.example.com --url-directory /welcome/
```


您可以執行 `npx nest domain list` 查看網域名稱是否被關聯

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
| www.example.com             | Online | directory | /welcome/ | false      |
+-----------------------------+--------+-----------+-----------+------------+
```


<span id="unbind"></span>
### unbind

```shell
npx nest domain unbind <domain_name> --function <function_id>
```


將網域名稱與本地函數取消關聯


* `<domain_name>`：*string，required*

   * 需要取消關聯的網域名稱

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`


您可以執行 `npx nest domain list` 查看網域名稱是否被取消關聯

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
+-----------------------------+--------+-----------+-----------+------------+
```
