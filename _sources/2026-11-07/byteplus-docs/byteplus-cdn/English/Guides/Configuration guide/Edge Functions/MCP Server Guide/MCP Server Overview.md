---
title: "MCP Server Overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-mcp-server-overview-en"
---

The [MCP Protocol](https://modelcontextprotocol.io/introduction) (Model Context Protocol) provides a standard way to connect LLMs (Large Language Models) and external services.


* MCP host: A program that accesses MCP services, such as Claude Desktop, IDE, or other AI tools.

* MCP client: A process running within the MCP host. It provides a standardized way for large language models to call external services or access external data.

* MCP server: A program that provides services to MCP clients through the MCP protocol. It exposes services as tools to MCP clients and exposes data as resources to MCP clients.


The MCP server provided by Edge Functions exposes the Edge Functions CLI as a tool to MCP clients. You can use MCP hosts such as Cursor, Cline or Trae to call the Edge Functions CLI.
