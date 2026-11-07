---
title: "安装CLI"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/get-started-with-edge-function-cli-cn"
---

本文档介绍如何安装边缘函数 CLI。

<span id="运行环境要求"></span>
## 运行环境要求

运行边缘函数 CLI 的设备需要满足以下要求：


* 操作系统必须属于以下类型：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* 安装了 [Node.js](https://nodejs.org/) 和 [npm](https://www.npmjs.com/)。版本要求如下：

   * Node.js：8.17.0+

   * npm：6.13.4+

* 安装了 [wget](https://www.gnu.org/software/wget/) 或 [cURL](https://curl.se/)。


<span id="操作步骤"></span>
## 操作步骤

建议您把边缘函数 CLI 以 [devDependencies](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#devdependencies) 的形式安装到您的 Node.js 项目，而不要将其安装到全局。这样可以保证一个 Node.js 项目中的所有协作者使用的边缘函数 CLI 版本是相同的。如果 Node.js 项目的不同协作者使用了不同版本的边缘函数 CLI，可能会出现协作冲突。


* 如果您还没有 Node.js 项目，您可以使用 `npx @byteplus/nest init` 创建一个新的 Node.js 项目，在您的 Node.js 项目中安装边缘函数 CLI 并创建一个本地函数。

* 如果您已有一个 Node.js 项目，可以把边缘函数 CLI 以 [devDependencies](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#devdependencies) 的形式安装到您的 Node.js 项目。


<span id="使用-npm-安装边缘函数-cli"></span>
### 使用 npm 安装边缘函数 CLI

```shell
npm i --save-dev @byteplus/nest
```


<span id="使用-yarn-安装边缘函数-cli"></span>
### 使用 yarn 安装边缘函数 CLI

```shell
yarn add -D @byteplus/nest
```


<span id="查看已安装的边缘函数-cli-的版本"></span>
## 查看已安装的边缘函数 CLI 的版本

安装完成后，您可以在您的 Node.js 项目的根目录运行 `npx nest --version` 查看边缘函数 CLI 的版本。

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
