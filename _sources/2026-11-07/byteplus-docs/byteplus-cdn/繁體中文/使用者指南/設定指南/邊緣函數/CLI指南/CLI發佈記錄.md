---
title: "CLI發佈記錄"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-release-notes-cn-zh-tw"
---

本文檔包含邊緣函數 CLI 的發佈記錄。

<span id="v1-3-0"></span>
## v1.3.0

此版本發布於 2025 年 11 月 28 日。

<span id="新增功能"></span>
### 新增功能

<span id="支援-pages-cli"></span>
#### 支援 Pages CLI

邊緣函數 Pages 為 BytePlus 邊緣函數所提供的靜態頁面託管服務，旨在協助開發者快速、高效地將靜態網站部署至全球邊緣節點網路。目前，您可以透過邊緣函數 CLI 使用邊緣函數 Pages。請參見 [nest pages](https://docs.byteplus.com/en/docs/byteplus-cdn/nest_pages_zh-tw)。

<span id="v1-2-0"></span>
## v1.2.0

このバージョンは 2025 年 7 月 16 日にリリースされました。

<span id="新機能"></span>
### 新機能

<span id="opaをサポートする関数プロジェクト"></span>
#### OPAをサポートする関数プロジェクト

OPA 関数テンプレートを使用して、[Open Policy Agent (OPA)](https://www.openpolicyagent.org/) をサポートする関数プロジェクトを作成できます。 [OPA関数プロジェクトを作成する](https://docs.byteplus.com/en/docs/byteplus-cdn/create_function_project_with_opa_jp) を参照してください。

<span id="バグ修正"></span>
#### バグ修正

[query コマンド](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-jp#query) の `-X` パラメータが有効にならない問題を修正しました。

<span id="v1-1-1"></span>
## v1.1.1

此版本發佈於 2025 年 6 月 23 日。

<span id="新增功能"></span>
### 新增功能

<span id="mcp-伺服器"></span>
#### MCP 伺服器

邊緣函數 CLI 可作為 MCP 伺服器被大語言模型調用。參見 [MCP 伺服器概覽](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-mcp-server-overview-zh-tw)。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aea6754b6ccb417ef1ba7c66be43ab6f.png) </span>

<span id="指定函數專案所在目錄"></span>
#### 指定函數專案所在目錄

[nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw) 命令新增 `<dir>` 參數，用於指定需要建立的函數專案所在的目錄。

<span id="新增-simple-page-函數範本"></span>
#### 新增 Simple Page 函數範本

內建函數範本中新增了 Simple Page 範本。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_087b92ded847576a99e3af520edd0d6a.png) </span>

Simple Page 範本展示如何傳回一個簡單的網頁。您無需設定 Access Key ID 和 Secret Access Key 即可使用該範本。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_28b2ac5593a80a359f39296478e033ef.png) </span>

<span id="增加地域限制功能"></span>
#### 增加地域限制功能

您在建立函數或儲存空間時，可以設定函數的發佈地域或 KV 資料的儲存地域是否僅限於中國內地。

以下命令新增 \-\-cn 參數：


* [nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw)：\-\-cn 參數用於設定函數的發佈地域是否僅限於中國內地。

* [nest functions create](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#create)：\-\-cn 參數用於設定函數的發佈地域是否僅限於中國內地。

* [nest kv namespace create](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-cn-zh-tw#create)：\-\-cn 參數用於設定 KV 資料的儲存地域是否僅限於中國內地。


以下命令的傳回值新增 REGION 列：

\- [nest functions list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list)：傳回值新增 REGION 列，用於展示函數的發佈地域是否僅限於中國內地。

\- [nest kv namespace list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-cn-zh-tw#list)：傳回值新增 REGION 列，用於展示 KV 資料的儲存地域是否僅限於中國內地。

同時，函數設定檔 nest.json 中的 functions 物件和 kv 物件也新增 Region 欄位。

<span id="問題修復"></span>
### 問題修復


* 修復了在 [nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw) 命令產生的 package.json 檔案中，`devDependencies` 下 `@byteplus/nest` 名稱錯誤的問題。

* 修復了 [nest domain list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-cn-zh-tw) 所顯示的網域名稱狀態與主控台不一致的問題。


<span id="優化"></span>
### 優化


* 對接了新版的邊緣函數 OpenAPI。

* [nest domain bind](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-cn-zh-tw) 命令增加了對轉送規則的可用性校驗邏輯。

* [nest debug source](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-cn-zh-tw) 命令可以對任意目錄的 .js 檔案進行偵錯。

* 發佈在 nest.json 中手動編輯的邊緣 KV 資料時，您可以使用 `@` 符號引用本地檔案作為 KV 鍵值對的值。


<span id="v1-0-0"></span>
## v1.0.0

該版本發佈於 2025 年 3 月 13 日。該版本是邊緣函數 CLI 的首個版本。
