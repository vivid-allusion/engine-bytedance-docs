---
title: "How It Works"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/How_It_Works_Functions"
---

This document introduced how functions and Edge KV work.

<span id="how-functions-work"></span>
## How functions work

<span id="how-functions-are-event-driven"></span>
### How functions are event\-driven

The functions you create in Edge Functions are event\-driven functions. To make functions execute under conditions you specify, you need to create triggers for the functions. Triggers include domain triggers and Cron triggers. Triggers fire corresponding events when certain conditions are met. When an event is triggered, the callback function specified by the event listener you registered for that event in your function code will be called.

In Edge Functions, you call the `addEventListener()` method to create an event listener.

<span id="domain-triggers"></span>
#### Domain triggers

To create a domain trigger, you need to associate a BytePlus CDN domain with a function and set up function forwarding rules for that domain. If an HTTP/HTTPS request accessing that domain matches the function forwarding rules, the domain trigger will fire a fetch event.

Domain triggers only support HTTP/HTTPS requests.

Edge Functions share edge nodes with BytePlus CDN. When users access a BytePlus CDN domain, they first obtain the IP address of the nearest edge node through DNS resolution, then send HTTP requests to that IP address. When BytePlus CDN receives a user request, it determines whether the request should be handled by the function associated with the domain based on the domain's function forwarding rules.


* If the user request does not match the function forwarding rules, BytePlus CDN will process the user request.

* If the user request matches the function forwarding rules, BytePlus CDN will forward the user request to Edge Functions. At the same time, the domain trigger will fire a fetch event in the code of the function associated with the domain. The callback function registered for the fetch event will be called. Edge Functions will process the user request according to the function's code logic, forward the user request to BytePlus CDN, or to other public cloud services.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_78ba2ef6609766644b4e55542a83deb9.jpeg) </span>

<span id="cron-triggers"></span>
#### Cron triggers

You can create Cron triggers and set up scheduled tasks for them. Cron triggers will fire cron events in the function code at predetermined times. The callback function registered for the cron event will be called. Cron events can be triggered on a single edge node or on all edge nodes.

<span id="in-what-environment-do-functions-run"></span>
### In what environment do functions run

The functions run in the Edge Functions runtime, which is deployed on BytePlus's global edge nodes. Each function can run securely in a V8 isolated environment. The runtime supports JavaScript (ES6) as the programming language. Developers interact with the Edge Functions runtime by calling runtime APIs in the function code. The runtime APIs include some standard APIs from [WinterTC](https://wintertc.org/) and some APIs unique to Edge Functions.

If a function is executed for the first time, or is executed after it has not been executed for a period of time, the runtime needs to allocate resources for that function before executing it. This process is called a "cold start". Compared to traditional container\-based FaaS service, Edge Functions have reduced their cold start time to a single\-digit millisecond level. After the function execution is complete, the resources are retained for a period of time. Functions that run again within this retention period can directly use these resources. This process is called a "warm start".

<span id="function-boundaries-and-lifecycle"></span>
### Function boundaries and lifecycle

To efficiently address resource isolation and garbage collection issues, the runtime defines the boundaries and lifecycle of functions.

Each time a function's code is event\-driven to run, the runtime implicitly associates one or more contexts with all objects in the code. A context is an independent function running environment used to distinguish the boundaries of functions. Objects associated with different contexts cannot access each other. The runtime contexts include **global initialization context** and **request context**.


* Global initialization context: The initialization runtime environment of the function. In the global initialization context, you can call `addEventListener()`, `atob()`,`btoa()` and standard ES6 APIs that are not runtime APIs. The global initialization context is created only during the function's cold start and runs only once.

* Request context: The runtime environment of the callback function registered for an event after the event is triggered. Multiple callback functions can run simultaneously. Global variables are visible to multiple concurrent callback functions. Different callback functions have different request contexts. In the request context, you can call all runtime APIs.


For example, in the code below, when the callback function runs for the first time, the Response object associated with the first request context is assigned to the global variable `respObject` associated with the global initialization context. When it runs for the second time, if the callback function associated with the second request context attempts to access an object associated with the first request context, it will raise a JavaScript runtime exception.

```javascript
addEventListener('fetch', (event) => {
    event.respondWith(handle(event));
});

let respObject = null;
async function handle(event) {
    const request = event.request; 
    if (respObject) {
       console.log(respObject.url); // JavaScript exception will occur
    } else {
        respObject = new Response("This will never work");
    }
    return "Hello World";
}
```


All JavaScript built\-in objects can be used across contexts, including String, Number, Object, Promise, and other objects. For example, the following code will not cause a runtime exception.

```javascript
addEventListener('fetch', (event) => {
    event.respondWith(handle(event));
});

let respObject = null;
async function handle(event) {
    const request = event.request; 
    if (respObject) {
       // Non exception because respObject is a JavaScript built-in object
       console.log(respObject.url); 
    } else {
        respObject = JSON.stringify(event.request);
    }
    return "Hello World";
}
```


Functions have a fixed runtime lifecycle in the runtime environment. For example, for a fetch event, the function's runtime lifecycle begins when the domain name trigger fires the fetch event and ends when the promise registered by the `respondWith()` method is resolved or rejected. After the runtime lifecycle ends, any other asynchronous operations that have not completed will be canceled. From the moment the domain name trigger fires the event, the runtime creates a request context for the function. This request context is implicitly associated with the callback function registered for the event. After the promise registered by the `respondWith()` method is resolved or rejected, the runtime will destroy that request context.

<span id="how-edge-kv-works"></span>
## How Edge KV works

Edge KV service is a distributed key\-value storage service on BytePlus's global edge nodes. After a key\-value pair is written to Edge KV through the Edge Functions console, OpenAPI, CLI or runtime API, it is automatically synchronized to all edge nodes. Functions can quickly read key\-value pairs located on the same edge node through the runtime API. A key\-value pair can be read by one or more functions. After the value of a key\-value pair is updated, the updated value automatically takes effect and is synchronized to all edge nodes. Edge KV data in all edge nodes has eventual consistency, with synchronization completed across all edge nodes within a maximum of 60 seconds.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4cf51da061440dbb53ea953eab91085b.jpeg) </span>

Edge KV data includes namespace and key\-value pairs. A BytePlus account can have one or more namespaces. Each namespace can have one or more key\-value pairs. In a namespace, the key of each key\-value pair is unique.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5e2a608042c3a2182ea8fc203f91ab07.jpeg) </span>
