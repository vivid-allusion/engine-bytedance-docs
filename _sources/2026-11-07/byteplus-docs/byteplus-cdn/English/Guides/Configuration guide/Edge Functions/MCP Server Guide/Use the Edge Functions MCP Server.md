---
title: "Use the Edge Functions MCP Server"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/integrate-mcp-server-en"
---

This document describes how to add the Edge Functions MCP server to your MCP host and use the Edge Functions MCP server.

<span id="runtime-environment-requirements"></span>
## Runtime environment requirements

Refer to the [Runtime Environment Requirements](https://docs.byteplus.com/docs/byteplus-cdn/get-started-with-edge-function-cli-en#system-requirements) for Edge Functions CLI.

<span id="add-edge-functions-mcp-server-to-an-mcp-host"></span>
## Add Edge Functions MCP server to an MCP host

Edge Functions provides an [MCP server configuration file for Claude for Desktop](https://modelcontextprotocol.io/quickstart/user). This configuration file is also compatible with MCP hosts such as Cursor, Cline or Trae. The MCP server configuration file specifies which MCP servers the MCP client needs to start at runtime, as well as the commands and parameters required to start the MCP servers.

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


This document uses [Cursor](https://www.cursor.com/) and [Trae](https://www.trae.ai/) as examples to show how to add the Edge Functions MCP server configuration to your MCP host.

<span id="add-edge-functions-mcp-server-to-cursor"></span>
### Add Edge Functions MCP server to Cursor

This document uses Cursor 0.5.0 as an example.


1. In Cursor, find **Cursor Settings**, select MCP, and then click **Add New Global MCP Server**. Cursor will open the mcp.json file.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4fe1a403bac0d95238e8d85c8bf5c447.png) </span>

2. In the mcp.json file, add the configuration for the Edge Functions MCP server and save your changes.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a3514f1ce4504a9321e34fc675414871.png) </span>

3. Return to the **Cursor Settings** page. You can see the Edge Functions MCP server you added. At the same time, the Edge Functions MCP server will be started. After startup is complete, the dot to the left of the Edge Functions MCP server will turn green. At this point, you can use the Edge Functions MCP server in the Cursor Agent.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e7211764ef55ec0867fc8d12a7a35617.png) </span>


<span id="add-edge-functions-mcp-server-to-trae"></span>
### Add Edge Functions MCP server to Trae

This document uses Trae 0.5.9 as an example.


1. In Trae's AI Side Bar, select the **MCP** tab. Click **Add**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the AI Side Bar does not have an MCP tab, you can click the gear icon on the right and select the MCP tab from the drop\-down menu.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_87b5606b3c985fae2564e1b04fbde18b.png) </span>

2. Click **Configure Manually**. In the **Configure Manually** window, paste the content of the Edge Functions MCP server configuration file. Click **Confirm**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b36275d0133d6e53a221c653e228b318.png) </span>

   The Edge Functions MCP server will be added to the default agent BuilderWithMCP. At the same time, the Edge Functions MCP server will be started. After startup is complete, the status of the Edge Functions MCP server will change to **Ready**. At this point, you can use the Edge Functions MCP server in the default agent BuilderWithMCP. In addition, you can also add the Edge Functions MCP server to other Trae agents.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_533a54431de7625f0e85b2911a1b6e49.png) </span>


<span id="use-edge-functions-mcp-server"></span>
## Use Edge Functions MCP server

The Edge Functions MCP server provides the following tools to the MCP client through the Edge Functions CLI:


* **init_project**: Create a function project and create a local function in the function project, i.e., [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-en).

* **add_function**: Create a function in the function project, i.e., [nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#create). Before using this tool, you must [set your Access Key ID and Secret Access Key](https://docs.byteplus.com/en/docs/18/47079#set-ak-sk).

* **pull_function**: Synchronize the code of the remote function to the local function, i.e., [nest functions pull](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#pull). Before using this tool, you must [set your Access Key ID and Secret Access Key](https://docs.byteplus.com/en/docs/18/47079#set-ak-sk).

* **deploy_function**: Deploy the local function to the edge node, i.e., [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-en). Before using this tool, you must [set your Access Key ID and Secret Access Key](https://docs.byteplus.com/en/docs/18/47079#set-ak-sk).

* **start_function**: Run the function code, i.e., [nest start](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-start-en).


You can use prompts to describe to the MCP client the tools you want to call and the parameters to pass to the tools. The MCP client plans the tasks to be completed based on your prompts and executes the corresponding Edge Functions CLI commands. You need to ensure that the function project directory is included in the LLM's context.

<span id="use-edge-functions-mcp-server-in-cursor"></span>
### Use Edge Functions MCP server in Cursor


1. In the AI Pane, select Agent as the conversation object.

2. Send a prompt to the agent to indicate the agent to create an Edge Functions project in the specified directory. The agent will call the Edge Functions CLI through the Edge Functions MCP server to create a function project and create a local function in the function project.

3. After the agent completes the creation of the function project and local function, you can verify whether the function project and local function were successfully created.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aea6754b6ccb417ef1ba7c66be43ab6f.png) </span>


<span id="use-edge-functions-mcp-server-in-trae"></span>
### Use Edge Functions MCP server in Trae

This document uses Trae's default agent BuilderWithMCP as an example to show how to use the Edge Functions MCP server.


1. In the AI Side Bar, enter `@` to select the BuilderWithMCP agent.

2. Send a prompt to the agent to indicate the agent to create an Edge Functions project in the specified directory. The agent will call the Edge Functions CLI through the Edge Functions MCP server to create a function project and create a local function in the function project.

3. After the agent completes the creation of the function project and local function, you can verify whether the function project and local function were successfully created.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a622388c8387632eefb2432e10f8bef5.png) </span>


&nbsp;

<span id="setting-access-key-id-and-secret-access-key"></span>
## Setting Access Key ID and Secret Access Key

Edge Functions MCP service is essentially Edge Functions CLI. Some commands in Edge Functions CLI need to obtain Access Key ID and Secret Access Key from the project configuration file. If you need to run these commands, you must set Access Key ID and Secret Access Key in the project configuration file.

Project configurations can be categorized into function project configurations and global project configurations.


* **Function project configuration**: Saved in the `nest.json` file in the root directory of each function project. The function project configuration file applies to the current project.

* **Global project configuration**: Saved in the `~/.nest.json` file. The global project configuration file applies to all function projects.


Edge Functions CLI prioritizes obtaining project configurations from the function project configuration file. If the project configuration retrieval fails, Edge Functions CLI obtains project configurations from the global project configuration file.

If you haven't installed Edge Functions CLI, you won't have a global project configuration file locally. Therefore, after calling the init_project tool to create a function project, you need to set the Access Key ID and Secret Access Key in the function project configuration file. For example, in the function project configuration file below, you need to:


* Set the value of the `access_key` parameter to your Access Key ID.

* Set the value of the `secret_key` parameter to your Secret Access Key.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can obtain your access key ID and secret access key from the <a href="https://console.byteplus.com/iam/keymanage">BytePlus Console</a>.</div>


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
