---
title: "The API gateway by default will convert the header to lowercase"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/The_API_gateway_by_default_will_convert_the_header_to_lowercase"
---

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

When processing HTTP requests, the API gateway converts all HTTP Header keys to lowercase letters, to standardize uniformly. Generally, the HTTP Header is case\-insensitive, so there is no problem.

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

If your HTTP Header is case\-sensitive, issues may arise.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

It is recommended to unify HTTP Headers in business logic to lowercase, or adapt specifically to this scenario.
