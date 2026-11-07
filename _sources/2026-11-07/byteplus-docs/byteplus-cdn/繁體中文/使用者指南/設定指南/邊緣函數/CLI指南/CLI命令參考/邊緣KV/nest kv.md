---
title: "nest kv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-cn-zh-tw"
---

管理邊緣 KV。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a></div>


* <div data-tips="true" data-tips-type="tip">邊緣 KV 的資料不保存在本地。邊緣函數 CLI 在邊緣函數服務端管理 KV 資料</div>



<span id="nest-kv-namespace"></span>
# nest kv namespace

管理儲存空間

<span id="子指令"></span>
## 子指令

<span id="list"></span>
### list

```shell
npx nest kv namespace list --page <page_number> --desc
```


取得儲存空間清單


* `<page_number>`：*integer，optional*

   * 清單分頁顯示的頁碼。預設為 1

* `--desc`：*boolean，optional*

   * 按儲存空間 ID 降冪排序。預設為按儲存空間 ID 升冪排序


```shell
$ npx nest kv namespace list
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
|                   ID:NAME                   |          REGION          |             PROJECT              |                            DESCRIPTION                            |     CREATETIME      |
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
| 24629043532424120990:ns                     | Outside Chinese Mainland | default                          | more updates                                                      | 2024-12-30 15:21:07 |
| 25540045541653372777:abtest_config          | Outside Chinese Mainland | default                          | testq                                                             | 2025-01-17 17:13:10 |
| 7758139412787918608:gochina                 | Outside Chinese Mainland | default                          |                                                                   | 2025-06-13 18:45:07 |
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
```


<span id="create"></span>
### create

```shell
npx nest kv namespace create <name> -d <description> -p <project>
```


建立一個儲存空間


* `<name>`：*string，required*

   * 儲存空間的名稱

* `<description>`：*string，optional*

   * 儲存空間的描述

* `<project>`：*string，optional*

   * 儲存空間所屬的專案。預設為 `default`


```shell
$ npx nest kv namespace create new12345
New namespace "new12345" created!
```


<span id="update"></span>
### update

```shell
npx nest kv namespace update <id:name> -d <description> 
```


更新指定的儲存空間描述


* `<id:name>`：*string，required*

   * 儲存空間的 ID 和名稱。格式為 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以透過 `npx nest kv namespace list` 取得儲存空間的 ID 和名稱

* `<description>`：*string，optional*

   * 儲存空間的描述


```shell
$ npx nest kv namespace update 1677061481998840412:new12345  -d "more updates"
[1677061481998840412:new12345]
>>> the desc is more updates
Namespace 1677061481998840412:new12345 updated!
```


<span id="delete"></span>
### delete

```shell
npx nest kv namespace delete <id:name>
```


刪除指定的儲存空間


* `<id:name>`：*string，required*

   * 儲存空間的 ID 和名稱。格式為 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以透過 `npx nest kv namespace list` 取得儲存空間的 ID 和名稱


<span id="nest-kv-keys"></span>
# nest kv keys

取得指定儲存空間的鍵值對清單

```shell
nest kv keys --namespace <id:name>
```



* `<id:name>`：*string，required*

   * 儲存空間的 ID 和名稱。格式為 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以透過 `npx nest kv namespace list` 取得儲存空間的 ID 和名稱


<span id="nest-kv-set"></span>
# nest kv set

```shell
nest kv set --namespace <id:name> <key> <value> --ttl <ttl>

nest kv set --namespace <id:name> <key> --file <file_path> --ttl <ttl>
```


新增或更新鍵值對


* `<id:name>`：*string，required*

   * 儲存空間的 ID 和名稱。格式為 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以透過 `npx nest kv namespace list` 取得儲存空間的 ID 和名稱

* `<key>`：*string，required*

   * 鍵值對的鍵

* `<value>`：*string，optional*

   * 鍵值對的值。您至少需要設定 `<value>` 和 `<file_path>` 其中一個

* `<ttl>`：*string，optional*

   * 鍵值對的過期時間。單位為秒。預設為永不過期

* `<file_path>`：*string，optional*

   * 檔案路徑。該檔案的內容將作為鍵值對的值。您至少需要設定 `<value>` 和 `<file_path>` 其中一個


<span id="nest-kv-delete"></span>
# nest kv delete

```shell
nest kv delete --namespace <id:name> <key>
```


刪除指定的鍵值對


* `<id:name>`：*string，required*

   * 儲存空間的 ID 和名稱。格式為 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以透過 `npx nest kv namespace list` 取得儲存空間的 ID 和名稱

* `<key>`：*string，required*

   * 鍵值對的鍵


<span id="nest-kv-get"></span>
# nest kv get

```shell
nest kv get --namespace <id:name> <key> --save-dev --no-decode
```


取得鍵值對的值


* `<id:name>`：*string，required*

   * 儲存空間的 ID 和名稱。格式為 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以透過 `npx nest kv namespace list` 取得儲存空間的 ID 和名稱

* `<key>`：*string，required*

   * 鍵值對的鍵

* `--save-dev`：*boolean，optional*

   * 將鍵值對保存到本地用於偵錯。預設不保存

* `--no-decode`：*boolean，optional*

   * 直接以 base64 編碼格式列印鍵值對的值。預設列印 base64 解碼後的值。如果您的鍵值對的值是二進位類型，為了避免列印的內容顯示為亂碼，您可以使用 `--no-decode` 列印值的 base64 編碼
