---
title: "使用邊緣函數 MCP 伺服器"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/integrate-mcp-server-zh-tw"
---

本文件介紹如何把邊緣函數 MCP 伺服器添加到您的 MCP 主機並使用邊緣函數 MCP 伺服器。

<span id="執行環境要求"></span>
## 執行環境要求

參見邊緣函數 CLI 的[執行環境要求](https://docs.byteplus.com/docs/byteplus-cdn/get-started-with-edge-function-cli-cn-zh-tw#%E5%9F%B7%E8%A1%8C%E7%92%B0%E5%A2%83%E8%A6%81%E6%B1%82)。

<span id="把邊緣函數-mcp-伺服器添加到-mcp-主機"></span>
## 把邊緣函數 MCP 伺服器添加到 MCP 主機

邊緣函數提供了 [Claude for Desktop 的 MCP 伺服器配置檔案](https://modelcontextprotocol.io/quickstart/user)。該配置檔案也相容 Cursor、Cline 或 Trae 等 MCP 主機。MCP 伺服器配置檔案規定了 MCP 用戶端在執行時需要啟動哪些 MCP 伺服器，以及啟動 MCP 伺服器所需的命令和參數。

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


本文分別以 [Cursor](https://www.cursor.com/) 和 [Trae](https://www.trae.ai/) 為例展示如何把邊緣函數 MCP 伺服器的配置添加到您的 MCP 主機。

<span id="把邊緣函數-mcp-伺服器添加到-cursor"></span>
### 把邊緣函數 MCP 伺服器添加到 Cursor

本文以 Cursor 0.5.0 為例。


1. 在 Cursor 中，找到 **Cursor Settings**，選擇 MCP，然後點擊 **Add New Global MCP Server**。Cursor 會開啟 mcp.json 檔案。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4fe1a403bac0d95238e8d85c8bf5c447.png) </span>

2. 在 mcp.json 檔案中，加入邊緣函數 MCP 伺服器的配置並儲存您的變更。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a3514f1ce4504a9321e34fc675414871.png) </span>

3. 返回 **Cursor Settings** 頁面。您可以看到您添加的邊緣函數 MCP 伺服器。同時，邊緣函數 MCP 伺服器會被啟動。啟動完成後，邊緣函數 MCP 伺服器左側的圓點會變為綠色。此時，您就可以在 Cursor Agent 中使用邊緣函數 MCP 伺服器。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f9716363a762287c6a015f033d23e712.png) </span>


<span id="把邊緣函數-mcp-伺服器添加到-trae"></span>
### 把邊緣函數 MCP 伺服器添加到 Trae

本文以 Trae 0.5.9 為例。


1. 在 Trae 的 AI 側欄，選擇 **MCP** 標籤頁。點擊 **添加**。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果 AI 側欄沒有 MCP 標籤頁。您可以點擊右側的齒輪圖示，在彈出的下拉選單中選擇 MCP 標籤頁。   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_03fea7275fcd0500d0ae25a8fc596631.png) </span>

2. 點擊 **手動配置**。在 **手動配置** 視窗貼上邊緣函數 MCP 伺服器配置檔案的內容。點擊 **確認**。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ca96e4ef6b45685d95a73d8911118fb7.png) </span>

   邊緣函數 MCP 伺服器會被添加到預設智能體 BuilderWithMCP。同時，邊緣函數MCP 伺服器會被啟動。啟動完成後，邊緣函數MCP 伺服器的狀態會變為 **可使用**。此時，您就可以在預設智能體 BuilderWithMCP 中使用邊緣函數 MCP 伺服器。另外，您也可以把邊緣函數 MCP 伺服器添加到其他 Trae 智能體。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_22bb575e06d9075821949c446264dbee.png) </span>


<span id="使用邊緣函數-mcp-伺服器"></span>
## 使用邊緣函數 MCP 伺服器

邊緣函數 MCP 伺服器通過邊緣函數 CLI 向 MCP 用戶端提供以下工具：


* **init_project**：建立一個函數專案並在函數專案中建立一個本地函數，即 [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw)。

* **add_function**：在函數專案中建立一個函數，即 [nest functions create](https://docs.byteplus.com/en/docs/18/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#create)。使用該工具前，您必須[設定 Access Key ID 和 Secret Access Key](https://docs.byteplus.com/en/docs/18/47088#set-ak-sk)。

* **pull_function**：把遠端函數的程式碼同步到本地函數，即 [nest functions pull](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#pull)。使用該工具前，您必須[設定 Access Key ID 和 Secret Access Key](https://docs.byteplus.com/en/docs/18/47088#set-ak-sk)。

* **deploy_function**：把本地函數部署到邊緣節點，即 [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-cn-zh-tw)。使用該工具前，您必須[設定 Access Key ID 和 Secret Access Key](https://docs.byteplus.com/en/docs/18/47088#set-ak-sk)。

* **start_function**：執行函數程式碼，即 [nest start](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-start-cn-zh-tw)。


您可以使用提示詞向 MCP 用戶端描述您希望調用的工具以及向工具傳入的參數。MCP 用戶端根據您的提示詞規劃需要完成的任務，並執行對應的邊緣函數 CLI 命令。您需要確保函數專案的目錄被包括到了 LLM 的上下文。

<span id="在-cursor-中使用邊緣函數-mcp-伺服器"></span>
### 在 Cursor 中使用邊緣函數 MCP 伺服器


1. 在 AI Pane，選擇 Agent 作為對話對象。

2. 向智能體發送提示詞，指示智能體在指定目錄建立一個邊緣函數 專案。智能體會通過邊緣函數 MCP 伺服器調用邊緣函數 CLI 建立一個函數專案，並在函數專案中建立一個本地函數。

3. 智能體完成函數專案和本地函數的建立後，您可以驗證函數專案和本地函數是否被成功建立。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f048ff2a9aa071393bd646c40bb0f100.png) </span>


<span id="在-trae-中使用邊緣函數-mcp-伺服器"></span>
### 在 Trae 中使用邊緣函數 MCP 伺服器

本文以 Trae 的預設智能體 BuilderWithMCP 為例展示如何使用邊緣函數 MCP 伺服器。


1. 在 AI 側欄，輸入 `@` 選擇 BuilderWithMCP 智能體。

2. 向智能體發送提示詞，指示智能體在指定目錄建立一個邊緣函數 專案。智能體會通過邊緣函數 MCP 伺服器調用邊緣函數 CLI 建立一個函數專案，並在函數專案中建立一個本地函數。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_204bf527a4eef7ec487f2bace2a889bf.png) </span>

3. 智能體完成函數專案和本地函數的建立後，您可以驗證函數專案和本地函數是否被成功建立。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a858ff1b9bcb317deadc0a19c5399f6f.png) </span>


&nbsp;

<span id="設置-access-key-id-和-secret-access-key"></span>
## 設置 Access Key ID 和 Secret Access Key

邊緣函數 MCP 伺服器本質上是邊緣函數 CLI。邊緣函數 CLI 中的部分命令需要從專案配置檔案中獲取 Access Key ID 和 Secret Access Key。如果您需要執行這些命令，您必須在專案配置檔案中設置 Access Key ID 和 Secret Access Key。

專案配置可以被分類為函數專案配置和全域專案配置。


* **函數專案配置**：保存在每個函數專案根目錄下的 `nest.json` 檔案。函數專案配置檔案適用於當前專案。

* **全域專案配置**：保存在 `~/.nest.json` 檔案。全域專案配置檔案適用於所有函數專案。


邊緣函數 CLI 優先從函數專案配置檔案中獲取專案配置。如果專案配置獲取失敗，邊緣函數 CLI 從全域專案配置檔案中獲取專案配置。

如果您沒有安裝邊緣函數 CLI，您的本地沒有全域專案配置檔案。因此，您在呼叫 init_project 工具創建函數專案後，需要在函數專案配置檔案中設置 Access Key ID 和 Secret Access Key。例如，在下面的函數專案配置檔案中，您需要：


* 把 `access_key` 參數的值設置為您的 Access Key ID。

* 把 `secret_key` 參數的值設置為您的 Secret Access Key。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以從 <a href="https://console.byteplus.com/iam/keymanage">BytePlus 控制台</a>獲取 Access Key ID 和 Secret Access Key。</div>


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
