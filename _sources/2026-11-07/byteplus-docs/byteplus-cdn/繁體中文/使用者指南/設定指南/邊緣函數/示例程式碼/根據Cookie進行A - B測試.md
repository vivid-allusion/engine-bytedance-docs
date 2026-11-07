---
title: "根據Cookie進行A/B測試"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-AB-Testing-cn-zh-tw"
---

本示例展示如何根據使用者請求中的 Cookie 標頭判斷使用者屬於測試組或對照組，並進行 A/B 測試。


* 若使用者請求中的 Cookie 標頭包含 test，則返回測試組的響應內容

* 若使用者請求中的 Cookie 標頭包含 control，則返回對照組的響應內容

* 若未包含 test 或 control，則以 50% 機率隨機返回測試組或對照組的響應內容


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


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)
