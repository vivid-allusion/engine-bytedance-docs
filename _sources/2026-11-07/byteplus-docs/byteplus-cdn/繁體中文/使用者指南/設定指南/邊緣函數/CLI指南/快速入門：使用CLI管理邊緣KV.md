---
title: "快速入門：使用CLI管理邊緣KV"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-kv-quickstart-cn-zh-tw"
---

本教學基於簡單的示例場景介紹如何使用邊緣函數 CLI 管理邊緣 KV。

邊緣 KV 服務是在 BytePlus 的全球邊緣節點上的分散式鍵值儲存服務。一個鍵值對透過邊緣函數控制台、OpenAPI 或執行時期 API 被寫入邊緣 KV 後，會自動被同步到所有邊緣節點。函數透過執行時期 API 可以快速讀取位於同邊緣節點的鍵值對。

<span id="示例場景"></span>
## 示例場景

您的網站支援 A/B 測試功能，可以根據用戶端的地理位置返回不同版本的網頁。版本切換的配置資訊儲存在邊緣 KV 中。您希望可以從函數的程式碼中讀取版本切換的配置資訊。在本教學中，假設配置資訊如下：

```json
{
  "us": "versionA",
  "eu": "versionB",
  "asia": "versionA"
}
```


<span id="執行環境要求"></span>
## 執行環境要求

執行邊緣函數 CLI 的裝置需要滿足以下要求：


* 作業系統必須屬於以下類型：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* 安裝了 [Node.js](https://nodejs.org/) 和 [npm](https://www.npmjs.com/)。版本要求如下：

   * Node.js：8.17.0 或更高版本

   * npm：6.13.4 或更高版本

* 安裝了 [wget](https://www.gnu.org/software/wget/) 或 [cURL](https://curl.se/)。


<span id="操作步驟"></span>
## 操作步驟

您需要完成以下步驟實現示例場景：


1. **安裝邊緣函數 CLI**：新建一個空白 Node.js 專案並在專案中安裝邊緣函數 CLI。

2. **設定您的 Access Key ID 和 Secret Access Key**：使用邊緣函數 CLI 設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key 。

3. **建立儲存空間**：使用邊緣函數 CLI 建立一個儲存空間。

4. **建立鍵值對**：使用邊緣函數 CLI 在儲存空間中建立一個鍵值對。

5. **在函數程式碼中讀取鍵值對的值**：在函數程式碼中讀取鍵值對的值。


<span id="步驟一：安裝邊緣函數-cli"></span>
### 步驟一：安裝邊緣函數 CLI

參見以下步驟安裝邊緣函數 CLI。


1. 使用 `npm init` 新建一個空白 Node.js 專案。


```shell
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (test) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /Users/MyFolder/package.json:

{
  "name": "test",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "description": ""
}


Is this OK? (yes) 
```



2. 在 Node.js 專案的目錄下執行 `npm i --save-dev @byteplus/nest` 安裝邊緣函數 CLI。


```shell
$ npm i --save-dev @byteplus/nest

added 1 package, and audited 2 packages in 739ms

found 0 vulnerabilities
```


接下來，您需要設定您的 Access Key ID 和 Secret Access Key。

<span id="步驟二：設定您的-access-key-id-和-secret-access-key"></span>
### 步驟二：設定您的 Access Key ID 和 Secret Access Key

在 `HelloWorld` 目錄執行以下指令在邊緣函數 CLI 中設定您的 Access Key ID 和 Secret Access Key。您可以從 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)獲取 Access Key ID 和 Secret Access Key。參見 [nest config](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-config-cn-zh-tw)。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


<span id="步驟三：建立一個儲存空間"></span>
### 步驟三：建立一個儲存空間

在 Node.js 專案的目錄下執行 `nest kv namespace create` 建立一個名稱為 `abtest_config` 的儲存空間。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您只能使用控制台、OpenAPI 或 CLI 建立儲存空間。您無法使用執行時期 API 建立儲存空間。</div>


```shell
$ npx nest kv namespace create abtest_config
New namespace "abtest_config" created!
```


您可以執行 `nest kv namespace list` 查看已建立的儲存空間。

```shell
$ npx nest kv namespace list
+---------------------------------------------------------------+--------------+----------------------+---------------------+
|                            ID:NAME                            |   PROJECT    |     DESCRIPTION      |     CREATETIME      |
+---------------------------------------------------------------+--------------+----------------------+---------------------+
| 25540045541653372777:abtest_config                            | default      |                      | 2025-01-17 17:13:10 |
+---------------------------------------------------------------+--------------+----------------------+---------------------+
```


<span id="步驟四：在儲存空間中建立一個鍵值對"></span>
### 步驟四：在儲存空間中建立一個鍵值對

在 Node.js 專案的目錄下執行 `nest kv set` 在 `abtest_config` 儲存空間下建立一個鍵值對。鍵值對的鍵是 `config_key`；鍵值對的值是示例場景中的 JSON 值 `{"us":"versionA","eu":"versionB","asia":"versionA"}`。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以使用控制台、OpenAPI 或執行時期 API 建立鍵值對。</div>


```shell
$ npx nest kv set --namespace 25540045541653372777:abtest_config config_key {"us":"versionA","eu":"versionB","asia":"versionA"}
```


您可以執行 `nest kv get` 查看您建立的鍵值對。

```Plain Text
$ npx nest kv get --namespace 25540045541653372777:abtest_config config_key
+-------+---------------+
| ITEM  |     VALUE     |
+-------+---------------+
| Key   | config_key    |
| Value | us:versionA   |
| DDL   | Never expires |
+-------+---------------+
```


<span id="步驟五：在函數程式碼中讀取鍵值對的值"></span>
### 步驟五：在函數程式碼中讀取鍵值對的值

參見以下步驟在函數程式碼中讀取鍵值對的值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以使用控制台、OpenAPI 或執行時期 API 讀取鍵值對的值。</div>


在函數程式碼中，您呼叫 [KV.get()](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-EdgeKV-RuntimeAPI-cn-zh-tw) 獲取鍵值對的值。

```JavaScript
const config = await KV.get("abtest_config","config_key",{type:"string"});
```


您可以透過邊緣函數 CLI 的 [nest debug](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-cn-zh-tw) 指令，在 Debugger 命令列中偵錯上述程式碼：


1. 執行 setkv 在 Debugger 中新增鍵值對。


```shell
nest: setkv abtest_config config_key {"us":"versionA","eu":"versionB","asia":"versionA"}
```



2. 執行 query 觸發函數執行。


```shell
nest: query
==> HttpResponse ✓
status: 200

statusText: OK

header:
  content-type => text/plain;charset=UTF-8
  date => Fri, 17 Jan 2025 09:53:26 GMT
  server => Sparrow
  transfer-encoding => chunked

body:
{us:versionA,eu:versionB,asia:versionA}
```
