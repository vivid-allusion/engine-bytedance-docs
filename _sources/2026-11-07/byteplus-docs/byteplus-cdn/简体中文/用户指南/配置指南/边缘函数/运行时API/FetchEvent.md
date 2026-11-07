---
title: "FetchEvent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn"
---

fetch 类型的事件，由域名触发器触发。

参见 MDN 文档中的 [FetchEvent](https://developer.mozilla.org/zh-CN/docs/Web/API/FetchEvent)。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">边缘函数运行时不允许您使用 <code>FetchEvent()</code> 构造函数构造 <code>FetchEvent</code> 对象。您必须通过调用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn">addEventListener()</a> 注册监听器监听 fetch 事件来获取 <code>FetchEvent</code> 对象。</div>


<span id="方法"></span>
## 方法

<span id="respondwith"></span>
### respondWith()

在 fetch 事件被触发时，边缘函数会拦截用户请求，并将您向该方法传入的 [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn) 对象或一个 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象作为响应。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">如果您不调用 <code>respondWith()</code> 方法，边缘函数会在 fetch 事件被触发时把用户请求转发到 BytePlus CDN。</div>


<span id="示例"></span>
#### 示例

```js
//边缘函数会把用户请求转发到 BytePlus CDN。
addEventListener(
    'fetch', (event) => {
      console.log("callback1 has been triggered");
    });

// 边缘函数会拦截用户请求，并允许您向该方法的参数传入一个 Response 对象作为响应。
addEventListener(
    'fetch', (event) => {
      console.log("callback2 has been triggered");
      event.respondWith(new Response("callback2 has been triggered"));  
    });
```


<span id="waituntil"></span>
### waitUntil()

通知边缘函数运行时等待在回调函数中注册的所有 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象被 resolve 或 reject。`waitUntil()` 方法可以被调用多次。您也可以把 `waitUntil()` 方法嵌套到 `waitUntil()` 方法里。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">如果函数的执行时间超过<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/functions-usage-limits">响应时间限制</a>，边缘函数运行时将销毁请求上下文，不再等待状态为 pending 的 <code>Promise</code> 对象。</div>


* <div data-tips="true" data-tips-type="warning">如果任一 <code>waitUntil()</code> 注册的 <code>Promise</code> 对象被 reject，边缘函数运行时将销毁请求上下文。建议为每个 <code>Promise</code> 添加错误处理，例如使用 <code>.catch()</code> 方法或 <code>try-catch</code> 语句。</div>



如果您未调用 `waitUntil()` 方法且未使用 `await`，当回调函数通过 `respondWith()` 返回响应后，边缘函数运行时将销毁请求上下文，不再等待状态为 pending 的 `Promise` 对象。`await` 虽然可以等待 `Promise` 被 resolve 或 reject，但会暂停回调函数的执行。相比之下，`waitUntil()` 方法允许在等待 `Promise` 被 resolve 或 reject 的同时，让回调函数继续执行其他操作。

<span id="示例"></span>
#### 示例

```JavaScript
// 定义上传日志的URL
const uploadURL = "https://log-collection.example.com/";

// 异步函数，用于上传回复的耗时
async function uploadLog(waiter) {
    const start = Date.now();
    // 等待waiter promise结束，这表示请求的回复已经发送完成
    await waiter;
    // 记录结束时间，注意，边缘函数的时钟对齐到 10 ms 左右，这是为了规避side-channel attack
    const end = Date.now();
    const cost = (end - start);
    // 将对象序列化为JSON字符串作为请求体
    const body = JSON.stringify({ cost: cost });
    await fetch(uploadURL, {
        method: "POST",
        body: body,
        headers: {
            'Content-Type': 'application/json'
        }
    });
}

// 监听fetch事件，并在事件发生时，调用handle函数处理
addEventListener('fetch', (event) => {
    event.respondWith(handle(event));
});

// 处理事件的函数
async function handle(event) {
    const response = new Response("Hello World");
    // response.body是一个readableStream，边缘函数运行时 API 包括waitClose方法
    // waitClose() 返回一个promise，当stream被终止的时候（可能是因为出错或者读取完成），waitClose() 会被resolve
    // 注意：如果您的Response是用于返回不含Body的响应，例如对 HTTP HEAD 请求的响应、304响应、204响应，则waitClose() 无效
    event.waitUntil(uploadLog(response.body.waitClose()));
    return response;
}

```


<span id="属性"></span>
## 属性

<span id="info"></span>
### info

获取客户端信息。


* `info.clientIp`：客户端的 IP 地址。如果客户端配置了代理，则该属性返回的是代理服务器的 IP 地址。

* `info.geo`：客户端 IP 的地理信息。geo 有以下属性：

   * `geo.country`：返回该 IP 地址所属国家的名称，例如 `China` 或 `United States`。

   * `geo.countryCode`：返回该 IP 地址所属国家的两位字母代码，符合 ISO 3166\-1 alpha\-2 标准。例如 `CN` 或 `US`。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">您只能通过 <code>province</code> 字段标识中国香港（Hong Kong）、中国澳门（Macao）和中国台湾（Taiwan）。中国香港、中国澳门和中国台湾的 <code>countryCode</code> 都是 <code>CN</code>。   </div>
   

   * `geo.region`：返回该 IP 地址所属中国地理大区的名称。例如 `EastChina`。如果该 IP 地址不属于中国内地，该参数返回 `XX`。

   * `geo.province`：返回该 IP 地址所属一级行政区的名称。例如 `Hebei` 或 `New Jersey`。

   * `geo.city`：返回该 IP 地址所属城市的名称。例如 `Shijiazhuang` 或 `Tampere`。

   * `geo.isp`：返回该 IP 地址所属 ISP 的名称。例如 `ChinaUnicom` 或 `DigitalOcean`。


<span id="示例"></span>
#### 示例

```JavaScript
addEventListener(
    'fetch', (event) => { event.respondWith(handle(event)); });
    
async function handle(event) {
  const info = event.info;
  console.log(info);  // 获得客户端的所有信息

  const clientIp = event.info.clientIp;
  console.log(clientIp); // 获得客户端的 IP 地址

  const country = event.info.geo.country;
  console.log(country); // 获得客户端 IP 地址所属的国家名称

  return new Response("done");
}
```


<span id="file"></span>
### File

参见 MDN 文档 [File](https://developer.mozilla.org/zh-CN/docs/Web/API/File)。

<span id="blob"></span>
### Blob

参见 MDN 文档 [Blob](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)。

<span id="formdata"></span>
### FormData

参见 MDN 文档 [FormData](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData)。
