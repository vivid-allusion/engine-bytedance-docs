---
title: "nest debug"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-cn-zh-tw"
---

使用邊緣函數 Debugger 命令列偵錯函數程式碼。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">您無需設定 Access Key ID 和 Secret Access Key 就可以執行本指令</div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案</div>



<span id="概要"></span>
## 概要

```shell
npx nest debug --function <function_id_or_name>
```


<span id="描述"></span>
## 描述


* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數


邊緣函數的 Debugger 啟動成功後，您會進入 Debugger 命令列。您可以在 Debugger 命令列中輸入 Debug 指令進行偵錯。您也可以使用 vi、cat 和 ls 三個指令在 Debugger 命令列中查看檔案

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


如果在一段時間內您沒有操作 Debugger 命令列，邊緣函數 CLI 會與邊緣函數 Debugger 斷開連線。如果您需要繼續使用 Debugger 命令列，您需要重新執行 `nest debug` 指令

<span id="debug-指令"></span>
## Debug 指令

<span id="source"></span>
### source

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">如果您的本地程式碼被更新，您需要執行 <code>source</code> 指令才能把新的程式碼上傳到邊緣函數 Debugger</div>


```shell
source <path_to_entry_file>
```


建構函數程式碼並把程式碼上傳到邊緣函數 Debugger。`source` 的別名為 `s`


* `<path_to_entry_file>`：*string，optional*

   * 入口檔案的路徑。入口檔案是本地函數執行的起點。預設為專案設定檔中的 `entry` 欄位指定的入口檔案


執行 source 指令的回應範例如下：

```shell
nest: source
==> [info]: building script "default"... 
==> Uploading scripts: [default]... 
```


<span id="query"></span>
### query

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">在執行此指令前，您需要首先執行 <code>source</code> 指令建構函數程式碼並把程式碼上傳到邊緣函數 Debugger。Debugger 命令列每次重新啟動時，您都需要先執行 <code>source</code> 指令再執行 <code>query</code> 指令</div>


```shell
query

query -X <http_method> <url>
```


向邊緣函數 Debugger 發送 HTTP 請求，透過網域名稱觸發器觸發您向邊緣函數 Debugger 上傳的函數程式碼中的 fetch 事件。`query` 的別名為 `q`


* `<http_method>`：*string，optional*

   * HTTP 方法。預設為 POST

* `<url>`：*string，optional*

   * 請求 URL。預設為 http://example.com


執行 query 指令的回應範例如下：

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


為邊緣函數 Debugger 啟動一個本地 HTTP 代理。這樣您就可以透過 cURL 等方式向本地 HTTP 代理發送 HTTP 請求，觸發函數執行。您也可以在特定連接埠上啟動本地 HTTP 代理，例如 `server 8086`


* `<port>`：*string，optional*

   * 本地 HTTP 代理的連接埠。預設為 60081


<span id="env"></span>
### env

```shell
env <key> <value>

env <key1> <value1> <key2> <value2>
```


新增或更新一個或多個環境變數


* `<key>`：*string，required*

   * 環境變數的鍵

* `<value>`：*string，required*

   * 環境變數的值


<span id="setkv"></span>
### setkv

```shell
setkv <namespace> <key> <value>

setkv <namespace1> <key1> <value1> <namespace2> <key2> <value2>
```


在邊緣 KV 中新增或更新一個或多個鍵值對。`setkv` 的別名是 `kv`


* `<namespace>`：*string，required*

   * 命名空間

* `<key>`：*string，required*

   * 鍵值對的鍵

* `<value>`：*string，required*

   * 鍵值對的值


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">使用 <code>setkv</code> 新增或更新鍵值對時，鍵值對的值會被 base64 編碼後存入邊緣 KV。因此，從邊緣 KV 取得的值需要先透過 <code>atob()</code> 進行解碼</div>


<div data-tips="true" data-tips-type="warning">例如，您透過邊緣函數 CLI 執行 <code>setkv ns myKey "This is my value"</code> 新增了一個鍵值對。如果您需要在函數程式碼中取得該鍵值對的值，您需要先呼叫 <code>atob()</code> 對值進行解碼</div>


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


開啟或關閉 CPU Profiler。CPU Profiler 用於統計函數程式碼執行的效能指標：


* 開啟後，函數程式碼後續的每次執行都會被統計

* 關閉後，CPU Profiler 會停止統計。統計結果會被列印到 Debugger 命令列


`cpuProfiler` 的別名是 `cpu`

例如，您可以先開啟 CPU Profiler，然後觸發函數程式碼執行，最後關閉 CPU Profiler 並查看統計結果

```shell
cpuProfiler

query

cpuProfiler
```


執行 cpuProfiler 的範例如下：

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


開啟或關閉 Insight。Insight 展示了函數程式碼最近一次執行的相關資訊：


* 執行 `insight true` 開啟 Insight，函數程式碼後續的每次執行都會被 Insight 統計。函數程式碼執行完成後，統計結果會被列印到命令列

* 執行 `insight false` 關閉 Insight，函數程式碼後續的執行不會再被統計


`insight` 的別名是 `ins`

例如，您可以先開啟 Insight，然後觸發函數程式碼執行，最後關閉 Insight 並查看統計結果

```shell
insight true

query

insight false
```


執行 insight 的範例如下：

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


取得說明資訊
