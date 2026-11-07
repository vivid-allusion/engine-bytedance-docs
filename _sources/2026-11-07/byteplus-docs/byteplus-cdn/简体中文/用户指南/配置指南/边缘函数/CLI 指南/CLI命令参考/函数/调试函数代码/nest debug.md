---
title: "nest debug"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-cn"
---

使用边缘函数 Debugger 命令行调试函数代码。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">您无需设置 Access Key ID 和 Secret Access Key 就可以运行本命令。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>



<span id="概要"></span>
## 概要

```shell
npx nest debug --function <function_id_or_name>
```


<span id="描述"></span>
## 描述


* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。


边缘函数的 Debugger 启动成功后，您会进入 Debugger 命令行。您可以在 Debugger 命令行中输入 Debug 命令进行调试。您也可以使用 vi、cat 和 ls 三个命令在 Debugger 命令行中查看文件。

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


如果在一段时间内您没有操作 Debugger 命令行，边缘函数 CLI 会与边缘函数 Debugger 断开连接。如果您需要继续使用 Debugger 命令行，您需要重新运行 `nest debug` 命令。

<span id="debug-命令"></span>
## Debug 命令

<span id="source"></span>
### source

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">如果您的本地代码被更新，您需要运行 <code>source</code> 命令才能把新的代码上传到边缘函数 Debugger。</div>


```shell
source <path_to_entry_file>
```


构建函数代码并把代码上传到边缘函数 Debugger。`source` 的别名为 `s`。


* `<path_to_entry_file>`：*string，optional*

   * 入口文件的路径。入口文件是本地函数执行的起点。默认为项目配置文件中的 `entry` 字段指定的入口文件。


运行 source 命令的响应示例如下：

```shell
nest: source
==> [info]: building script "default"... 
==> Uploading scripts: [default]... 
```


<span id="query"></span>
### query

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">在运行此命令前，您需要首先运行 <code>source</code> 命令构建函数代码并把代码上传到边缘函数 Debugger。Debugger 命令行每次重新启动时，您都需要先运行 <code>source</code> 命令再运行 <code>query</code> 命令。</div>


```shell
query

query -X <http_method> <url>
```


向边缘函数 Debugger 发送 HTTP 请求，通过域名触发器触发您向边缘函数 Debugger 上传的函数代码中的 fetch 事件。`query` 的别名为 `q`。


* `<http_method>`：*string，optional*

   * HTTP 方法。默认为 POST。

* `<url>`：*string，optional*

   * 请求 URL。默认为 http://example.com。


运行 query 命令的响应示例如下：

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


为边缘函数 Debugger 启动一个本地 HTTP 代理。这样您就可以通过 cURL 等方式向本地 HTTP 代理发送 HTTP 请求，触发函数执行。您也可以在特定端口上启动本地 HTTP 代理，例如 `server 8086`。


* `<port>`：*string，optional*

   * 本地 HTTP 代理的端口。默认为 60081。


<span id="env"></span>
### env

```shell
env <key> <value>

env <key1> <value1> <key2> <value2>
```


添加或更新一个或多个环境变量。


* `<key>`：*string，required*

   * 环境变量的键。

* `<value>`：*string，required*

   * 环境变量的值。


<span id="setkv"></span>
### setkv

```shell
setkv <namespace> <key> <value>

setkv <namespace1> <key1> <value1> <namespace2> <key2> <value2>
```


在边缘 KV 中添加或更新一个或多个键值对。`setkv` 的别名是 `kv`。


* `<namespace>`：*string，required*

   * 命名空间。

* `<key>`：*string，required*

   * 键值对的键。

* `<value>`：*string，required*

   * 键值对的值。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">使用 <code>setkv</code> 添加或更新键值对时，键值对的值会被 base64 编码后存入边缘 KV。因此，从边缘 KV 获取的值需要先通过 <code>atob()</code> 进行解码。</div>


<div data-tips="true" data-tips-type="warning">例如，您通过边缘函数 CLI 运行 <code>setkv ns myKey "This is my value"</code> 添加了一个键值对。如果您需要在函数代码中获取该键值对的值，您需要先调用 <code>atob()</code> 对值进行解码。</div>


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


开启或关闭 CPU Profiler。CPU Profiler 用于统计函数代码执行的性能指标。


* 开启后，函数代码后续的每次执行都会被统计。

* 关闭后，CPU Profiler 会停止统计。统计结果会被打印到 Debugger 命令行。


`cpuProfiler` 的别名是 `cpu`。

例如，您可以先开启 CPU Profiler，然后触发函数代码执行，最后关闭 CPU Profiler 并查看统计结果。

```shell
cpuProfiler

query

cpuProfiler
```


运行 cpuProfiler 的示例如下：

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


开启或关闭 Insight。Insight 展示了函数代码最近一次执行的相关信息。


* 运行 `insight true` 开启 Insight，函数代码后续的每次执行都会被 Insight 统计。函数代码执行完成后，统计结果会被打印到命令行。

* 运行 `insight false` 关闭 Insight，函数代码后续的执行不会再被统计。


`insight` 的别名是 `ins`。

例如，您可以先开启 Insight，然后触发函数代码执行，最后关闭 Insight 并查看统计结果。

```shell
insight true

query

insight false
```


运行 insight 的示例如下：

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


获取帮助信息。
