---
title: "CronEvent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-CronEvent"
---

A cron\-type event triggered by a Cron trigger.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must register a listener to listen for cron events by calling <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener">addEventListener()</a> to get the <code>CronEvent</code> object.</div>


<span id="methods"></span>
## Methods

<span id="text"></span>
### text()

This method returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). When the Promise is resolved, it returns the custom parameter you have configured in the Cron trigger as a [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) object. See [Cron Triggers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers) to learn how to set a custom parameter in a Cron trigger.

<span id="arraybuffer"></span>
### arrayBuffer()

This method returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). When the Promise is resolved, it returns the custom parameter you have configured in the Cron trigger as an [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) object. See [Cron Triggers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers) to learn how to set a custom parameter in a Cron trigger.

<span id="stream"></span>
### stream()

This method returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). When the Promise is resolved, it returns the custom parameter you have configured in the Cron trigger as a [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) object. See [Cron Triggers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers) to learn how to set a custom parameter in a Cron trigger.

<span id="json"></span>
### json()

This method returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). When the Promise is resolved, it returns the custom parameter you have configured in the Cron trigger as a [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON) object. See [Cron Triggers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers) to learn how to set a custom parameter in a Cron trigger.

<span id="properties"></span>
## Properties

<span id="job"></span>
### job

Returns the name of the Cron trigger.

<span id="cronexpression"></span>
### cronExpression

Returns the Cron expression of the Cron trigger.

<span id="example-code"></span>
## Example code

```JavaScript
// Register an event listener to monitor cron events
addEventListener('cron', onCron);

// Callback function that is called when a cron event is triggered
async function onCron(event) {
    // You can add specific code for scheduled tasks here
    return 'Parameter: ' + await event.text();
}
```
