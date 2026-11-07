---
title: "nest config"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-config-cn-zh-tw"
---

檢視和修改專案設定檔。

<span id="概要"></span>
## 概要

```shell
npx nest config

npx nest config set <parameter> <value>

npx nest config set -g <parameter> <value>
```


<span id="描述"></span>
## 描述

專案設定包含函數專案的工作目錄、入口程式碼檔案目錄、函數專案下所有本地函數的資訊及邊緣 KV 資料等資訊。專案設定可分為函數專案設定和全域專案設定。邊緣函數 CLI 優先從函數專案設定中取得設定。如果取得不到，則從全域專案設定中取得設定。


* `npx nest config set` 用於設定函數專案設定檔中的參數

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">您可以使用全域參數 <code>-c <config_file_path></code> 為當前指令指定一個函數設定檔   </div>
   

* `npx nest config set -g` 用於設定全域專案設定檔中的參數

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">建議您僅在全域專案設定檔中設定以 <code>cloud</code> 開頭的參數，例如 <code>cloud.access_key</code> 和 <code>cloud.secret_key</code>。這些參數是邊緣函數 OpenAPI 服務的相關設定，適用於相同 BytePlus 帳號下的所有函數   </div>
   

您可以透過 `npx nest config` 檢視當前函數專案中生效的邊緣函數 CLI 設定

<span id="子指令"></span>
## 子指令

<span id="set"></span>
### set

修改邊緣函數 CLI 設定的參數，例如 `npx nest config set name example-function`

您可以使用 `-g` 修改邊緣函數 CLI 的全域專案設定檔

<span id="參數描述"></span>
#### 參數描述


|參數 |描述 |
|---|---|
|work_dir |函數專案的工作目錄 |
|src_dir |函數入口程式碼檔案的目錄 |
|output_dir |函數執行程式碼檔案的目錄。您使用 nest debug 或 nest start 執行本地函數時，邊緣函數 CLI 會基於函數入口程式碼檔案在 `output_dir` 中指定的目錄產生一個函數執行程式碼檔案。相比函數入口程式碼檔案，函數執行程式碼檔案會被新增一個立即執行函式（IIFE） |
|cloud.api_server |邊緣函數 OpenAPI 服務 URL。該參數為固定值，您無需修改 |
|cloud.debug_server |邊緣函數 Debugger 服務 URL。該參數為固定值，您無需修改 |
|cloud.api_version |邊緣函數 OpenAPI 服務版本。該參數為固定值，您無需修改 |
|cloud.api_region |邊緣函數 OpenAPI 服務地域。該參數為固定值，您無需修改 |
|cloud.api_timeout |邊緣函數 OpenAPI 逾時時間。預設為5000毫秒 |
|cloud.key_manager_url |BytePlus 控制台的 API 存取金鑰頁面 URL。該參數為固定值，您無需修改 |
|cloud.product |邊緣函數 OpenAPI 產品類型。該參數為固定值，您無需修改 |
|cloud.access_key |您的 BytePlus 帳號的 Access Key ID。您可以從 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)取得 Access Key ID |
|cloud.secret_key |您的 BytePlus 帳號的 Secret Access Key。您可以從 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)取得 Secret Access Key |
|functions.[N].id |專案清單中第 N 個本地函數的 ID |
|functions.[N].name |專案清單中第 N 個本地函數的名稱 |
|functions.[N].type |專案清單中第 N 個本地函數的入口程式碼檔案類型 |
|functions.[N].entry |專案清單中第 N 個本地函數的入口程式碼檔案名稱 |
