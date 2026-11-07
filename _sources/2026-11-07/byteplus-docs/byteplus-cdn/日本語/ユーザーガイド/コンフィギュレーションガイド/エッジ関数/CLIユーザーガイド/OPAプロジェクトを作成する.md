---
title: "OPAプロジェクトを作成する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/create_function_project_with_opa_jp"
---

このドキュメントでは、エッジ関数CLIを使用して、[Open Policy Agent (OPA)](https://www.openpolicyagent.org/)をサポートする関数プロジェクトを作成する方法について説明します。

<span id="opaとは"></span>
## OPAとは

OPAは、クラウドネイティブ技術スタック全体のポリシー適用を統一する、オープンソースの汎用ポリシーエンジンです。OPAは、ポリシーをコードとして記述し、ポリシーの実装をサービス自体のロジックから切り離すことができる高レベルの宣言型言語 Regoを提供します。

サービスがポリシーベースの決定を行う必要がある場合、入力データをOPAに送信します。OPAは事前に定義されたポリシーに基づいて入力データを評価し、決定結果を生成します。この結果は、単純なブール値 (許可または拒否など) にすることも、より複雑な構造化ドキュメントにすることもできます。ポリシーは宣言型言語で記述されているため、ポリシー自体の内容に集中でき、OPAはこれらのポリシーを実行する責任を負います。

<span id="opaの適用シナリオ"></span>
## OPAの適用シナリオ

OPAの柔軟性により、ユーザーからのリクエストの認証や RBAC アクセス制御など、さまざまな複雑な適用シナリオに適しています。

<span id="ユーザーからのリクエストの認証"></span>
### ユーザーからのリクエストの認証

エッジコンピューティングでは、リクエストがオリジンサーバーに到達する前にユーザーを認証および承認することが一般的な要件です。たとえば、OPAを使用して有料コンテンツを保護し、未承認のリクエストをフィルタリングすることで、オリジンサーバーのセキュリティを強化できます。

<span id="rbac-アクセス制御"></span>
### RBAC アクセス制御

ロールベースのアクセス制御 (RBAC)は、ユーザーのロールと責任に基づいてリソースへのアクセスを許可します。たとえば、企業内では、従業員の役職や職務に基づいて、さまざまなレベルのシステムアクセスを許可できます。OPAを使用して、複雑な RBAC ポリシーを定義および実装できます。例えば、管理者ロールを持つユーザーのみが特定のAPIにアクセスでき、訪問者ロールのユーザーは別のAPIにのみアクセスできるというポリシーを定義することができます。

<span id="エッジ関数がopaポリシーを評価する方法"></span>
## エッジ関数がOPAポリシーを評価する方法

エッジ関数は、そのランタイムに組み込まれたWebAssembly（Wasm）モジュールを通じてOPAポリシーを評価します。このモジュールは、`.rego`ファイルからコンパイルされた`.wasm`ファイルの読み込みと実行を担当します。エッジ関数CLIを使用して、これらの`.wasm`ファイルをエッジ関数にアップロードできます。関数がHTTPリクエストを受信すると、Wasmモジュールはリクエスト情報に基づいてポリシーを評価し、決定結果を返します。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_795486d1f0d9a6e9b5df4d1467e893c4.jpeg) </span>

エッジ関数ランタイムのWasmモジュールがOPAポリシーを評価する具体的なプロセスは次のとおりです：


1. **入力の準備**：関数はHTTPリクエストによってトリガーされる`fetch`イベントをリッスンします。`fetch`イベントがトリガーされると、関数はそのHTTPリクエストから必要なデータ（ヘッダー、URL、JWTなど）を抽出し、抽出されたデータに基づいてJSONドキュメントを生成し、Wasmモジュールによるポリシー評価の入力として使用します。例えば、単純なJSONドキュメントは次のように表示されます：

   ```json
   {
     "method": "GET"
   }
   ```
   

   このJSONドキュメントは、評価のためにWasmモジュールに渡されます。たとえば、単純なポリシーファイル (`policy.rego`)は次のようになり、`GET` メソッドのみを許可するように指定します。

   ```rego
       package example
       
       default allow := false
       
       allow if {
           input.method == "GET"
       }
   ```
   

2.  **ポリシー評価の実行**: 関数は、Wasm モジュールに読み込まれたポリシーを呼び出し、生成したJSONドキュメントを渡します。 Wasm モジュールはポリシーロジックに従って入力データを評価します。

3. **決定結果の返却**: Wasm モジュールは決定結果を含むJSONドキュメントを返します。例えば、 `[{"result": {"allow": true}}]`。

4. **決定の実行**: 決定結果を受信した後、関数は結果に基づいて対応するビジネスロジック (リクエストの許可または拒否、ヘッダーの書き換えなど)を実行できます。

   たとえば、ポリシー評価を実行した後、評価結果の `allow` フィールドを確認できます。`true`の場合はリクエストを許可し、それ以外の場合は 403 Forbidden エラーを返します。

   ```javascript
   const r = policy.eval(input);
   
   let allow = false;
   if (r.length === 1 && r[0]["result"] === true) {
     allow = true;
   }
   
   if (!allow) {
     return new Response("Forbidden", {
       status: 403,
       statusText: "Forbidden",
     });
   }
   
   return new Response("OK", { status: 200, statusText: "OK" });
   ```
   


さらに、開発プロセスを簡素化するために、エッジ関数CLI には OPA コンパイルツールチェーンが組み込まれており、`.rego` ファイルを `.wasm` ファイルに直接コンパイルできます。この設計により、基盤となるコンパイルと統合の詳細を気にすることなく、JavaScriptコードでOPAポリシーを呼び出すことができます。

<span id="opaをサポートする関数プロジェクトの作成、デバッグ、公開"></span>
## OPAをサポートする関数プロジェクトの作成、デバッグ、公開

このセクションでは、エッジ関数CLIを使用して、OPAをサポートする関数プロジェクトを作成、デバッグ、公開する方法について説明します。

<span id="ステップ-1-opaをサポートする関数プロジェクトを作成する"></span>
### ステップ 1: OPAをサポートする関数プロジェクトを作成する

デバイスで次のコマンドを実行します。このコマンドは、エッジ関数CLIをインストールし、OPAをサポートする関数プロジェクトを作成し、関数プロジェクトにローカル関数を作成します。[nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-jp)を参照してください。

```shell
$ npx @byteplus/nest@latest init
```


コマンドラインのプロンプトに従って、関数が使用するテンプレートを `OPA` に設定し、必要に応じて他のパラメーターを設定する必要があります。この記事では、関数の名前が `opa-demo` であると仮定します。

```bash
$ npx @byteplus/nest@latest init opa  
✓ Name: opa-demo
==> [info]: No AK&SK found, you can login to get more function templates. see also `nest config -h`
✓ Select a template you want to start with: OPA
✓ Put code file in src/ directory?: Yes
✓ Entry File in src/ (optional, default is index.js): index.js
✓ Project Name (optional, default is "default"): 
✓ Description: An OPA function project
```


コマンドの実行後、関数プロジェクトの構造は次のようになります。

```Plain Text
opa-demo/
├── src/
│   ├── index.js         # JavaScript コードのエントリファイル
│   ├── opa-wasm-sdk/    # OPA Javascript SDK
│   └── opa-demo.rego    # OPA ポリシーファイル
├── nest.json            # プロジェクト構成ファイル
├── package.json         # Node.js プロジェクト情報
└── node_modules/
```



* **`src/index.js`**: JavaScript コードのエントリファイル。このファイルで OPA ポリシーを呼び出します。

* **`src/opa-demo.rego`**: Rego 言語で記述された OPA ポリシーファイル。

* **`src/opa-wasm-sdk`**: エッジ関数が提供する OPA JavaScript SDK。この SDKは [OPA Wasm Javascript Module](https://www.openpolicyagent.org/ecosystem/entry/opa-wasm-js) に基づいて開発されていますが、両者は完全に同じではありません。この SDKはすでにプロジェクトに埋め込まれています。`index.js` でこの SDKを直接使用できます。

* **`nest.json`**: 関数プロジェクトの構成ファイル。


プロジェクトが作成されたら、次のステップは、ビジネスニーズに応じて OPA ポリシーを編集することです。

<span id="ステップ-2-opa-ポリシーを編集する"></span>
### ステップ 2: OPA ポリシーを編集する

`OPA` テンプレートは、`src/opa-demo.rego` に初期 OPA ポリシーファイルを提供します。任意のコードエディターでこのファイルを開き、必要に応じてコードを変更できます。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">エッジ関数は OPAのバージョン 1.4.2のみをサポートします。したがって、OPA バージョン 1.4.2の組み込み関数のみを使用できます。OPA 組み込み関数の使用方法については、<a href="https://v1-4-2--opa-docs.netlify.app/policy-reference">バージョン 1.4.2のポリシーリファレンス</a>を参照してください。ただし、エッジ関数でサポートされていない組み込み関数またはカスタム関数を JavaScript コードで実装し、<code>loadPolicy()</code> メソッドを介して実装した関数を読み込むことができます。<a href="https://docs.byteplus.com/en/docs/18/57424#loadpolicy">loadPolicy()</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="warning">エッジ関数CLIは、Rego コードが OPA v1 標準に準拠していることをデフォルトとします。Rego コードが OPA v0の機能を使用している場合は、<code>nest.json</code> ファイルの <code>attachment.rego_version</code> フィールドを介して必要な互換性バージョンを明示的に指定する必要があります。<a href="https://docs.byteplus.com/en/docs/18/57424#rego-%E8%A8%80%E8%AA%9E%E3%83%90%E3%83%BC%E3%82%B8%E3%83%A7%E3%83%B3%E3%81%AE%E4%BA%92%E6%8F%9B%E6%80%A7%E3%81%AB%E9%96%A2%E3%81%99%E3%82%8B%E8%AA%AC%E6%98%8E">Rego 言語バージョンの互換性に関する説明</a>を参照してください。</div>



```rego
package example

default allow := false

allow if {
    input.method == "GET"
}
```


OPA プロジェクトの場合、`nest.json` ファイルの `attachment` フィールドは、エッジ関数CLI が OPA ポリシーファイルを処理する方法を定義するために使用されます。


* **`rego_paths`**: OPA ポリシーファイルのパスを指定するために使用されます。Regoは OPA が使用するポリシー言語です。したがって、`rego_paths`は、決定ロジックを含む `.rego` ファイルがどこにあるかをシステムに伝えます。

* **`entrypoints`**: OPA ポリシーファイルでクエリできる特定のルールを定義します。ポリシー評価が必要な場合、システムはここで定義された特定のルールを呼び出して決定結果を取得します。


以下は、`attachment` フィールドの構成例です。この例では、


* `["src/opa-demo.rego"]`は、ポリシーファイルが `src/opa-demo.rego` にあることを示します。

* `["example/allow"]`は、example という名前のパッケージ内の allow ルールを参照します。これは、外部システムが example.allow ルールの評価を要求できることを意味します。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">エッジ関数CLI に <code>.rego</code> ファイルからコンパイルさせるのではなく、カスタムのプリコンパイル済み <code>.wasm</code> ファイルを使用する場合は、<code>nest.json</code> で <code>functions.attachment.wasm_path</code> フィールドを構成し、Wasm ファイルのパスを指すようにします。</div>


```json
  "functions": [
    {
      "id": "",
      "name": "opa-demo",
      "type": "opa",
      "entry": "src/index.js",
      "attachment": {
        "rego_paths": [
          "src/opa-demo.rego"
        ],
        "entrypoints": [
          "example/allow"
        ]
      },
      "region": "outside_chinese_mainland"
    }
  ]
```


OPA ポリシーを定義したら、関数コードを編集して、関数で OPA ポリシーを呼び出して決定を下せるようにする必要があります。

<span id="ステップ-3-関数コードを編集する"></span>
### ステップ 3: 関数コードを編集する

`OPA` テンプレートは、`src/index.js` に初期 JavaScript コードファイルを提供します。このファイルは、OPA Javascript SDKを読み込み、OPA ポリシーファイルで定義されたルールに基づいて決定を下します。この SDKは OPA Wasm Javascript Module に基づいて開発されていますが、両者は完全に同じではありません。この SDKの使用方法については [OPA JavaScript SDKリファレンス](https://docs.byteplus.com/en/docs/18/57424#opa-javascript-sdk%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9)を参照し、必要に応じてコードを変更してください。

```JavaScript
const { loadPolicy } = require("opa-wasm-sdk");

addEventListener("fetch", (event) =>
  event.respondWith(handleRequest(event.request))
);

// initialize a global opa policy
let policy = null;

/**
 * Takes in a custom function map and returns a loaded policy which can be
 * used to evaluate the policy.
 *
 * @param { Object[string, Function] } customBuiltins a map from name to custom builtins function
 * @returns {class} a loaded policy which can be used to evaluate the policy
 */
policy = loadPolicy();

function handleRequest(request) {
  if (policy == null) {
    return new Response("Policy not ready", {
      status: 503,
      statusText: "Service Unavailable",
    });
  }

  let inputJson = {
    method: request.method,
  };
  console.log(inputJson);

  /**
   * Evaluates the policy with any the given `input` and return the result set.
   * This should be re-used for multiple evaluations of the same policy with
   * different inputs.
   *
   * To call a non-default entrypoint in Wasm specify it as the second param. A
   * list of entrypoints can be accessed with the `this.entrypoints` prototype.
   *
   * The output of policy evaluation is a set of variable assignments. The
   * variable assignments specify values that satisfy the expressions in the
   * policy query (i.e., if the variables in the query are replaced with the
   * values from the assignments, all of the expressions in the query would be
   * defined and not false.)
   *
   * When policies are compiled into Wasm, the user provides the path of the
   * policy decision that should be exposed by the Wasm module. The policy
   * decision is assigned to a variable named result. The policy decision can
   * be ANY JSON value (boolean, string, object, etc.) but there will be
   * at-most-one assignment. This means that callers should first check if the
   * set of variable assignments is empty (indicating an undefined policy decision)
   * otherwise they should select the "result" key out of the variable assignment
   * set.
   *
   * @param {Object | ArrayBuffer>} input `input` parameter maybe an `object`,
   * primitive literal or `ArrayBuffer`, which assumed to be a well-formed stringified JSON.
   * @param {number | string>} entrypoints  ID or name of the entrypoint to call (optional)
   * @returns {Array} result set of evaluation（i.e.，[{"result": <value of example/allow>}]）
   */
  let r = policy.eval(inputJson);
  console.log(JSON.stringify(r));

  let allow = false;
  if (r.length === 1 && r[0]["result"] === true) {
    allow = true;
  }

  if (!allow) {
    return new Response("Forbidden", {
      status: 403,
      statusText: "Forbidden",
    });
  }

  return new Response("OK", { status: 200, statusText: "OK" });
}
```


コードの編集が完了したら、ローカル環境で関数プロジェクトをデバッグして、その動作が期待どおりであることを確認することをお勧めします。

<span id="ステップ-4-プロジェクトをデバッグする"></span>
### ステップ 4: プロジェクトをデバッグする

関数プロジェクトのルートディレクトリで [nest start](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-start-jp) コマンドを実行します。このコマンドは、`.rego` ファイルをコンパイルし、`.js` ファイルをパッケージ化し、関数コードを実行します。エッジ関数CLIは、エッジ関数Debugger用のローカル HTTP プロキシを起動し、wssプロトコルを介してエッジ関数Debuggerとの接続を確立します。

```shell
$ npx nest start
==> Local http proxy running on 127.0.0.1:18080
==> Setting up debugger on wss://byteplusef-debugger.byteintlapi.com/f6663e0c-feb0-425f-b876-cea949946cdc...
==> [info]: Connection setup successfully!
==> [info]: Loading environment variables... ✓
==> [info]: Loading KV... ✓
==> [info]: Building function "opa-demo"...
==> [info]: Compile policies [/Users/example/opa-demo/src/example.rego] to [/Users/example/opa-demo/output/opa-demo/bundle.tar.gz] .
==> [info]: unpacking bundle to [/Users/example/opa-demo/output/opa-demo/bundle] .
==> [info]: Uploading function 'opa-demo': /Users/example/opa-demo/output/opa-demo/index.js... ✓
```


cURL などのツールを使用してこのアドレスに HTTP リクエストを送信すると、関数のドメイン名トリガーが fetch イベントをトリガーします。この方法を使用して、関数が期待どおりに機能しているかどうかを確認できます。

<span id="デバッグ例"></span>
#### デバッグ例

OPA テンプレートが提供する OPA ポリシーを例にとります。OPA ポリシーでは GET リクエストのみが許可されているため、それぞれ POST リクエストと GET リクエストを送信して、ポリシーの有効性をテストできます。


1. 次のコマンドを実行して、関数に GET リクエストを送信します。


```shell
$ curl 127.0.0.1:18080 -v
*   Trying 127.0.0.1:18080...
* Connected to 127.0.0.1 (127.0.0.1) port 18080
> GET / HTTP/1.1
> Host: 127.0.0.1:18080
> User-Agent: curl/8.7.1
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Content-Type: text/plain;charset=UTF-8
< Date: Wed, 09 Jul 2025 07:11:07 GMT
< Server: Sparrow
< Transfer-Encoding: chunked
<
* Connection #0 to host 127.0.0.1 left intact
```


通常、`200 OK` レスポンスが返されます。これは、リクエストが OPA ポリシーに準拠しており、関数によって正常に処理されたことを示します。


2. 次のコマンドを実行して、関数に POST リクエストを送信します。


```shell
$ curl -X POST 127.0.0.1:18080 -v
*   Trying 127.0.0.1:18080...
* Connected to 127.0.0.1 (127.0.0.1) port 18080
> POST / HTTP/1.1
> Host: 127.0.0.1:18080
> User-Agent: curl/8.7.1
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 403 Forbidden
< Content-Type: text/plain;charset=UTF-8
< Date: Wed, 09 Jul 2025 07:17:16 GMT
< Server: Sparrow
< Transfer-Encoding: chunked
<
* Connection #0 to host 127.0.0.1 left intact
```


通常、`403 Forbidden` レスポンスが返されます。これは、リクエストが OPA ポリシーによって正常にインターセプトされたことを示します。

ローカルでのデバッグに合格したら、関数をエッジノードに公開できます。

<span id="ステップ-5-ローカル関数を公開する"></span>
### ステップ 5: ローカル関数を公開する

関数プロジェクトのルートディレクトリで次のコマンドを実行して、ローカル関数をグローバルエッジノードに公開します。関数をドメイン名に関連付ける前に、まず関数を完全に公開する必要があります。[nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-jp)を参照してください。

```shell
$ npx nest deploy --message "This is a new version"
```


コマンドラインで、新しい関数IDを作成するかどうかを尋ねられます。はいを選択してEnterキーを押します。エッジ関数CLIは、エッジ関数に対応するリモート関数を作成し、リモート関数をローカル関数と同期します。次に、エッジ関数CLIは、リモート関数をグローバルエッジノードに公開します。

関数が公開されたら、最後のステップは、関数が期待どおりに機能していることを確認することです。

<span id="ステップ-6-関数の検証"></span>
### ステップ 6: 関数の検証

関数が公開されたら、 **ステップ 4: プロジェクトのデバッグ** の方法を参照して、ドメイン名に HTTP リクエストを送信することで、関数が期待どおりに機能しているかどうかを確認できます。

<span id="opa-javascript-sdkリファレンス"></span>
## OPA JavaScript SDKリファレンス

OPA JavaScript SDKはOPA Wasm Javascript Moduleに基づいて開発されていますが、両者は完全に同じではありません。このセクションでは、OPA JavaScript SDKの `loadPolicy()` メソッド、`policy.eval()` メソッド、および `policy.setData()` メソッドの使用方法について説明します。

<span id="loadpolicy"></span>
### `loadPolicy()`

`loadPolicy()` メソッドは、OPA ポリシーを読み込み、ポリシーを評価するために使用できるインスタンスを返します。

**構文**

```javascript
loadPolicy(customBuiltins)
```


 **パラメーター** 


* `customBuiltins` *optional*

   カスタム関数のマッピングとして機能するオブジェクト。オブジェクトのキーは、Rego ポリシーで使用する関数名 (文字列) で、値は対応する JavaScript 関数です。エッジ関数は [バージョン 1.4.2の OPA 組み込み関数](https://v1-4-2--opa-docs.netlify.app/policy-reference/#built-in-functions)のみをサポートしており、これらの組み込み関数を Rego ポリシーで直接使用できます。エッジ関数でサポートされていない組み込み関数またはカスタム関数については、JavaScript で実装し、`customBuiltins` パラメーターに渡すことができます。


**戻り値**

ポリシー評価を実行するために使用できる `eval()` や `setData()` などのメソッドを含む、読み込まれたポリシーオブジェクトインスタンス。

**例**

<span id="カスタム関数の使用"></span>
#### カスタム関数の使用

Rego ポリシーでカスタム関数を使用する場合は、カスタム関数の実装を含むオブジェクトを `loadPolicy()` メソッドに渡すことができます。

たとえば、Rego ポリシーで `custom.path_check` という名前の関数を使用して、リクエストパスが `/test` で始まるかどうかを確認するとします。


1. Rego ポリシーファイル (例: `example.rego`) で、次のようにこのカスタム関数を呼び出すことができます。

   ```rego
   package example
   
   default allow := false
   
   allow if {
       input.method == "GET"
       custom.path_check(input.path)
   }
   ```
   

2. JavaScript エントリファイル (例: `index.js`) で、`loadPolicy()` メソッドで `custom.path_check` 関数の実装を提供する必要があります。

   ```javascript
   const { loadPolicy } = require("opa-wasm-sdk");
   
   addEventListener("fetch", (event) =>
     event.respondWith(handleRequest(event.request))
   );
   
   let policy = null;
   // Initialize a global opa policy
   policy = loadPolicy({
     "custom.path_check": (path) => {
       return path.startsWith("/test");
     },
   });
   
   function handleRequest(request) {
     if (policy == null) {
       return new Response("Policy not ready", {
         status: 503,
         statusText: "Service Unavailable",
       });
     }
   
     let url = new URL(request.url);
   
     let inputJson = {
       method: request.method,
       path: url.pathname,
     };
     console.log(inputJson);
   
     let r = policy.eval(inputJson);
     console.log(JSON.stringify(r));
   
     let allow = false;
     if (r.length === 1 && r[0]["result"] === true) {
       allow = true;
     }
   
     if (!allow) {
       return new Response("Forbidden", {
         status: 403,
         statusText: "Forbidden",
       });
     }
   
     return new Response("OK", { status: 200, statusText: "OK" });
   }
   ```
   

3. カスタム関数のシグネチャを宣言するために `capabilities.json` ファイルを作成する必要があります。これにより、OPAはカスタム関数を理解し、ポリシー評価に正しく統合できます。

   ```json
   {
     "builtins": [
       {
         "name": "custom.path_check",
         "decl": {
           "type": "function",
           "args": [
             { "type": "string" }
           ],
           "result": {
             "type": "boolean"
           }
         }
       }
     ]
   }
   ```
   

4. `nest.json` ファイルで、`attachment.capabilities_path` フィールドを介して `capabilities.json` ファイルのパスを指定する必要があります。これにより、エッジ関数CLIがOPA関数をビルドおよびデプロイするときに、この構成ファイルを見つけて使用できるようになります。

   ```json
   {
     "work_dir": "/Users/example/opa-demo",
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
       "access_key": "",
       "secret_key": ""
     },
     "functions": [
       {
         "id": "",
         "name": "opa-test",
         "type": "opa",
         "entry": "src/index.js",
         "attachment": {
           "rego_paths": [
             "src/example.rego"
           ],
           "entrypoints": [
             "example/allow"
           ],
           "capabilities_path": "capabilities.json"
         },
         "region": "outside_chinese_mainland"
       }
     ]
   }
   ```
   


<span id="policy-eval"></span>
### `policy.eval()`

`policy.eval()` メソッドは、指定された入力で読み込まれたポリシーを評価し、結果セットを返します。

**構文**

```javascript
policy.eval(input, entrypoint)
```


 **パラメーター** 


* `input` *required*

   ポリシー評価の入力パラメーター。`object`、プリミティブリテラル、または `ArrayBuffer` (整形式の文字列化された JSON であると想定)を指定できます。

* `entrypoint` *optional*

   呼び出すエントリポイントの ID または名前。指定しない場合は、デフォルトのエントリポイントが使用されます。


**戻り値**

評価の結果セットを表す配列。たとえば、`[{"result": <value of example/allow>}]`。

**例**

[ステップ 3: 関数コードを編集する](https://docs.byteplus.com/en/docs/18/57424#%E3%82%B9%E3%83%86%E3%83%83%E3%83%97-3-%E9%96%A2%E6%95%B0%E3%82%B3%E3%83%BC%E3%83%89%E3%82%92%E7%B7%A8%E9%9B%86%E3%81%99%E3%82%8B)の例を参照してください。

<span id="policy-setdata"></span>
### `policy.setData()`

`policy.setData()` メソッドは、ポリシーで使用されるデータを設定します。

**構文**

```javascript
policy.setData(data)
```


 **パラメーター** 


* `data` *required*

   ポリシーで使用されるデータ。`object`、プリミティブリテラル、または `ArrayBuffer` (整形式の文字列化された JSON であると想定)を指定できます。


**戻り値**

なし。

**例**

ユーザーが許可されたユーザーのリストに含まれているかどうかを確認するポリシーがあるとします。`policy.setData()`を使用して、許可されたユーザーのリストを設定できます。


1. Rego ポリシーファイル (例: `example.rego`) で、`data` キーワードを使用してデータにアクセスできます。

   ```rego
   package example
   
   default allow := false
   
   allow if {
       input.user in data.allowed_users
   }
   ```
   

2. JavaScript エントリファイル (例: `index.js`) で、`policy.setData()`を使用して `allowed_users` データを設定できます。

   ```javascript
   const { loadPolicy } = require("opa-wasm-sdk");
   
   addEventListener("fetch", (event) =>
     event.respondWith(handleRequest(event.request))
   );
   
   let policy = null;
   // Initialize a global opa policy
   policy = loadPolicy();
   
   // Set the data for the policy
   policy.setData({
       "allowed_users": ["alice", "bob"]
   });
   
   function handleRequest(request) {
     if (policy == null) {
       return new Response("Policy not ready", {
         status: 503,
         statusText: "Service Unavailable",
       });
     }
   
     let inputJson = {
       user: request.headers.get("user"),
     };
     console.log(inputJson);
   
     let r = policy.eval(inputJson);
     console.log(JSON.stringify(r));
   
     let allow = false;
     if (r.length === 1 && r[0]["result"] === true) {
       allow = true;
     }
   
     if (!allow) {
       return new Response("Forbidden", {
         status: 403,
         statusText: "Forbidden",
       });
     }
   
     return new Response("OK", { status: 200, statusText: "OK" });
   }
   ```
   


<span id="rego-言語バージョンの互換性に関する説明"></span>
## Rego 言語バージョンの互換性に関する説明

エッジ関数CLIは、RegoコードがOPA v1標準に準拠していることをデフォルトとします。Rego コードが OPA v0の機能を使用している場合は、`nest.json` ファイルの `attachment.rego_version` フィールドを介して必要な互換性バージョンを明示的に指定する必要があります。

たとえば、Rego コードが OPA v0の機能である `opa.runtime()` 組み込み関数を使用している場合は、`attachment.rego_version`を `v0` に設定する必要があります。

```json
  "functions": [
    {
      "id": "",
      "name": "opa-demo",
      "type": "opa",
      "entry": "src/index.js",
      "attachment": {
        "rego_paths": [
          "src/opa-demo.rego"
        ],
        "entrypoints": [
          "example/allow"
        ],
        "rego_version": "v0"
      },
      "region": "outside_chinese_mainland"
    }
  ]
```
