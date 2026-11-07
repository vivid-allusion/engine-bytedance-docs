---
title: "nest debug"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-jp"
---

エッジ関数 Debuggerコマンドラインを使用して関数コードをデバッグします。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを実行するためにAccess Key IDとSecret Access Keyを設定する必要はありません。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>



<span id="概要"></span>
## 概要

```shell
npx nest debug --function <function_id_or_name>
```


<span id="説明"></span>
## 説明


* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。


エッジ関数Debuggerが正常に起動すると、Debuggerコマンドラインに入ります。Debuggerコマンドラインでデバッグコマンドを入力してデバッグを行うことができます。また、Debuggerコマンドラインでvi、cat、lsコマンドを使用してファイルを表示することもできます。

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
==> [info]: loading envrionment variables... ✔
nest: 
```


Debuggerコマンドラインを一定時間操作しないと、エッジ関数 CLIはエッジ関数 Debuggerとの接続を切断します。Debuggerコマンドラインを引き続き使用する必要がある場合は、`nest debug`コマンドを再度実行する必要があります。

<span id="デバッグコマンド"></span>
## デバッグコマンド

<span id="source"></span>
### source

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">ローカルコードが更新された場合、<code>source</code>コマンドを実行して新しいコードをエッジ関数 Debuggerにアップロードする必要があります。</div>


```shell
source <path_to_entry_file>
```


関数コードをビルドし、エッジ関数 Debuggerにアップロードします。`source`のエイリアスは`s`です。


* `<path_to_entry_file>`: *string, optional*

   * エントリーファイルへのパス。エントリーファイルはローカル関数の実行開始点です。デフォルトはプロジェクト設定ファイルの`entry`フィールドで指定されたエントリーファイルです。


sourceコマンドを実行した際のレスポンス例：

```shell
nest: source
==> [info]: building script "default"... 
==> Uploading scripts: [default]... 
```


<span id="query"></span>
### query

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">このコマンドを実行する前に、まず<code>source</code>コマンドを実行して関数コードをビルドし、エッジ関数 Debuggerにアップロードする必要があります。Debuggerコマンドラインを再起動するたびに、<code>query</code>コマンドを実行する前に<code>source</code>コマンドを実行する必要があります。</div>


```shell
query

query -X <http_method> <url>
```


エッジ関数 DebuggerにHTTPリクエストを送信し、ドメイントリガーを通じてエッジ関数 Debuggerにアップロードした関数コードのfetchイベントをトリガーします。`query`のエイリアスは`q`です。


* `<http_method>`: *string, optional*

   * HTTPメソッド。デフォルトはPOSTです。

* `<url>`: *string, optional*

   * リクエストURL。デフォルトはhttp://example.comです。


queryコマンドを実行した際のレスポンス例：

```shell
nest: query
==> HttpResponse ✔
status: 200

statusText: OK

header:
  content-type => text/plain;charset=UTF-8
  date => Mon, 06 Jan 2025 07:35:38 GMT
  server => Sparrow
  transfer-encoding => chunked

body:
Hello World!
```


<span id="server"></span>
### server

```shell
server <port>
```


エッジ関数Debugger用のローカルHTTPプロキシを起動します。これにより、cURLなどの方法を使用してローカルHTTPプロキシにHTTPリクエストを送信し、関数の実行をトリガーすることができます。特定のポートでローカルHTTPプロキシを起動することもできます。例：`server 8086`。


* `<port>`: *string, optional*

   * ローカルHTTPプロキシのポート。デフォルトは60081です。


<span id="env"></span>
### env

```shell
env <key> <value>

env <key1> <value1> <key2> <value2>
```


1つまたは複数の環境変数を追加または更新します。


* `<key>`: *string, required*

   * 環境変数のキー。

* `<value>`: *string, required*

   * 環境変数の値。


<span id="setkv"></span>
### setkv

```shell
setkv <namespace> <key> <value>

setkv <namespace1> <key1> <value1> <namespace2> <key2> <value2>
```


エッジKVに1つまたは複数のキーバリューペアを追加または更新します。`setkv`のエイリアスは`kv`です。


* `<namespace>`: *string, required*

   * 名前空間。

* `<key>`: *string, required*

   * キーバリューペアのキー。

* `<value>`: *string, required*

   * キーバリューペアの値。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>setkv</code>を使用してキーバリューペアを追加または更新する場合、キーバリューペアの値はbase64エンコードされてからエッジKVに保存されます。したがって、エッジKVから取得した値は、まず<code>atob()</code>を使用してデコードする必要があります。</div>


<div data-tips="true" data-tips-type="warning">例えば、エッジ関数CLIを通じて<code>setkv ns myKey "This is my value"</code>を実行してキーバリューペアを追加した場合、関数コードでこのキーバリューペアの値を取得する必要がある場合は、まず<code>atob()</code>を使用して値をデコードする必要があります。</div>


<div data-tips="true" data-tips-type="warning">```javascript
const value = await KV.get("ns", "myKey", {type: "string"});
return new Response(`${atob(value)}`, { status: 200 });
```
</div>


<span id="cpuprofiler"></span>
### cpuProfiler

```shell
cpuProfiler
```


CPU Profilerをオンまたはオフにします。CPU Profilerは関数コード実行のパフォーマンスメトリクスを収集するために使用されます。


* オンにすると、その後の関数コードの実行ごとにプロファイリングが行われます。

* オフにすると、CPU Profilerはプロファイリングを停止します。プロファイリング結果はDebuggerコマンドラインに出力されます。


`cpuProfiler`のエイリアスは`cpu`です。

例えば、まずCPU Profilerをオンにし、次に関数コードの実行をトリガーし、最後にCPU Profilerをオフにしてプロファイリング結果を表示することができます。

```shell
cpuProfiler

query

cpuProfiler
```


cpuProfilerを実行した例：

```shell
nest: cpuProfiler
==> cpuProfiler ✔
cpu profiler start


nest: query
==> HttpResponse ✔
status: 200

statusText: OK

header:
  content-type => text/plain;charset=UTF-8
  date => Mon, 06 Jan 2025 08:11:22 GMT
  server => Sparrow
  transfer-encoding => chunked

body:
Hello World!


nest: cpuProfiler
==> cpuProfilerResult ✔
+---------------+----------+------+--------+----------------+-----------+
|   FUNCTION    | HITCOUNT | LINE | COLUMN |     SCRIPT     |   CODE    |
+---------------+----------+------+--------+----------------+-----------+
| (program)     | 33.3%    |    0 |      0 |                | (runtime) |
| handleRequest | 33.3%    |    4 |     31 | script-default | N/A       |
+---------------+----------+------+--------+----------------+-----------+



==> cpuProfiler ✔
cpu profiler stop
```


<span id="insight"></span>
### insight

```shell
insight true

insight false
```


Insightをオンまたはオフにします。Insightは関数コードの最新の実行に関連する情報を表示します。


* `insight true`を実行するとInsightがオンになり、その後の関数コードの実行ごとにInsightによってプロファイリングが行われます。関数コードの実行が完了すると、プロファイリング結果がコマンドラインに出力されます。

* `insight false`を実行するとInsightがオフになり、その後の関数コードの実行はプロファイリングされません。


`insight`のエイリアスは`ins`です。

例えば、まずInsightをオンにし、次に関数コードの実行をトリガーし、最後にInsightをオフにしてプロファイリング結果を表示することができます。

```shell
insight true

query

insight false
```


insightを実行した例：

```shell
nest: insight true
==> enableInsight ✔
successfully


nest: query
==> HttpResponse ✔
status: 200

statusText: OK

header:
  content-type => text/plain;charset=UTF-8
  date => Mon, 06 Jan 2025 08:14:21 GMT
  server => Sparrow
  transfer-encoding => chunked

body:
Hello World!


==> Insight ✔
+----------------------------+---------------+
|          METRICS           |     VALUE     |
+----------------------------+---------------+
| ExecuteTime                | 0             |
| TcpSSLBandwidthOut         | 0             |
| Event                      | fetch         |
| InMethod                   | GET           |
| QueueTime                  | 0             |
| TcpSSLBandwidthIn          | 0             |
| FetchRedirectLocationError | 0             |
| FetchHttpsAttempt          | 0             |
| FetchUnknown               | 0             |
| SetupTime                  | 0             |
| FetchHttpAttempt           | 0             |
| FetchError                 | 0             |
| JoinTime                   | 0             |
| FetchAttempt               | 0             |
| InAuthority                | example.com   |
| SourceTime                 | 0             |
| WaitPromiseNumber          | 0             |
| Fetch5xx                   | 0             |
| CreateTs                   | 1736151261435 |
| Fetch4xx                   | 0             |
| RealTime                   | 3             |
| CpuTime                    | 266           |
| FetchRedirectRequest       | 0             |
| Fetch3xx                   | 0             |
| GcTime                     | 0             |
| OutStatus                  | 200           |
| ResponseTime               | 0             |
| TcpBandwidthIn             | 0             |
| TcpBandwidthOut            | 0             |
| Fetch2xx                   | 0             |
+----------------------------+---------------+

nest: insight false
==> disableInsight ✔
successfully
```


<span id="help"></span>
### help

```shell
help
```


ヘルプ情報を取得します。
