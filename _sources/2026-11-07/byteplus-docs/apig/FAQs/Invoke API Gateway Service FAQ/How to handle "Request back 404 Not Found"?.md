---
title: "How to handle \"Request back 404 Not Found\"?"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/How_to_handle_Request_back_404_Not_Found"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description 

When calling the API Gateway service, it returns a `404 Not Found` error, and the Response Body is empty.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis


* Configuration issue, the request did not match a route.

* Incorrect service protocol. e.g., service A only supports the HTTP protocol, accessing it using the HTTPS protocol will back `404 Not Found`.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


* Check the matching rule(s) in the route (Method/Path/QueryString) to see if they are consistent with the actual HTTP(S) request sent.

* Check if the Service protocol used is correct.
