---
title: "addEventListener()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener"
---

Register an event listener. Refer to the MDN documentation [addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener).

Edge Functions support the following event types:


* fetch: The event type triggered by domain triggers. See [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent).

* cron: The event type triggered by Cron triggers. See [CronEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-CronEvent).


You can register both cron events and fetch events in the same code file. The callback functions for these two types of events do not interfere with each other. You can register up to 16 callback functions for each event.

You can call `addEventListener()` multiple times to register multiple listeners for the same or different events. You register one callback function in each listener.


* For fetch events, multiple callback functions will be executed in the order they were registered. If a callback function has already called [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent#respondwith) to return a result, subsequent registered but uncalled callback functions will not be executed. If all callback functions fail to return a result within the response time limit, the runtime will throw an error.

* For cron events, only the first callback function will be executed. If the first callback function does not return a result within the response time limit, the runtime will throw an error.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">See <a href="https://docs.byteplus.com/docs/byteplus-cdn/Usage_Limits_Functions">Usage Limits</a> to understand the response time limits for Edge Functions.</div>


<span id="example"></span>
## Example

<span id="listen-for-fetch-events"></span>
### Listen for fetch events

The following code describes how to listen for fetch events.

```JavaScript
addEventListener(
    'fetch', (event) => {
      console.log("callback1 has been triggered");
    });

addEventListener(
    'fetch', (event) => {
      console.log("callback2 has been triggered");
      event.respondWith(new Response("callback2 has been triggered"));  
    });
// This callback function will never be executed
addEventListener('fetch', (event) => {
    console.log("This will never be displayed");
});
```


<span id="listen-for-cron-events"></span>
### Listen for cron events

The following code describes how to listen for cron events.

```javascript
addEventListener('cron', onCron);

async function onCron(event) {

    // 1. You can add payload data to each Cron trigger through OpenAPI or console. 
    // You can get payload data by using the following API of the event object.
  const text = await event.text();

  // 2. Gets attributes of the Cron trigger
  const job = event.job; 
  const cronExpression = event.cronExpression; 
  console.log("cron triggered");
}
```
