---
title: "nest debug"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-en"
---

Debugs function code with the Edge Functions Debugger command line.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You don't need to set up an access key ID and secret access key to run this command.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>



<span id="synopsis"></span>
## Synopsis

```shell
npx nest debug --function <function_id_or_name>
```


<span id="description"></span>
## Description


* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). By default, it's the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list).


After the Edge Functions Debugger starts successfully, you'll enter the Debugger command line. You can input Debug commands in the Debugger command line for debugging. You can also use the vi, cat, and ls commands in the Debugger command line to view files.

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


If you don't operate the Debugger command line for a period of time, the Edge Functions CLI will disconnect from the Edge Functions Debugger. If you need to continue using the Debugger command line, you need to run the `nest debug` command again.

<span id="debug-commands"></span>
## Debug commands

<span id="source"></span>
### source

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If your local code is updated, you need to run the <code>source</code> command to upload the new code to the Edge Functions Debugger.</div>


```shell
source <path_to_entry_file>
```


Build the function code and upload it to the Edge Functions Debugger. The alias for `source` is `s`.


* `<path_to_entry_file>`: *string, optional*

   * Path to the entry file. The entry file is the starting point for executing the local function. By default, it's the entry file specified in the `entry` field of the project configuration file.


An example response when running the source command:

```shell
nest: source
==> [info]: building script "default"... 
==> Uploading scripts: [default]... 
```


<span id="query"></span>
### query

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before running this command, you need to first run the <code>source</code> command to build the function code and upload it to the Edge Functions Debugger. Every time the Debugger command line restarts, you need to run the <code>source</code> command before running the <code>query</code> command.</div>


```shell
query

query -X <http_method> <url>
```


Send an HTTP request to the Edge Functions Debugger, triggering the fetch event in the function code you uploaded to the Edge Functions Debugger through the domain trigger. The alias for `query` is `q`.


* `<http_method>`: *string, optional*

   * HTTP method. Default is POST.

* `<url>`: *string, optional*

   * Request URL. Default is http://example.com.


An example response when running the query command:

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


Start a local HTTP proxy for the Edge Functions Debugger. This allows you to send HTTP requests to the local HTTP proxy using methods like cURL, triggering function execution. You can also start the local HTTP proxy on a specific port, for example, `server 8086`.


* `<port>`: *string, optional*

   * Port for the local HTTP proxy. Default is 60081.


<span id="env"></span>
### env

```shell
env <key> <value>

env <key1> <value1> <key2> <value2>
```


Add or update one or more environment variables.


* `<key>`: *string, required*

   * Key of the environment variable.

* `<value>`: *string, required*

   * Value of the environment variable.


<span id="setkv"></span>
### setkv

```shell
setkv <namespace> <key> <value>

setkv <namespace1> <key1> <value1> <namespace2> <key2> <value2>
```


Add or update one or more key\-value pairs in Edge KV. The alias for `setkv` is `kv`.


* `<namespace>`: *string, required*

   * Namespace.

* `<key>`: *string, required*

   * Key of the key\-value pair.

* `<value>`: *string, required*

   * Value of the key\-value pair.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using <code>setkv</code> to add or update key\-value pairs, the value of the key\-value pair is base64 encoded before being stored in Edge KV. Therefore, values retrieved from Edge KV need to be decoded using <code>atob()</code> first.</div>


<div data-tips="true" data-tips-type="warning">For example, if you add a key\-value pair by running <code>setkv ns myKey "This is my value"</code> through the Edge Functions CLI. If you need to get the value of this key\-value pair in your function code, you need to decode the value using <code>atob()</code> first.</div>


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


Turn on or off the CPU Profiler. The CPU Profiler is used to collect performance metrics of function code execution.


* When turned on, every subsequent execution of the function code will be profiled.

* When turned off, the CPU Profiler will stop profiling. The profiling results will be printed to the Debugger command line.


The alias for `cpuProfiler` is `cpu`.

For example, you can first turn on the CPU Profiler, then trigger the function code execution, and finally turn off the CPU Profiler to view the profiling results.

```shell
cpuProfiler

query

cpuProfiler
```


An example of running cpuProfiler:

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


Turn on or off Insight. Insight shows information related to the most recent execution of the function code.


* Running `insight true` turns on Insight, and every subsequent execution of the function code will be profiled by Insight. After the function code execution is complete, the profiling results will be printed to the command line.

* Running `insight false` turns off Insight, and subsequent executions of the function code will not be profiled.


The alias for `insight` is `ins`.

For example, you can first turn on Insight, then trigger the function code execution, and finally turn off Insight to view the profiling results.

```shell
insight true

query

insight false
```


An example of running insight:

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


Get help information.
