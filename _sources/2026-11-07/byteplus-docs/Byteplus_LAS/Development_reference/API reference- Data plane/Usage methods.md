---
title: "Usage methods"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Usage_methods"
---

<span id="17eecf08"></span>
# Base URL


|Region |region id |Base URL |
|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |https://operator.las.ap\-southeast\-1.bytepluses.com |


<span id="ec3f59bb"></span>
# Data plane API authentication

Supports API Key authentication.

<span id="47662561"></span>
## API Key signature authentication

<span id="a6eac7fc"></span>
### Prerequisites

API Key has been created. For details, see [API Key management](https://docs.byteplus.com/docs/Byteplus_LAS/API_key_management).

<span id="7268afdd"></span>
### Signature construction

API Key signature authentication requires adding the `Authorization` header to the HTTP request header as follows:

```Bash
Authorization: Bearer <ARK_API_KEY>
```


<span id="cc9a61a7"></span>
### Examples

```Shell
curl https://operator.las.ap-southeast-1.bytepluses.com/api/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $ARK_API_KEY" \
  -d $'{
    "messages": [
        {
            "content": "You are a helpful assistant.",
            "role": "system"
        },
        {
            "content": "hello",
            "role": "user"
        }
    ],
    "model": "seed-1-5-pro-32k-250115",
    "stream": true
}'
```
