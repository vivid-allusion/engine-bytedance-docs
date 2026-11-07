---
title: "使用边缘函数 MCP 服务"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/integrate-mcp-server-zh-cn"
---

本文档介绍如何把边缘函数 MCP 服务添加到您的 MCP 主机并使用边缘函数 MCP 服务。

<span id="运行环境要求"></span>
## 运行环境要求

参见边缘函数 CLI 的 [运行环境要求](https://docs.byteplus.com/docs/byteplus-cdn/get-started-with-edge-function-cli-cn#%E8%BF%90%E8%A1%8C%E7%8E%AF%E5%A2%83%E8%A6%81%E6%B1%82)。

<span id="把边缘函数-mcp-服务添加到-mcp-主机"></span>
## 把边缘函数 MCP 服务添加到 MCP 主机

边缘函数提供了 [Claude for Desktop 的 MCP 服务配置文件](https://modelcontextprotocol.io/quickstart/user)。该配置文件也兼容 Cursor、Cline 或 Trae 等 MCP 主机。MCP 服务配置文件规定了 MCP 客户端在运行时需要启动哪些 MCP 服务，以及启动 MCP 服务所需的命令和参数。

```JSON
{
  "mcpServers": {
    "byteplus-edge-function": {
      "command": "npx",
      "args": [
        "-y",
        "@byteplus/nest@latest",
        "mcp",
        "server"
      ]
    }
  }
}
```


本文分别以 [Cursor](https://www.cursor.com/) 和 [Trae](https://www.trae.ai/) 为例展示如何把边缘函数 MCP 服务的配置添加到您的 MCP 主机。

<span id="把边缘函数-mcp-服务添加到-cursor"></span>
### 把边缘函数 MCP 服务添加到 Cursor

本文以 Cursor 0.5.0 为例。


1. 在 Cursor 中，找到 **Cursor Settings**，选择 MCP，然后点击 **Add New Global MCP Server**。Cursor 会打开 mcp.json 文件。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4fe1a403bac0d95238e8d85c8bf5c447.png) </span>

2. 在 mcp.json 文件中，加入边缘函数 MCP 服务的配置并保存您的改动。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a3514f1ce4504a9321e34fc675414871.png) </span>

3. 返回 **Cursor Settings** 页面。您可以看到您添加的边缘函数 MCP 服务。同时，边缘函数 MCP 服务会被启动。启动完成后，边缘函数 MCP 服务左侧的圆点会变为绿色。此时，您就可以在 Cursor Agent 中使用边缘函数 MCP 服务。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f9716363a762287c6a015f033d23e712.png) </span>


<span id="把边缘函数-mcp-服务添加到-trae"></span>
### 把边缘函数 MCP 服务添加到 Trae

本文以 Trae 0.5.9 为例。


1. 在 Trae 的 AI 侧栏，选择 **MCP** 标签页。点击 **添加**。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果 AI 侧栏没有 MCP 标签页。您可以点击右侧的齿轮图标，在弹出的下拉菜单中选择 MCP 标签页。   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_03fea7275fcd0500d0ae25a8fc596631.png) </span>

2. 点击 **手动配置**。在 **手动配置** 窗口粘贴边缘函数 MCP 服务配置文件的内容。点击 **确认**。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ca96e4ef6b45685d95a73d8911118fb7.png) </span>

   边缘函数 MCP 服务会被添加到默认智能体 BuilderWithMCP。同时，边缘函数 MCP 服务会被启动。启动完成后，边缘函数 MCP 服务的状态会变为 **可使用**。此时，您就可以在默认智能体 BuilderWithMCP 中使用边缘函数 MCP 服务。另外，您也可以把边缘函数 MCP 服务添加到其他 Trae 智能体。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_22bb575e06d9075821949c446264dbee.png) </span>


<span id="使用边缘函数-mcp-服务"></span>
## 使用边缘函数 MCP 服务

边缘函数 MCP 服务通过边缘函数 CLI 向 MCP 客户端提供以下工具：


* **init_project**：创建一个函数项目并在函数项目中创建一个本地函数，即 [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn)。

* **add_function**：在函数项目中创建一个函数，即 [nest functions create](https://docs.byteplus.com/en/docs/18/docs/byteplus-cdn/cli-ref-nest-function-cn#create)。使用该工具前，您必须 [设置 Access Key ID 和 Secret Access Key](https://docs.byteplus.com/en/docs/18/47035#set-ak-sk)。

* **pull_function**：把远端函数的代码同步到本地函数，即 [nest functions pull](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#pull)。使用该工具前，您必须 [设置 Access Key ID 和 Secret Access Key](https://docs.byteplus.com/en/docs/18/47035#set-ak-sk)。

* **deploy_function**：把本地函数部署到边缘节点，即 [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-cn)。使用该工具前，您必须 [设置 Access Key ID 和 Secret Access Key](https://docs.byteplus.com/en/docs/18/47035#set-ak-sk)。

* **start_function**：运行函数代码，即 [nest start](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-start-cn)。


您可以使用提示词向 MCP 客户端描述您希望调用的工具以及向工具传入的参数。MCP 客户端根据您的提示词规划需要完成的任务，并执行对应的边缘函数 CLI 命令。您需要确保函数项目的目录被包括到了 LLM 的上下文。

<span id="在-cursor-中使用边缘函数-mcp-服务"></span>
### 在 Cursor 中使用边缘函数 MCP 服务


1. 在 AI Pane，选择 Agent 作为对话对象。

2. 向智能体发送提示词，指示智能体在指定目录创建一个边缘函数项目。智能体会通过边缘函数 MCP 服务调用边缘函数 CLI 创建一个函数项目，并在函数项目中创建一个本地函数。

3. 智能体完成函数项目和本地函数的创建后，您可以验证函数项目和本地函数是否被成功创建。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f048ff2a9aa071393bd646c40bb0f100.png) </span>


<span id="在-trae-中使用边缘函数-mcp-服务"></span>
### 在 Trae 中使用边缘函数 MCP 服务

本文以 Trae 的默认智能体 BuilderWithMCP 为例展示如何使用边缘函数 MCP 服务。


1. 在 AI 侧栏，输入 `@` 选择 BuilderWithMCP 智能体。

2. 向智能体发送提示词，指示智能体在指定目录创建一个边缘函数项目。智能体会通过边缘函数 MCP 服务调用边缘函数 CLI 创建一个函数项目，并在函数项目中创建一个本地函数。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_204bf527a4eef7ec487f2bace2a889bf.png) </span>

3. 智能体完成函数项目和本地函数的创建后，您可以验证函数项目和本地函数是否被成功创建。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a858ff1b9bcb317deadc0a19c5399f6f.png) </span>


&nbsp;

<span id="设置-access-key-id-和-secret-access-key"></span>
## 设置 Access Key ID 和 Secret Access Key

边缘函数 MCP 服务本质上是边缘函数 CLI。边缘函数 CLI 中的部分命令需要从项目配置文件中获取 Access Key ID 和 Secret Access Key。如果您需要运行这些命令，您必须在项目配置文件中设置 Access Key ID 和 Secret Access Key。

项目配置可以被分类为函数项目配置和全局项目配置。


* **函数项目配置**：保存在每个函数项目根目录下的 `nest.json` 文件。函数项目配置文件适用于当前项目。

* **全局项目配置**：保存在 `~/.nest.json` 文件。全局项目配置文件适用于所有函数项目。


边缘函数 CLI 优先从函数项目配置文件中获取项目配置。如果项目配置获取失败，边缘函数 CLI 从全局项目配置文件中获取项目配置。

如果您没有安装边缘函数 CLI，您的本地没有全局项目配置文件。因此，您在调用 init_project 工具创建函数项目后，需要在函数项目配置文件中设置 Access Key ID 和 Secret Access Key。例如，在下面的函数项目配置文件中，您需要：


* 把 `access_key` 参数的值设置为您的 Access Key ID。

* 把 `secret_key` 参数的值设置为您的 Secret Access Key。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以从 <a href="https://console.byteplus.com/iam/keymanage">BytePlus 控制台</a>获取 Access Key ID 和 Secret Access Key。</div>


```json
{
  "work_dir": "/Users/test/abc",
  "src_dir": "src",
  "output_dir": "output",
  "cloud": {
    "api_server": "https://cdn.byteplusapi.com",
    "debug_server": "wss://byteplusef-debugger.byteintlapi.com",
    "api_version": "2021-03-01",
    "api_region": "ap-singapore-1",
    "api_timeout": 5000,
    "key_manager_url": "https://console.byteplus.com/iam/keymanage",
    "product": "CDN",
    "access_key": "<Your Access Key ID>",
    "secret_key": "<Your Secret Access Key>"
  },
  "functions": [
    {
      "id": "",
      "name": "test",
      "type": "js",
      "entry": "src/index.js",
      "project": "default"
    }
  ],
  "debugger": {}
}

```
