---
title: "创建 Pages 项目"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/create-pages-project"
---

本文档介绍如何在控制台创建 Pages 项目。

<span id="开始前准备"></span>
## 开始前准备


1. 登录 [Pages 页面](https://console.byteplus.com/cdn/cdn-bp/synthopages/list)。

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260520072316-1250619110716.png) </span>

2. 单击 **新项目**。

3. 在 **创建方式** 区域，选择以下任一方式：

   * **Upload File**：上传本地 ZIP 包。

   * **Git**：从 Git 仓库导入代码并构建部署。

   * **Template**：从预置模板快速生成项目并自动部署。有关 Template 的详细说明，请参见 使用 Pages 模板。


<span id="通过上传文件创建项目"></span>
## 通过上传文件创建项目

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260520072601-1402753087649.png) </span>

配置以下参数，然后单击 **创建**：


|分类 |参数 |说明 |
|---|---|---|
|**基础配置** |**创建方式** |选择 **上传文件**。 |
||**上传文件** |上传 ZIP 格式的文件包。ZIP 包中必须包含 `index.html` 入口文件。 |
|**通用设置** |**Pages 项目名称** |输入项目名称。 |
||**项目描述**（可选） |输入项目描述。 |
||**项目** |选择所属的 BytePlus 项目。 |
||**加速区域** |选择控制台中可用的加速区域。 |
|**加速设置** |**域名**（可选） |配置自定义域名。若暂不填写，项目创建后仍可通过平台预览地址访问。 |
||**自动生成免费证书** |为自定义域名自动申请免费证书。 |


创建成功后，Pages 会自动触发首次部署。

<span id="通过-git-导入项目"></span>
## 通过 Git 导入项目

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260520072659-1109676898256.png) </span>

选择 **Git** 后，按照以下步骤完成配置：


1. 在 **导入 Git 存储库** 区域，先添加 GitHub 账号。

2. 在 GitHub 授权页面中，选择允许 Pages 访问所有仓库或指定仓库。

3. 授权完成后，返回 Pages 控制台。控制台将展示当前账号下已授权访问的仓库列表。

4. 在目标仓库右侧单击 **导入**。

5. 导入完成后，配置以下内容：

   
   |分类 |参数 |说明 |
   |---|---|---|
   |**导入 Git 存储库** |**GitHub 账号 / 仓库** |显示当前导入的仓库信息。 |
   ||**生产分支** |首次创建时使用默认分支进行构建。项目创建完成后，您可以在项目详情页修改生产分支。 |
   |**构建和输出设置** |**根目录** |指定项目源码所在目录。 |
   ||**构建输出目录** |指定构建产物目录，例如 `dist`。 |
   ||**构建命令** |指定构建命令，例如 `npm run build`。 |
   ||**安装命令** |指定安装依赖命令，例如 `npm install` 或 `npm ci`。 |
   |**环境变量** |**Key / Value** |可选。为构建或运行设置环境变量。 |
   |**通用设置** |**Pages 项目名称** |输入项目名称。 |
   ||**项目描述**（可选） |输入项目描述。 |
   ||**项目** |选择所属的 BytePlus 项目。 |
   ||**加速区域** |选择控制台中可用的加速区域。 |
   |**加速设置** |**域名**（可选） |配置自定义域名。若不填写，项目创建后仍可通过平台预览地址访问。 |
   ||**自动生成免费证书** |为自定义域名自动申请免费证书。 |
   

6. 单击 **创建**。


创建成功后，Pages 会自动拉取仓库代码并触发首次部署。部署成功后，您可以通过项目列表中的 **预览** 入口，或在项目详情页的 **预览** 区域访问部署结果。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">环境变量名称必须使用合法字符。请勿将邮箱地址等包含 <code>@</code> 的内容直接填写在 <strong>Key</strong> 字段中。</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260520073002-546090849609.png) </span>

<span id="说明"></span>
## 说明


* 对于通过 Git 创建的项目，修改代码仓库内容后，您需要重新触发部署才能使变更生效。

* 对于通过 ZIP 上传创建的项目，后续可以通过 **部署 \> 新部署** 重新上传新的 ZIP 包完成更新。
