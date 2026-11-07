---
title: "使用 Pages 模板"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/use-pages-templates"
---

本文档介绍如何通过 Template 创建 Pages 项目，以及常见模板的定位和模型接入方式。

<span id="通过-template-创建项目"></span>
## 通过 Template 创建项目

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260520073157-383537593005.png) </span>

选择 **Template** 后，按照以下步骤完成配置：


1. 从模板列表中选择模板，例如 `Vuejs`、`Nextjs`、`HTML2Markdown`、`OpenClaw` 或 `VibeCoding`。

2. 在 **选择 Git 提供程序账户** 区域，选择用于创建模板项目的 GitHub 账号。

3. 在 **配置项目** 区域，填写或选择以下信息：

   * **项目页面名称**

   * **存储库名称**

   * **加速区**

   * **存储库类型**（**Private** 或 **Public**）

4. 根据模板需要，在 **环境变量** 区域配置相关参数。

5. 如果所选模板需要模型能力，可在 **配置大模型** 区域补充模型相关配置。

6. 如有需要，在 **加速设置** 中填写自定义域名，并选择是否自动生成免费证书。

7. 单击 **创建**。


模板项目创建成功后，Pages 会执行以下操作：


* 在所选 GitHub 账号下自动创建新的代码仓库。

* 使用生成的仓库自动触发首次部署。

* 在部署成功后生成可访问的预览链接。


<span id="常见模板说明"></span>
## 常见模板说明

不同模板的主配置区域基本一致，主要差异通常体现在模板定位、预置能力、环境变量要求和模型配置要求上。当前控制台中的常见模板可按以下方式理解：


* `Vuejs` 与 `Nextjs` 为通用框架模板，主要提供对应技术栈的起步项目，适合从基础工程开始开发自定义站点或应用。

* `HTML2Markdown` 为场景化工具模板，预置特定工具能力及相关配置项，适合快速创建具有明确用途的工具型项目。

* `VibeCoding` 与 `OpenClaw` 为场景化 AI 应用模板。其中，`VibeCoding` 用于创建基于模型能力生成应用的示例项目；`OpenClaw` 为基于 Next.js 的 OpenClaw 应用模板。两者都不是单纯的前端框架选项，而是包含预设业务能力的模板项目。


<span id="模型接入说明"></span>
## 模型接入说明

当前控制台中的 **配置大模型** 区域支持为部分模板补充模型配置。

`OpenClaw` 与 `VibeCoding` 模板均支持通过火山方舟接入模型；其中，`VibeCoding` 还支持接入第三方模型。

<span id="说明"></span>
## 说明


* 对于通过 Template 创建的项目，Pages 会先创建对应仓库并自动执行首次部署。

* 模板项目创建完成后，后续更新仍需根据仓库变更重新触发部署。
