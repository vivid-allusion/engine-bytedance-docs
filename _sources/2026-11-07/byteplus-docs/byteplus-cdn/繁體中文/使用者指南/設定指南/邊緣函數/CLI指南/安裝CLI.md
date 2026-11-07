---
title: "安裝CLI"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/get-started-with-edge-function-cli-cn-zh-tw"
---

本文件介紹如何安裝邊緣函數 CLI。

<span id="執行環境要求"></span>
## 執行環境要求

執行邊緣函數 CLI 的裝置需要滿足以下要求：


* 作業系統必須屬於以下類型：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* 安裝了 [Node.js](https://nodejs.org/) 和 [npm](https://www.npmjs.com/)。版本要求如下：

   * Node.js：8.17.0+

   * npm：6.13.4+

* 安裝了 [wget](https://www.gnu.org/software/wget/) 或 [cURL](https://curl.se/)。


<span id="操作步驟"></span>
## 操作步驟

建議您把邊緣函數 CLI 以 [devDependencies](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#devdependencies) 的形式安裝到您的 Node.js 專案，而不要將其安裝到全域。這樣可以確保一個 Node.js 專案中的所有協作者使用的邊緣函數 CLI 版本是相同的。如果 Node.js 專案的不同協作者使用了不同版本的邊緣函數 CLI，可能會出現協作衝突。


* 如果您還沒有 Node.js 專案，您可以使用 `npx @byteplus/nest init` 建立一個新的 Node.js 專案，在您的 Node.js 專案中安裝邊緣函數 CLI 並建立一個本地函數。

* 如果您已有一個 Node.js 專案，可以把邊緣函數 CLI 以 [devDependencies](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#devdependencies) 的形式安裝到您的 Node.js 專案。


<span id="使用-npm-安裝邊緣函數-cli"></span>
### 使用 npm 安裝邊緣函數 CLI

```shell
npm i --save-dev @byteplus/nest
```


<span id="使用-yarn-安裝邊緣函數-cli"></span>
### 使用 yarn 安裝邊緣函數 CLI

```shell
yarn add -D @byteplus/nest
```


<span id="查看已安裝的邊緣函數-cli-的版本"></span>
## 查看已安裝的邊緣函數 CLI 的版本

安裝完成後，您可以在您的 Node.js 專案的根目錄執行 `npx nest --version` 查看邊緣函數 CLI 的版本。

```shell
$ npx nest --version
  ______    _              ______                _   _
 |  ____|  | |            |  ____|              | | (_)
 | |__   __| | __ _  ___  | |__ _   _ _ __   ___| |_ _  ___  _ __
 |  __| / _` |/ _` |/ _ \ |  __| | | | '_ \ / __| __| |/ _ \| '_ \
 | |___| (_| | (_| |  __/ | |  | |_| | | | | (__| |_| | (_) | | | |
 |______\__,_|\__, |\___| |_|   \__,_|_| |_|\___|\__|_|\___/|_| |_|
               __/ |
              |___/

Version: 1.0.0
```
