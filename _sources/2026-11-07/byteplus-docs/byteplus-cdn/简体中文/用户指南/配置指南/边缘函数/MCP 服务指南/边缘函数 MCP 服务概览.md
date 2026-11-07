---
title: "边缘函数 MCP 服务概览"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-mcp-server-overview-zh-cn"
---

[MCP 协议](https://modelcontextprotocol.io/introduction)（Model Context Protocol）提供了一种标准的方法来连接大语言模型和外部服务。


* MCP 主机：访问 MCP 服务的程序，例如 Claude Desktop、IDE 或其他 AI 工具。

* MCP 客户端：运行在 MCP 主机内的进程。为大语言模型提供调用外部服务或访问外部数据的标准化方式。

* MCP 服务器：通过 MCP 协议为 MCP 客户端提供服务的程序。把服务作为工具暴露给 MCP 客户端；把数据作为资源暴露给 MCP 客户端。


边缘函数提供的 MCP 服务把边缘函数 CLI 作为工具暴露给 MCP 客户端。您可以使用 Cursor、Cline 或 Trae 等 MCP 主机调用边缘函数 CLI。
