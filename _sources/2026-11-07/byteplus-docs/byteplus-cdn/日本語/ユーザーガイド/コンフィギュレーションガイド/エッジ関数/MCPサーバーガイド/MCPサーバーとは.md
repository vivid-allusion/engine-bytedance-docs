---
title: "MCPサーバーとは"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-mcp-server-overview-jp"
---

[MCPプロトコル](https://modelcontextprotocol.io/introduction)（Model Context Protocol）は、大規模言語モデルと外部サービスを接続するための標準的な方法を提供します。


* MCPホスト：MCPサービスにアクセスするプログラム。例えば、Claude Desktop、IDE、または他のAIツールなど。

* MCPクライアント：MCPホスト内で実行されるプロセス。大規模言語モデルに外部サービスの呼び出しや外部データへのアクセスを提供する標準化された方法。

* MCPサーバー：MCPプロトコルを通じてMCPクライアントにサービスを提供するプログラム。サービスをツールとしてMCPクライアントに公開し、データをリソースとしてMCPクライアントに公開する。


エッジ関数が提供するMCPサーバーは、エッジ関数CLIをツールとしてMCPクライアントに公開します。CursorやClineやTraeなどのMCPホストを使用してエッジ関数CLIを呼び出すことができます。
