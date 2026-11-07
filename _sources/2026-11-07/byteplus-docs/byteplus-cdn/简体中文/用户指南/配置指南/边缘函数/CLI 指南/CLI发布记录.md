---
title: "CLI发布记录"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-release-notes-cn"
---

本文档包含边缘函数 CLI 的发布记录。

<span id="v1-3-0"></span>
## v1.3.0

该版本发布于 2025 年 11 月 28 日。

<span id="新增功能"></span>
### 新增功能

<span id="支持-pages-cli"></span>
#### 支持 Pages CLI

边缘函数 Pages 是 BytePlus 边缘函数提供的一项静态页面托管服务，旨在帮助开发者快速、高效地将静态网站部署到全球边缘节点网络。目前，您可以通过边缘函数 CLI 使用边缘函数 Pages。参见 [nest pages](https://docs.byteplus.com/en/docs/byteplus-cdn/nest_pages_cn)。

<span id="v1-2-0"></span>
## v1.2.0

该版本发布于 2025 年 7 月 16 日。

<span id="新增功能"></span>
### 新增功能

<span id="支持-opa-的函数项目"></span>
#### 支持 OPA 的函数项目

您可以通过 OPA 函数模板创建一个支持 [开放策略代理（Open Policy Agent, OPA）](https://www.openpolicyagent.org/) 的函数项目。 参见 [创建 OPA 函数项目](https://docs.byteplus.com/en/docs/byteplus-cdn/create_function_project_with_opa_zh-cn)。

<span id="问题修复"></span>
#### 问题修复

修复了 [query 命令](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-cn#query) 的 `-X` 参数不生效的问题。

<span id="v1-1-1"></span>
## v1.1.1

该版本发布于 2025 年 6 月 23 日。

<span id="新增功能"></span>
### 新增功能

<span id="mcp-服务器"></span>
#### MCP 服务器

边缘函数 CLI 可作为 MCP 服务器被大语言模型调用。参见 [MCP 服务概览](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-mcp-server-overview-zh-cn)。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f048ff2a9aa071393bd646c40bb0f100.png) </span>

<span id="指定函数项目所在目录"></span>
#### 指定函数项目所在目录

[nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-cn) 命令新增 `<dir>` 参数，用于指定需要创建的函数项目所在的目录。

<span id="新增-simple-page-函数模板"></span>
#### 新增 Simple Page 函数模板

内置函数模板中新增了 Simple Page 模板。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_087b92ded847576a99e3af520edd0d6a.png) </span>

Simple Page 模板展示如何返回一个简单的网页。您无需设置 Access Key ID 和 Secret Access Key 即可使用该模板。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_28b2ac5593a80a359f39296478e033ef.png) </span>

<span id="增加地域限制功能"></span>
#### 增加地域限制功能

您在创建函数或存储空间时，可以设置函数的发布地域或 KV 数据的存储地域是否仅限于中国内地。

以下命令新增 \-\-cn 参数：


* [nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-cn)：\-\-cn 参数用于设置函数的发布地域是否仅限于中国内地。

* [nest functions create](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-cn#create)：\-\-cn 参数用于设置函数的发布地域是否仅限于中国内地。

* [nest kv namespace create](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-cn#create)：\-\-cn 参数用于设置 KV 数据的存储地域是否仅限于中国内地。


以下命令的返回值新增 REGION 列：


* [nest functions list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-cn#list)：返回值新增 REGION 列，用于展示函数的发布地域是否仅限于中国内地。

* [nest kv namespace list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-cn#list)：返回值新增 REGION 列，用于展示 KV 数据的存储地域是否仅限于中国内地。


同时，函数配置文件 nest.json 中的 functions 对象和 kv 对象也新增 Region 字段。

<span id="问题修复"></span>
### 问题修复


* 修复了在 [nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-cn) 命令生成的 package.json 文件中，`devDependencies` 下 `@byteplus/nest` 名称错误的问题。

* 修复了 [nest domain list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-cn) 所显示的域名状态与控制台不一致的问题。


<span id="优化"></span>
### 优化


* 对接了新版的边缘函数 OpenAPI。

* [nest domain bind](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-cn) 命令增加了对转发规则的可用性校验逻辑。

* [nest debug source](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-cn) 命令可以对任意目录的 .js 文件进行调试。

* 发布在 nest.json 中手动编辑的边缘 KV 数据时，您可以使用 `@` 符号引用本地文件作为 KV 键值对的值。


<span id="v1-0-0"></span>
## v1.0.0

该版本发布于 2025 年 3 月 13 日。该版本是边缘函数 CLI 的首个版本。
