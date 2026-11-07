---
title: "初心者向け：CLIでローカル関数を作成し公開する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-quickstart-jp"
---

このチュートリアルでは、簡単な例のシナリオに基づいて、デバイス上でエッジ関数CLIを使用してローカル関数を作成し、公開する方法を紹介します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">現在、エッジ関数の使用によってByteplusアカウントに料金は発生しません。</div>


<span id="例のシナリオ"></span>
## 例のシナリオ

あなたは`www.example.com`というドメイン名のウェブサイトを持っています。このドメインをByteplus CDNに追加しました。エッジ関数を使用して、ユーザーにカスタムページを送信したいと考えています。

<span id="実行環境"></span>
## 実行環境

エッジ関数CLIを実行するデバイスは、以下の要件を満たす必要があります：


* オペレーティングシステムは以下のいずれかである必要があります：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* [Node.js](https://nodejs.org/)と[npm](https://www.npmjs.com/)がインストールされている。バージョン要件は以下の通りです：

   * Node.js: 8.17.0+

   * npm: 6.13.4+

* [wget](https://www.gnu.org/software/wget/)または[cURL](https://curl.se/)がインストールされている。


<span id="手順"></span>
## 手順

デバイス上でエッジ関数CLIを使用するには、以下の手順に従ってください。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7c863e5bda23d80107d7e82823bfa39c.png) </span>


1.  **エッジ関数CLIをインストールしてローカル関数を作成する** : `nest init`コマンドを使用して、エッジ関数CLIをインストールし、ローカル関数を作成します。

2. **Access Key IDとSecret Access Keyを設定する** : エッジ関数CLIを使用して、ByteplusアカウントのAccess Key IDとSecret Access Keyを設定します。

3.  **コードを編集してデバッグする** : ローカル関数のコードを編集してデバッグします。

4.  **ローカル関数を公開する** : ローカル関数をByteplus CDNのグローバルエッジノードに公開します。

5.  **ドメインを関連付けて転送ルールを設定する** : 関数のトリガーをドメイントリガーとして設定し、ドメイントリガーで関数をドメインに関連付けます。同時に、ドメインの転送ルールを設定します。Byteplus CDNが転送ルールに一致するユーザーからのリクエストを受信すると、そのユーザーからのリクエストをエッジ関数に転送します。

6. **関数を検証する** : 関数の実際の実行結果が期待通りかどうかを検証します。


<span id="ステップ1：エッジ関数cliをインストールしてローカル関数を作成する"></span>
### ステップ1：エッジ関数CLIをインストールしてローカル関数を作成する

デバイス上で以下のコマンドを実行します。このコマンドはエッジ関数CLIをインストールし、関数プロジェクトを作成し、その関数プロジェクト内にローカル関数を作成します。[nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-jp)を参照してください。

```shell
$ npx @byteplus/nest@latest init
```


コマンドラインのプロンプトに従って関数名を`HelloWorld`に設定し、他の設定はEnterキーを押してデフォルト値に設定する必要があります。以下の例では、コマンドを実行するディレクトリが`/Users/MyFolder`であると仮定しています。

```shell
Need to install the following packages:
@byteplus/nest@1.0.0
Ok to proceed? (y) y
    
==> [debug]: Loading function from file "nest.json"
==> [debug]: Failed to load function config, read file "nest.json" error: open nest.json: no such file or directory
==> [debug]: Temporary function configuration will be used
✓ Name: HelloWorld
==> [info]: No AK&SK found, you can login to get more function templates. see also `nest config -h`
✓ Select a template you want to start with: Hello World
✓ Put code file in src/ directory?: Yes
✓ Entry File in src/ (optional, default is index.js): index.js
✓ Project Name (optional, default is "default"): 
✓ Description: 
==> 🛠️  Creating a BytePlus Function `HelloWorld` in directory /Users/MyFolder/HelloWorld ...
==> [info]: 📦  Generating package.json...
==> [info]: 🧾  Generating nest.json for project...
==> [info]: 🖨️  Generating code files from template...✓
==> [info]: 📥  Installing dependencies...✓
==> [info]: 👏  Done!, New function created at ./HelloWorld
    
==> Continue Developing
==> [info]: Change directory: cd ./HelloWorld
==> [info]: Start dev server: npm run start
    
==> Publish Function
==> [info]: Setting access_key: npm run nest config -g set cloud.access_key <your_access_key>
==> [info]: Setting secret_key: npm run nest config -g set cloud.secret_key <your_secret_key>
==> [info]: Deploy function: npm run deploy
==> [info]: 💡  You can find your AKSK at BytePlus(https://console.byteplus.com/iam/keymanage)
```


コマンドが実行された後、現在のディレクトリ構造は以下のようになります：

```markdown
└── 📁MyFolder
    └── 📁HelloWorld
        └── nest.json
        └── package-lock.json
        └── package.json
        └── 📁src
            └── index.js
    └── package.json
```


ここで、`HelloWorld`ディレクトリは作成した関数プロジェクトで、`HelloWorld/src/index.js`はローカル関数のエントリーファイルです。

次に、Access Key IDとSecret Access Keyを設定する必要があります。

<span id="ステップ2：access-key-idとsecret-access-keyを設定する"></span>
### ステップ2：Access Key IDとSecret Access Keyを設定する

`HelloWorld`ディレクトリで以下のコマンドを実行して、エッジ関数CLIにAccess Key IDとSecret Access Keyを設定します。Access Key IDとSecret Access Keyは[BytePlus Console](https://console.byteplus.com/iam/keymanage)から取得できます。[nest config](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-config-jp)を参照してください。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


次に、ローカル関数のコードを編集してデバッグできます。

<span id="ステップ3：コードを編集してデバッグする"></span>
### ステップ3：コードを編集してデバッグする

以下の手順に従って、ローカル関数のコードを編集してデバッグします。


1. 任意のコードエディタで`HelloWorld/src/index.js`ファイルを開き、必要に応じてコードを修正します。このチュートリアルではHelloWorldテンプレートが提供するコードを使用します。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">このコードは<a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-addEventListener-jp">addEventListener()</a>を呼び出してイベントリスナーを登録します。渡されるパラメータには<code>fetch</code>とコールバック関数<code>{event.respondWith(handleResponse(event));}が含まれます。</code>fetch`はこのイベントリスナーがフェッチイベントをリッスンすることを示し、ドメイントリガーによってフェッチイベントがトリガーされた場合、コールバック関数が呼び出されます。ステップ5で関数のドメイントリガーを設定します。<a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-FetchEvent-jp">FetchEvent</a>を参照してください。   </div>
   

   ```JavaScript
   /**
    * Add the necessary event listener
    * @param {Event} fetch event, {Function} async function
    */
   addEventListener('fetch', event => {
     event.respondWith(handleRequest(event.request));
   })
   
   /**
    * Make a response to client
    * @param {Request} request
    */
   async function handleRequest(request) {
     return new Response('Hello World!', { status: 200 });
   }
   ```
   

2. `HelloWorld`ディレクトリで以下のコマンドを実行して、Debuggerコマンドラインに入り、コードをデバッグします。コードをデバッグする前に、`source`コマンドを実行して関数コードをDebuggerにアップロードする必要があります。Debuggerコマンドラインの使用方法については、[nest debug](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-jp)を参照してください。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">一定時間Debuggerコマンドラインを操作しないと、Debuggerコマンドラインが切断され、<strong>Error: ws connection closed by server for timeout</strong>エラーが報告されます。<code>npx nest debug</code>を実行してDebuggerコマンドラインを再起動できます。   </div>
   

   ```shell
   $ npx nest debug
     ______    _              ______                _   _             
    |  ____|  | |            |  ____|              | | (_)            
    | |__   __| | __ _  ___  | |__ _   _ _ __   ___| |_ _  ___  _ __  
    |  __| / _` |/ _` |/ _ \ |  __| | | | '_ \ / __| __| |/ _ \| '_ \ 
    | |___| (_| | (_| |  __/ | |  | |_| | | | | (__| |_| | (_) | | | |
    |______\__,_|\__, |\___| |_|   \__,_|_| |_|\___|\__|_|\___/|_| |_|
                  __/ |                                               
                 |___/                                                
                 
   ==> Setting up debugger...
   ==> [info]: connection setup successfully!
   ==> [info]: loading envrionment variables... ✓
   nest:  
   ```
   

   例えば、以下の例では、まず`source`を実行して関数コードをDebuggerにアップロードし、次に`query`を実行して関数コードの実行をトリガーしています。

   ```shell
   nest: source
   ==> [info]: building function "HelloWorld"... 
   ==> Uploading functions: [HelloWorld]... 
   nest: query
   ==> HttpResponse ✓
   status: 200
   
   statusText: OK
   
   header:
     content-type => text/plain;charset=UTF-8
     date => Fri, 17 Jan 2025 06:07:53 GMT
     server => Sparrow
     transfer-encoding => chunked
   
   body:
   Hello World!
   ```
   


関数コードをデバッグした後、ローカル関数を公開できます。

<span id="ステップ4：ローカル関数を公開する"></span>
### ステップ4：ローカル関数を公開する

`HelloWorld`ディレクトリで以下のコマンドを実行して、ローカル関数をグローバルエッジノードに公開します。関数をドメインに関連付ける前に、関数を完全に公開する必要があります。[nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-jp)を参照してください。

```shell
npx nest deploy --message "This is a new version"
```


コマンドラインは新しい関数IDを作成するかどうかを尋ねます。Yesを選択してEnterを押します。エッジ関数CLIはエッジ関数に対応するリモート関数を作成し、ローカル関数と同期します。その後、エッジ関数CLIはこのリモート関数をグローバルエッジノードに公開します。

```shell
$ npx nest deploy --message "This is a new version"
==> Deploying function "HelloWorld"...
✓ Function HelloWorld has no id, create a new one for it?: Yes
==> [info]: Register function on remote cloud...✓
==> [info]: Building function "HelloWorld", entry=/Users/MyFolder/HelloWorld/src/index.js ... ✓
==> [info]: function "HelloWorld" was built into /Users/MyFolder/HelloWorld/output/HelloWorld/index.js .
==> [info]: Uploading "/Users/MyFolder/HelloWorld/output/HelloWorld/index.js" to remote cloud...✓
==> [info]: Publishing function code to edge node...✓
==> [info]: Function HelloWorld publish started, the ticket is 1887
==> [info]: Loading deploy ticket status...✓
==> [info]: The Full publish now is Publishing, version is: 1.0.1
==> [info]: Run `nest tickets 1887` to get more details

==> All functions were deployed successfully.
```


次に、ローカル関数にドメインを関連付ける必要があります。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">関数の完全な公開には通常5〜10分かかります。関数をドメインに関連付ける前に、関数が完全に公開されるのを待つ必要があります。</div>


<span id="ステップ5：ドメインを関連付けて転送ルールを設定する"></span>
### ステップ5：ドメインを関連付けて転送ルールを設定する

この例では、ドメイントリガーを使用して関数の実行をトリガーします。したがって、関数をドメイン`www.example.com`に関連付ける必要があります。ドメインの転送ルールを設定した後、BytePlus CDNが転送ルールに一致するユーザーからのリクエストを受信すると、そのリクエストをエッジ関数に転送します。さらに、ドメイントリガーは関数内のフェッチイベントをトリガーします。

以下のコマンドを実行して、ローカル関数をドメイン`www.example.com`に関連付け、ドメインの転送ルールを設定します。[nest domain](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-domain-jp)を参照してください。この例ではユーザーからのリクエストURLのパスを制限しないため：


* ルールタイプは`--url-directory`に設定する必要があります。これはURLディレクトリを意味します。

* ルールは`/`に設定する必要があります。これはドメイン下のすべてのパスに一致することを示します。


```shell
$ npx nest domain bind www.example.com   --url-directory /
==> [info]: Binding new domains to function...✓
==> [info]: Applying forward rules to domains...✓
```


数分待つ必要があります。その後、HelloWorldディレクトリで`npx nest domain list`コマンドを実行して、ローカル関数がドメインに正常に関連付けられ、このローカル関数のドメイントリガーが有効になっているかどうかを確認します。

```shell
$ npx nest domain list
+---------------------------+--------+-----------+---------+------------+
|          DOMAIN           | STATUS |   TYPE    | PATTERN | IGNORECASE |
+---------------------------+--------+-----------+---------+------------+
| www.example.com           | Online | directory | /       | false      |
+---------------------------+--------+-----------+---------+------------+
```


www.example.comがドメインリストに表示され、そのステータスが**Online**の場合、このドメインのドメイントリガーが有効になっていることを示します。この時点で、ユーザーがこのドメインにHTTPまたはHTTPSリクエストを送信し、そのリクエストが転送ルールに一致する場合、ドメイントリガーはこのドメインに関連付けられた関数内のフェッチイベントをトリガーします。

次に、関数の実行結果が期待通りかどうかを検証します。

<span id="ステップ6：関数を検証する"></span>
### ステップ6：関数を検証する

www.example.comにアクセスし、ウェブページのレスポンス内容が`Hello World!`であることを確認できます。検証が成功した場合、例のシナリオが実装されたことを意味します。
