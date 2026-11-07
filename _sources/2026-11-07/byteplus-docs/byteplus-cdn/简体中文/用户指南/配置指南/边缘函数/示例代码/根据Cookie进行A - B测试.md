---
title: "根据Cookie进行A/B测试"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-AB-Testing-cn"
---

该示例展示了如何根据用户请求中的 Cookie 请求头判断用户属于测试组或对照组，并进行 A/B 测试。


* 如果用户请求中的 Cookie 请求头包含了 test，则返回测试组的响应内容。

* 如果用户请求中的 Cookie 请求头包含了 control，则返回对照组的响应内容。

* 如果用户请求中的 Cookie 请求头不包含 test 或 control，则以 50% 的概率随机返回测试组或对照组的响应内容。


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


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)
