---
title: "addEventListener()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn"
---

注册一个事件监听器。参见 MDN 文档 [addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)。

边缘函数支持以下事件类型：


* fetch：域名触发器触发的事件类型。参见 [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)。

* cron：Cron 触发器触发的事件类型。参见 [CronEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-CronEvent-cn)。


你可以在同一个代码文件中同时注册 cron 事件和 fetch 事件，这两种事件对应的回调函数是互不干扰的。您最多可以为每个事件注册 16 个回调函数。

您可以多次调用 `addEventListener()` 注册多个关于同一个或者不同事件的监听器。您在每个监听器中注册一个回调函数。


* 对于 fetch 事件，多个回调函数将按照注册顺序执行。如果一个回调函数已经调用 [respondWith()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn#respondwith) 返回了结果，那么后续已注册但没有被调用的回调函数就不会被执行。如果所有的回调函数在响应时间限制内均未返回结果，运行时将会抛出错误。

* 对于 cron 事件，仅第一个回调函数会被执行。如果第一个回调函数在响应时间限制内未返回结果，运行时将会抛出错误。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/functions-usage-limits">使用限制</a> 了解边缘函数的响应时间限制。</div>


<span id="示例"></span>
## 示例

<span id="监听-fetch-事件"></span>
### 监听 fetch 事件

以下代码描述了如何监听 fetch 事件。

```JavaScript
addEventListener(
    'fetch', (event) => {
      // 回调函数1 打印"callback1 has been triggered"
      console.log("callback1 has been triggered");
    });

addEventListener(
    'fetch', (event) => {
      // 回调函数2 打印"callback2 has been triggered"
      console.log("callback2 has been triggered");
      event.respondWith(new Response("callback2 has been triggered"));  // 这个调用表示该回调函数正确处理了返回，后续的回调函数不被调用
    });

addEventListener('fetch', (event) => {
    // 回调函数3 根据代码的结构，该回调函数永远不会被执行，因为在前面的代码中，事件的响应操作已经被处理了。
    console.log("这个永远不会被显示");
});
```


<span id="监听-cron-事件"></span>
### 监听 cron 事件

以下代码描述了如何监听 cron 事件。

```javascript
addEventListener('cron', onCron);

async function onCron(event) {

  // 1. 您可以通过OpenAPI/或控制台为每个Cron触发器添加一个 payload。
  //    该数据不会影响程序的正常运行。你可以通过使用event对象的如下API来获取这个数据。
  const text = await event.text();

  // 2. 获取Cron触发器的相关属性
  const job = event.job; // Cron触发器的名称
  const cronExpression = event.cronExpression; // Cron触发器的时间规则
  console.log("cron triggered");
}
```
