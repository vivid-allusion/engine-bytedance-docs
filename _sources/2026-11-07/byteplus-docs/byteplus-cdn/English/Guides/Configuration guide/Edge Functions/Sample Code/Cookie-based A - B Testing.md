---
title: "Cookie-based A/B Testing"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-AB-Testing"
---

This example demonstrates how to perform A/B testing by determining whether a user belongs to the test group or the control group based on the Cookie request header in the user's request.


* If the Cookie request header in the user's request contains 'test', the response content for the test group is returned.

* If the Cookie request header in the user's request contains 'control', the response content for the control group is returned.

* If the Cookie request header in the user's request does not contain 'test' or 'control', the response content for either the test group or the control group is randomly returned with a 50% probability.


```JavaScript
addEventListener("fetch", event => {
  event.respondWith(handleRequest(event.request))
})

function handleRequest(request) {
  const NAME = "experiment-0"

  const TEST_RESPONSE = new Response("Test group")
  const CONTROL_RESPONSE = new Response("Control group")

  const cookie = request.headers.get("cookie")
  if (cookie && cookie.includes(`${NAME}=control`)) {
    return CONTROL_RESPONSE
  }
  else if (cookie && cookie.includes(`${NAME}=test`)) {
    return TEST_RESPONSE
  }
  else {
    const group = Math.random() < 0.5 ? "test" : "control" // 50/50 split
    const response = group === "control" ? CONTROL_RESPONSE : TEST_RESPONSE
    response.headers.append("Set-Cookie", `${NAME}=${group}; path=/`)

    return response
  }
}
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)
