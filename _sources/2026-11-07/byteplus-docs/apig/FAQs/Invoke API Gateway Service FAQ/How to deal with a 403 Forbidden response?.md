---
title: "How to deal with a 403 Forbidden response?"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/How_to_deal_with_a_403_Forbidden_response"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

When calling the API Gateway service, a `403 Forbidden` error is returned, and the response body contains `RBAC: access denied`.

<span id=".5Y-v6IO95Y6f5Zug"></span>
## Possible cause

Configuration issues. The API Gateway service might have credentials turned on, but the request does not carry a valid JWT Token.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

Please use requests with an authentication Token to access the services published by the API Gateway.
