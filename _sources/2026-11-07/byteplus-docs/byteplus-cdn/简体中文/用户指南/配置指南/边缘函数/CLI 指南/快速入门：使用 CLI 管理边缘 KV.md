---
title: "快速入门：使用 CLI 管理边缘 KV"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-kv-quickstart-cn"
---

本教程基于简单的示例场景介绍如何使用边缘函数 CLI 管理边缘 KV。

边缘 KV 服务是在 BytePlus 的全球边缘节点上的分布式键值存储服务。一个键值对通过边缘函数控制台、OpenAPI 或运行时 API 被写入边缘 KV 后，会自动被同步到所有边缘节点。函数通过运行时 API 可以快速读取位于同一边缘节点的键值对。

<span id="示例场景"></span>
## 示例场景

您的网站支持 A/B 测试功能，可以根据用户的地理位置返回不同版本的网页。版本切换的配置信息存储在边缘 KV 中。您希望可以从函数的代码中读取版本切换的配置信息。在本教程中，假设配置信息如下：

```json
{
  "us": "versionA",
  "eu": "versionB",
  "asia": "versionA"
}
```


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

您需要完成以下步骤实现示例场景。


1. **安装边缘函数 CLI**：新建一个空白 Node.js 项目并在项目中安装边缘函数 CLI。

2. **设置您的 Access Key ID 和 Secret Access Key**：使用边缘函数 CLI 设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key 。

3. **创建存储空间**：使用边缘函数 CLI 创建一个存储空间。

4. **创建键值对**：使用边缘函数 CLI 在存储空间中创建一个键值对

5. **在函数代码中读取键值对的值**：在函数代码中读取键值对的值。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cc1018717c89006d3c315629ae349e1c.png) </span>

<span id="步骤一：安装边缘函数-cli"></span>
### 步骤一：安装边缘函数 CLI

参见以下步骤安装边缘函数 CLI。


1. 使用 `npm init` 新建一个空白 Node.js 项目。


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



2. 在 Node.js 项目的目录下运行 `npm i --save-dev @byteplus/nest` 安装边缘函数 CLI。


```shell
$ npm i --save-dev @byteplus/nest

added 1 package, and audited 2 packages in 739ms

found 0 vulnerabilities
```


接下来，您需要设置您的 Access Key ID 和 Secret Access Key。

<span id="步骤二：设置您的-access-key-id-和-secret-access-key"></span>
### 步骤二：设置您的 Access Key ID 和 Secret Access Key

在 `HelloWorld` 目录运行以下命令在边缘函数 CLI 中设置您的 Access Key ID 和 Secret Access Key。您可以从 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)获取 Access Key ID 和 Secret Access Key。参见 [nest config](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-config-cn)。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


<span id="步骤三：创建一个存储空间"></span>
### 步骤三：创建一个存储空间

在 Node.js 项目的目录下运行 `nest kv namespace create` 创建一个名称为 `abtest_config` 的存储空间。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您只能使用控制台、 OpenAPI 或 CLI 创建存储空间。您无法使用运行时 API 创建存储空间。</div>


```shell
$ npx nest kv namespace create abtest_config
New namespace "abtest_config" created!
```


您可以运行 `nest kv namespace list` 查看已创建的存储空间。

```shell
$ npx nest kv namespace list
+---------------------------------------------------------------+--------------+----------------------+---------------------+
|                            ID:NAME                            |   PROJECT    |     DESCRIPTION      |     CREATETIME      |
+---------------------------------------------------------------+--------------+----------------------+---------------------+
| 25540045541653372777:abtest_config                            | default      |                      | 2025-01-17 17:13:10 |
+---------------------------------------------------------------+--------------+----------------------+---------------------+
```


<span id="步骤四：在存储空间中创建一个键值对"></span>
### 步骤四：在存储空间中创建一个键值对

在 Node.js 项目的目录下运行 `nest kv set` 在 `abtest_config` 存储空间下创建一个键值对。键值对的键是 `config_key`；键值对的值是示例场景中的 JSON 值 `{"us":"versionA","eu":"versionB","asia":"versionA"}`。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以使用控制台、OpenAPI 或运行时 API 创建键值对。</div>


```shell
$ npx nest kv set --namespace 25540045541653372777:abtest_config config_key {"us":"versionA","eu":"versionB","asia":"versionA"}
```


您可以运行 `nest kv get` 查看您创建的键值对。

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


<span id="步骤五：在函数代码中读取键值对的值"></span>
### 步骤五：在函数代码中读取键值对的值

参见以下步骤在函数代码中读取键值对的值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以使用控制台、OpenAPI 或运行时 API 读取键值对的值。</div>


在函数代码中，您调用 [KV.get()](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-EdgeKV-RuntimeAPI-cn) 获取键值对的值。

```JavaScript
const config = await KV.get("abtest_config","config_key",{type:"string"});
```


您可以通过边缘函数 CLI 的 [nest debug](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-cn) 命令，在 Debugger 命令行中调试上述代码：


1. 运行 setkv 在 Debugger 中添加键值对。


```shell
nest: setkv abtest_config config_key {"us":"versionA","eu":"versionB","asia":"versionA"}
```



2. 运行 query 触发函数执行。


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
