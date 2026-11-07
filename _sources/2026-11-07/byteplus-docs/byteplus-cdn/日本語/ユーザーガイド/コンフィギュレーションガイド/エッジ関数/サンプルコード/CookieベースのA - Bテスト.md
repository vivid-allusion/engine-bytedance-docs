---
title: "CookieベースのA/Bテスト"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-AB-Testing-jp"
---

この例は、ユーザーからのリクエストにあるCookieリクエストヘッダーに基づいて、ユーザーがテストグループに属するか、コントロールグループに属するかを判断し、A/Bテストを実行する方法を示しています。


* ユーザーからのリクエストのCookieリクエストヘッダーに'test'が含まれている場合、テストグループ用のレスポンスコンテンツが返されます。

* ユーザーからのリクエストのCookieリクエストヘッダーに'control'が含まれている場合、コントロールグループ用のレスポンスコンテンツが返されます。

* ユーザーからのリクエストのCookieリクエストヘッダーに'test'も'control'も含まれていない場合、50%の確率でテストグループまたはコントロールグループのいずれかのレスポンスコンテンツがランダムに返されます。


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


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)
