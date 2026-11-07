---
title: "CLI概览"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-function-cli-overview-cn"
---

除了控制台和 OpenAPI 之外，您还可以使用边缘函数 CLI 管理函数和边缘 KV。与控制台和 OpenAPI 相比，边缘函数 CLI 还支持以下额外功能：


* 创建一个或多个本地函数

* 编辑和调试本地函数代码

* 对一个或多个本地函数进行增删改查和发布操作

* 同步本地函数与远端函数


边缘函数 CLI 使您可以在本地编写和调试函数代码，并把本地的函数代码发布到边缘函数服务端。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3e98b961c75e0c51e67e0de33f0db751.png) </span>

<span id="基本概念"></span>
## 基本概念

在使用边缘函数 CLI 之前，建议您先了解下面的基本概念。

<span id="远端函数"></span>
### 远端函数

您在边缘函数服务端创建的函数。每个远端函数都有一个函数 ID 作为该函数的唯一标识。

<span id="本地函数"></span>
### 本地函数

您在函数项目中创建的函数。本地函数可以没有函数 ID。您可以为本地函数关联一个远端函数的函数 ID。

<span id="函数项目"></span>
### 函数项目

包含函数项目配置文件（nest.json）的 Node.js 项目，用于管理本地函数。您使用 [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn) 创建一个函数项目。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 还会在该函数项目中创建一个本地函数。</div>


一个函数项目可以包含一个或多个本地函数，但只能有一个本地函数是默认函数。您可以使用 [nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#create) 在函数项目中创建一个本地函数。

<span id="项目配置"></span>
### 项目配置

项目配置包含了函数项目的工作目录、入口代码文件目录、函数项目下所有本地函数的信息及边缘 KV 数据等信息。项目配置可以被分类为函数项目配置和全局项目配置。


* **函数项目配置**：保存在每个函数项目根目录下的 `nest.json` 文件。函数项目配置文件适用于当前项目。

* **全局项目配置**：保存在 `~/.nest.json` 文件。全局项目配置文件适用于所有函数项目。


边缘函数 CLI 优先从函数项目配置文件中获取项目配置。如果项目配置获取失败，边缘函数 CLI 从全局项目配置文件中获取项目配置。
