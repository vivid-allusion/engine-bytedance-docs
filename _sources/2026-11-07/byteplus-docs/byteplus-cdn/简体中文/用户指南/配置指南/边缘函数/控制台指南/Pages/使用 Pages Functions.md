---
title: "使用 Pages Functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/use-pages-functions"
---

本文档介绍如何在 Pages 中使用 Functions，以及 Functions 路由的生成方式。

<span id="什么是-pages-functions"></span>
## 什么是 Pages Functions

Pages 支持基于项目中的 `/functions` 目录提供轻量动态能力。您可以在静态站点之外，通过 Functions 处理简单的接口请求或动态逻辑。

<span id="路由生成规则"></span>
## 路由生成规则

Functions 路由由项目中的 `/functions` 目录自动生成。

例如：


* `functions/api/hello.js` 会生成 `/functions/api/hello` 路由。


<span id="在哪里查看-functions-路由"></span>
## 在哪里查看 Functions 路由

在 **部署** 页签中，单击某个 **部署 ID**，进入 **Deployment Details** 页面。

如果当前部署包含 `/functions` 目录，您可以在 **Functions** 页签中查看当前部署对应的 Functions 路由配置。

如果项目中未包含 `/functions` 目录，则该页签中不会展示函数路由。

<span id="说明"></span>
## 说明


* `/functions` 目录中的文件路径决定 Functions 的访问路径。

* Functions 路由信息以当前部署内容为准；当部署内容发生变化时，展示的路由配置也会相应更新。
