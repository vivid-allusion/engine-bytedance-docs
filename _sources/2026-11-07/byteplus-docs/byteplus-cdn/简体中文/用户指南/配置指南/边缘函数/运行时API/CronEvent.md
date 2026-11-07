---
title: "CronEvent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-CronEvent-cn"
---

cron 类型的事件，由 Cron 触发器触发。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">您必须通过调用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn">addEventListener()</a> 注册监听器监听 cron 事件来获取 <code>CronEvent</code> 对象。</div>


<span id="方法"></span>
## 方法

<span id="text"></span>
### text()

该方法返回一个 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象，当该 `Promise` 对象被 resolve 之后，返回的值是您在 Cron 触发器中配置的自定义参数，类型为 [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)。参见 [Cron 触发器](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn) 了解如何在 Cron 触发器中配置自定义参数。

<span id="arraybuffer"></span>
### arrayBuffer()

该方法返回一个 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象，当 该 `Promise` 对象被 resolve 之后，返回的值是您在 Cron 触发器中配置的自定义参数，类型为 [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)。参见 [Cron 触发器](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn) 了解如何在 Cron 触发器中配置自定义参数。

<span id="stream"></span>
### stream()

该方法返回一个 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象，当该 `Promise` 对象被 resolve 之后，返回的值是您在 Cron 触发器中配置的自定义参数，类型为 [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)。参见 [Cron 触发器](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn) 了解如何在 Cron 触发器中配置自定义参数。

<span id="json"></span>
### json()

该方法返回一个 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象，当该 `Promise` 对象被 resolve 之后，返回的值是您在 Cron 触发器中配置的自定义参数，类型为 [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)。参见 [Cron 触发器](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn) 了解如何在 Cron 触发器中配置自定义参数。

<span id="属性"></span>
## 属性

<span id="job"></span>
### job

返回 Cron 触发器的名称。

<span id="cronexpression"></span>
### cronExpression

返回 Cron 触发器的 Cron 表达式。

<span id="示例代码"></span>
## 示例代码

```JavaScript
// 注册一个事件监听器，监听 cron 事件
addEventListener('cron', onCron);

// cron 事件被触发时，被调用的回调函数
async function onCron(event) {
    // 这里可以添加定时任务的具体代码
    return 'Parameter: ' + await event.text();
}
```
