---
title: "使用 CLI 托管静态页面"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/pages_host_webpage_cn"
---

本文档介绍如何使用 Pages 托管静态页面。

<span id="什么是-pages"></span>
## 什么是 Pages

Pages 是 BytePlus 边缘函数提供的一项静态页面托管服务，旨在帮助您快速、高效地将静态网站部署到全球边缘节点网络。通过 Pages，您可以轻松托管各种类型的静态内容，包括但不限于：


* 静态网站（HTML/CSS/JavaScript）

* 单页应用（SPA）

* 文档站点

* 博客

* 静态资源库


Pages 基于分布在全球的 BytePlus 边缘节点构建，将您的静态资源缓存到离用户最近的边缘节点，从而实现低延迟、高可用的内容交付。

您可以通过控制台或边缘函数 CLI 使用 Pages。

<span id="基本概念"></span>
## 基本概念

<span id="pages-项目"></span>
### Pages 项目

Pages 项目是边缘函数中用于托管和管理静态页面的基本单元。每个 Pages 项目都拥有唯一的 ID，作为其身份标识。通过 Pages 项目，您可以集中管理静态页面的生命周期。

<span id="使用限制"></span>
## 使用限制

BytePlus Pages 的使用限制如下。


* 每个 BytePlus 账号最多可以创建 10 个 Pages 项目

* 每个 Pages 项目最多保留 100 个历史资源，多余资源会自动清理

* 每个 Pages 项目每个月最多发布 100 次

* 对于每个 Pages 项目，静态资源在压缩后的大小不超过 50 MB

* 对于每个 Pages 项目，静态资源的文件个数不超过 500 个

* 对于每个 Pages 项目，静态资源的单文件大小不超过 25 MB


<span id="示例场景"></span>
## 示例场景

您有一个静态网站项目，包含 .html、.css、.js 等文件，您希望通过 BytePlus Pages 快速托管和发布该网站。

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

<span id="步骤一：安装边缘函数-cli"></span>
### 步骤一：安装边缘函数 CLI

BytePlus Pages 无需本地函数项目，因此您可以选择将 CLI 安装到全局环境中：

```shell
npm install -g @byteplus/nest
```


<span id="步骤二：设置您的-access-key-id-和-secret-access-key"></span>
### 步骤二：设置您的 Access Key ID 和 Secret Access Key

在任意目录下运行以下命令在边缘函数 CLI 中设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。您可以从 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage) 获取 Access Key ID 和 Secret Access Key：

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


<span id="步骤三：创建并发布-pages-项目"></span>
### 步骤三：创建并发布 Pages 项目


1. **创建静态资源目录**：在任意位置创建一个静态资源目录（例如 `site`），并将您的静态网站文件放入该目录中：

   ```shell
   mkdir -p site
   # 将您的静态文件（如 .html、.css、.js 等）放入 site 目录中
   ```
   

2. **创建并发布 Pages 项目**：执行以下命令创建并立即发布一个 Pages 项目：

   ```shell
   npx nest pages create --name demo-site --upload ./site
   ```
   

   #### 参数说明    <span id="参数说明"></span>

   
   |参数 |类型 |是否必填 |描述 |
   |---|---|---|---|
   |\-\-name |string |是 |指定新 Pages 项目的名称 |
   |\-\-upload |string |是 |本地静态资源目录路径（必须包含 index.html 入口文件） |
   

   命令执行成功后，您将看到类似以下的输出信息：

   ```shell
   ==> New Pages demo-site created!
   ==> [info]: Compressing given assets directory ./site...✓
   ==> [info]: Uploading assets...✓
   ==> [info]: Deploying pages...✓
   ==> Pages demo-site is publishing, you can visit it by open http://pywahntknjrhcufp.synthopages.bytepluses.com in browser a few minutes later
   ```
   

   发布操作通常需要 1\-5 分钟生效。生效后，您就可以通过命令输出中提供的域名访问您的静态站点了。

   如果您的 Pages 项目尚未关联自定义域名，系统会自动分配一个用于预览的临时公网域名。该域名的后缀为 synthopages.bytepluses.com。请注意，这个域名仅供预览使用。您可以在浏览器中打开该域名来预览您的静态网站。


<span id="步骤四：为静态站点关联自定义域名"></span>
### 步骤四：为静态站点关联自定义域名

为了让您的静态站点可以通过自定义域名访问，可以使用以下命令为 Pages 项目添加域名：

```shell
nest pages domain add -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


执行成功后，您将看到类似以下的输出：

```Plain Text
==> [info]: Adding domain "wow.test.example.com" to pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was added successfully.
```


新添加的域名需要验证后才能正式上线使用。您需要为域名添加 CNAME 解析记录，然后执行以下命令进行验证：

```shell
nest pages domain verify -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```
