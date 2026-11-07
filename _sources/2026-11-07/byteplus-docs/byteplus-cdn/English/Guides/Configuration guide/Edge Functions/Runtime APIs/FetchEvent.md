---
title: "FetchEvent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent"
---

A fetch\-type event triggered by a domain trigger.

See the MDN documentation for [FetchEvent](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Edge Functions runtime does not allow you to construct a <code>FetchEvent</code> object using the <code>FetchEvent()</code> constructor. You need to register a listener to listen for fetch events by calling <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener">addEventListener()</a> to obtain the <code>FetchEvent</code> object.</div>


<span id="methods"></span>
## Methods

<span id="respondwith"></span>
### respondWith()

When a fetch event is triggered, Edge Functions intercepts the user request and uses the [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response) object or the [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) object you pass to this method as the response.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you do not call the <code>respondWith()</code> method, Edge Functions will forward the user request to BytePlus CDN when the fetch event is triggered.</div>


<span id="examples"></span>
#### Examples

```js
// Edge Functions will forward the user request to BytePlus CDN.
addEventListener(
    'fetch', (event) => {
      console.log("callback1 has been triggered");
    });

// Edge Functions will intercept the user request and allow you to pass a Response object to the method's parameter as the response.
addEventListener(
    'fetch', (event) => {
      console.log("callback2 has been triggered");
      event.respondWith(new Response("callback2 has been triggered"));  
    });
```


<span id="waituntil"></span>
### waitUntil()

Notifies the Edge Functions runtime to wait for all [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) objects registered in the callback function to be resolved or rejected. The `waitUntil()` method can be called multiple times. You can also nest `waitUntil()` methods within each other.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If the function execution time exceeds the <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Usage_Limits_Functions">Usage Limits</a>, the Edge Functions runtime will destroy the request context and will no longer wait for <code>Promise</code> objects in a pending state.</div>


* <div data-tips="true" data-tips-type="warning">If any <code>Promise</code> object registered by <code>waitUntil()</code> is rejected, the Edge Functions runtime will destroy the request context. It is recommended to add error handling for each <code>Promise</code>, such as using the <code>.catch()</code> method or <code>try-catch</code> statements.</div>



If you do not call the `waitUntil()` method and do not use `await`, the Edge Functions runtime will destroy the request context when the callback function returns a response through `respondWith()`, and will no longer wait for `Promise` objects in a pending state. Although `await` can wait for `Promise` objects to be resolved or rejected, it pauses the execution of the callback function. In comparison, the `waitUntil()` method allows the callback function to continue executing other operations while waiting for `Promise` objects to be resolved or rejected.

<span id="examples"></span>
#### Examples

```JavaScript
// Define the URL for uploading logs
const uploadURL = "https://log-collection.example.com/";

// Async function to upload response time
async function uploadLog(waiter) {
    const start = Date.now();
    // Wait for the waiter promise to complete, indicating the request response has been sent
    await waiter;
    // Record the end time. Note: The edge function's clock is aligned to approximately 10 ms, which is to prevent side-channel attacks.
    const end = Date.now();
    const cost = (end - start);
    // Serialize the object to a JSON string as the request body
    const body = JSON.stringify({ cost: cost });
    await fetch(uploadURL, {
        method: "POST",
        body: body,
        headers: {
            'Content-Type': 'application/json'
        }
    });
}

// Listen for fetch events and call the handle function to process when the event occurs
addEventListener('fetch', (event) => {
    event.respondWith(handle(event));
});

// Function to handle events
async function handle(event) {
    const response = new Response("Hello World");
    // response.body is a readableStream. the Edge Functions runtime API includes the waitClose method
    // waitClose returns a promise. When the stream is terminated (possibly due to error or completion), waitClose will be resolved
    // Note: If your Response is used to return a response without a Body, such as a response to an HTTP HEAD request, a 304 response, or a 204 response, then waitClose() is ineffective
    event.waitUntil(uploadLog(response.body.waitClose()));
    return response;
}
```


<span id="properties"></span>
## Properties

<span id="info"></span>
### info

Gets client information.


* `info.clientIp`: The IP address of the client. If the client is configured with a proxy, this property returns the IP address of the proxy server.

* `info.geo`: The geographic information of the client IP. geo has the following properties:

   * `geo.country`: Returns the name of the country to which the IP address belongs, such as `China` or `United States`.

   * `geo.countryCode`: Returns the two\-letter country code of the IP address, compliant with the ISO 3166\-1 alpha\-2 standard. For example, `CN` or `US`.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can only identify Hong Kong, China (Hong Kong), Macao, China (Macao), and Taiwan, China (Taiwan) via the <code>province</code> field. The <code>countryCode</code> for Hong Kong, Macao, and Taiwan is <code>CN</code>.   </div>
   

   * `geo.region`: Returns the name of the geographical region in China to which the IP address belongs. For example, `EastChina`. If the IP address does not belong to Chinese Mainland, this parameter returns `XX`.

   * `geo.province`: Returns the name of the first\-level administrative division to which the IP address belongs. For example, `Hebei` or `New Jersey`.

   * `geo.city`: Returns the name of the city to which the IP address belongs. For example, `Shijiazhuang` or `Tampere`.

   * `geo.isp`: Returns the name of the ISP to which the IP address belongs. For example, `ChinaUnicom` or `DigitalOcean`.


<span id="examples"></span>
#### Examples

```JavaScript
addEventListener(
    'fetch', (event) => { event.respondWith(handle(event)); });
    
async function handle(event) {
  const info = event.info;
  console.log(info);  // Get all client information

  const clientIp = event.info.clientIp;
  console.log(clientIp); // Get the client's IP address

  const country = event.info.geo.country;
  console.log(country); // Get the country name of the client's IP address

  return new Response("done");
}
```


<span id="file"></span>
### File

See the MDN documentation [File](https://developer.mozilla.org/en-US/docs/Web/API/File).

<span id="blob"></span>
### Blob

See the MDN documentation [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob).

<span id="formdata"></span>
### FormData

See the MDN documentation [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData).
