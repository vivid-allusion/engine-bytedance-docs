---
title: "How to handle \"Token error\"?"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/How_to_handle_Token_error"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

Service authentication not enabled. The user carries JWT Token information in the access request when calling the current Service. The request returns a JWT Token error and access is denied.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Incorrect actions. Please do not use a JWT Token to access services where authentication is not turned on.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

There are two solutions available; please select according to the actual situation:


* Enable authentication for the current gateway Service, and then use the request carrying the Token to access again.

* Remove the Token information from the request and re\-access the gateway Service.
