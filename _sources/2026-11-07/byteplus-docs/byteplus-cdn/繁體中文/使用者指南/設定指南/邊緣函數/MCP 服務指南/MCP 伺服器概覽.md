---
title: "MCP 伺服器概覽"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-mcp-server-overview-zh-tw"
---

[MCP 協定](https://modelcontextprotocol.io/introduction)（Model Context Protocol）提供了一種標準的方法來連接大語言模型和外部服務。


* MCP 主機：存取 MCP 伺服器的程式，例如 Claude Desktop、IDE 或其他 AI 工具。

* MCP 用戶端：執行在 MCP 主機內的程序。為大型語言模型提供呼叫外部服務或存取外部資料的標準化方式。

* MCP 伺服器：透過 MCP 協議為 MCP 用戶端提供服務的程式。將服務作為工具暴露給 MCP 用戶端；將資料作為資源暴露給 MCP 用戶端。


邊緣函數提供的 MCP 服務把邊緣函數 CLI 作為工具暴露給 MCP 用戶端。您可以使用 Cursor、Cline 或 Trae 等 MCP 主機調用邊緣函數 CLI。
