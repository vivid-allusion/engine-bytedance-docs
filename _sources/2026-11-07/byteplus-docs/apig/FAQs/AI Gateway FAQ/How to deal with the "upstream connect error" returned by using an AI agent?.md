---
title: "How to deal with the \"upstream connect error\" returned by using an AI agent?"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/How_to_deal_with_the_upstream_connect_error_returned_by_using_an_AI_agent"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

Using an AI APIG instance to proxy a LLM, returning an `upstream connect error or disconnect/reset before headers` error.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e3e588073fa5a94e288211529510ab3b.png) </span>

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The gateway and the backend Upstream cannot connect, possible reasons are as follows:


* If the error is returned a few seconds after the request is sent, it indicates that the network from the APIG instance to the backend upstream is not connected.

* If the error is returned almost within 1 second after the request is sent, it indicates that the connection to the server's port corresponding to upstream has failed. When the network is normal but the port is incorrect, the system will immediately return this error.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


* When the network between the APIG instance and the backend upstream is not connected, please check whether the network between the APIG instance and the backend upstream is connected and whether the security groups allow the corresponding port.

* When the upstream connection to the backend service port fails, please check whether the upstream's backend service port is configured correctly. e.g., when the backend service is an HTTP service on port 8080, please confirm that the HTTP service is properly enabled at port 8080.
