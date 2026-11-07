---
title: "MCPサーバーを利用する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/integrate-mcp-server-jp"
---

このドキュメントでは、エッジ関数MCPサーバーをMCPホストに追加し、エッジ関数MCPサーバーを使用する方法について説明します。

<span id="ランタイム環境要件"></span>
## ランタイム環境要件

エッジ関数CLIの[ランタイム環境要件](https://docs.byteplus.com/docs/byteplus-cdn/get-started-with-edge-function-cli-jp#system-requirements)を参照してください。

<span id="エッジ関数mcpサーバーをmcpホストに追加する"></span>
## エッジ関数MCPサーバーをMCPホストに追加する

エッジ関数は、[Claude for Desktop用のMCPサーバー設定ファイル](https://modelcontextprotocol.io/quickstart/user)を提供しています。この設定ファイルは、CursorやClineやTraeなどのMCPホストとも互換性があります。MCPサーバー設定ファイルは、実行時にMCPクライアントが起動する必要があるMCPサーバーと、MCPサーバーを起動するために必要なコマンドとパラメータを指定します。

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


このドキュメントでは、[Cursor](https://www.cursor.com/)と[Trae](https://www.trae.ai/)を例として、エッジ関数MCPサーバーの設定をMCPホストに追加する方法を説明します。

<span id="エッジ関数mcpサーバーをcursorに追加する"></span>
### エッジ関数MCPサーバーをCursorに追加する

このドキュメントではCursor 0.5.0を例として使用します。


1. Cursorで**Cursor Settings**を見つけ、MCPを選択し、**Add New Global MCP Server**をクリックします。Cursorがmcp.jsonファイルを開きます。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4fe1a403bac0d95238e8d85c8bf5c447.png) </span>

2. mcp.jsonファイルで、エッジ関数MCPサーバーの設定を追加し、変更を保存します。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a3514f1ce4504a9321e34fc675414871.png) </span>

3. **Cursor Settings**ページに戻ります。追加したエッジ関数MCPサーバーが表示されます。同時に、エッジ関数MCPサーバーが起動します。起動が完了すると、エッジ関数MCPサーバーの左側のドットが緑色に変わります。この時点で、Cursor Agentでエッジ関数MCPサーバーを使用できます。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e7211764ef55ec0867fc8d12a7a35617.png) </span>


<span id="エッジ関数mcpサーバーをtraeに追加する"></span>
### エッジ関数MCPサーバーをTraeに追加する

このドキュメントではTrae 0.5.9を例として使用します。


1. TraeのAIサイドバーで、**MCP**タブを選択します。**Add**をクリックします。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">AIサイドバーにMCPタブがない場合は、右側の歯車アイコンをクリックし、ドロップダウンメニューからMCPタブを選択できます。   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_87b5606b3c985fae2564e1b04fbde18b.png) </span>

2. **Configure Manually**をクリックします。**Configure Manually**ウィンドウで、エッジ関数MCPサーバー設定ファイルの内容を貼り付けます。**Confirm**をクリックします。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b36275d0133d6e53a221c653e228b318.png) </span>

   エッジ関数MCPサーバーがデフォルトエージェントのBuilderWithMCPに追加されます。同時に、エッジ関数MCPサーバーが起動します。起動が完了すると、エッジ関数MCPサーバーのステータスが**Ready**に変わります。この時点で、デフォルトエージェントBuilderWithMCPでエッジ関数MCPサーバーを使用できます。また、他のTraeエージェントにもエッジ関数MCPサーバーを追加できます。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_533a54431de7625f0e85b2911a1b6e49.png) </span>


<span id="エッジ関数mcpサーバーを使用する"></span>
## エッジ関数MCPサーバーを使用する

エッジ関数MCPサーバーは、エッジ関数CLIを通じて以下のツールをMCPクライアントに提供します：


* **init_project**: 関数プロジェクトを作成し、関数プロジェクト内にローカル関数を作成します（[nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-jp)に相当）。

* **add_function**: 関数プロジェクト内に関数を作成します（[nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#create)に相当）。[Access Key IDとSecret Access Keyを設定する](https://docs.byteplus.com/en/docs/18/47090#set-ak-sk)ことがが必要です。

* **pull_function**: リモート関数のコードをローカル関数に同期します（[nest functions pull](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#pull)に相当）。[Access Key IDとSecret Access Keyを設定する](https://docs.byteplus.com/en/docs/18/47090#set-ak-sk)ことがが必要です。

* **deploy_function**: ローカル関数をエッジノードにデプロイします（[nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-jp)に相当）。[Access Key IDとSecret Access Keyを設定する](https://docs.byteplus.com/en/docs/18/47090#set-ak-sk)ことがが必要です。

* **start_function**: 関数コードを実行します（[nest start](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-start-jp)に相当）。


プロンプトを使用して、MCPクライアントに呼び出したいツールとツールに渡すパラメータを説明することができます。MCPクライアントは、プロンプトに基づいて完了すべきタスクを計画し、対応するエッジ関数CLIコマンドを実行します。関数プロジェクトのディレクトリがLLMのコンテキストに含まれていることを確認する必要があります。

<span id="cursorでエッジ関数mcpサーバーを使用する"></span>
### Cursorでエッジ関数MCPサーバーを使用する


1. AIペインで、会話オブジェクトとしてAgentを選択します。

2. エージェントに指定のディレクトリにエッジ関数プロジェクトを作成するようプロンプトを送信します。エージェントはエッジ関数MCPサーバーを通じてエッジ関数CLIを呼び出し、関数プロジェクトを作成し、関数プロジェクト内にローカル関数を作成します。

3. エージェントが関数プロジェクトとローカル関数の作成を完了したら、それらが正常に作成されたことを確認できます。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aea6754b6ccb417ef1ba7c66be43ab6f.png) </span>


<span id="traeでエッジ関数mcpサーバーを使用する"></span>
### Traeでエッジ関数MCPサーバーを使用する

このドキュメントでは、TraeのデフォルトエージェントBuilderWithMCPを例として、エッジ関数MCPサーバーの使用方法を説明します。


1. AIサイドバーで、`@`を入力してBuilderWithMCPエージェントを選択します。

2. エージェントに指定のディレクトリにエッジ関数プロジェクトを作成するようプロンプトを送信します。エージェントはエッジ関数MCPサーバーを通じてエッジ関数CLIを呼び出し、関数プロジェクトを作成し、関数プロジェクト内にローカル関数を作成します。

3. エージェントが関数プロジェクトとローカル関数の作成を完了したら、それらが正常に作成されたことを確認できます。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a622388c8387632eefb2432e10f8bef5.png) </span>


&nbsp;

<span id="access-key-idとsecret-access-keyを設定する"></span>
## Access Key IDとSecret Access Keyを設定する

エッジ関数MCPサービスは本質的にエッジ関数CLIです。エッジ関数CLIの一部のコマンドは、プロジェクト設定ファイルからAccess Key IDとSecret Access Keyを取得する必要があります。これらのコマンドを実行する必要がある場合は、プロジェクト設定ファイルにAccess Key IDとSecret Access Keyを設定する必要があります。

プロジェクト設定は、関数プロジェクト設定とグローバルプロジェクト設定に分類できます。


* **関数プロジェクト設定**：各関数プロジェクトのルートディレクトリにある`nest.json`ファイルに保存されます。関数プロジェクト設定ファイルは現在のプロジェクトに適用されます。

*  **グローバルプロジェクト設定**：`~/.nest.json`ファイルに保存されます。グローバルプロジェクト設定ファイルはすべての関数プロジェクトに適用されます。


エッジ関数CLIは、まず関数プロジェクト設定ファイルからプロジェクト設定を取得します。プロジェクト設定の取得に失敗した場合、エッジ関数CLIはグローバルプロジェクト設定ファイルからプロジェクト設定を取得します。

エッジ関数CLIをインストールしていない場合、ローカルにグローバルプロジェクト設定ファイルはありません。したがって、init_project ツールを呼び出して関数プロジェクトを作成した後、関数プロジェクト設定ファイルに Access Key IDとSecret Access Key を設定する必要があります。例えば、以下の関数プロジェクト設定ファイルでは、次のことが必要です：


* `access_key`パラメータの値をあなたのAccess Key IDに設定します。

* `secret_key`パラメータの値をあなたのSecret Access Keyに設定します。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Access Key IDとSecret Access Keyは<a href="https://console.byteplus.com/iam/keymanage">BytePlus Console</a>から取得できます。</div>


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
