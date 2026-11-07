---
title: "Common Error Codes"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/PujiSz"
---

<span id="response-status-codes"></span>
## Response status codes

When an API request is successful, the HTTP response status code is 200.

When an API request fails, one of the following situations will occur:


* The HTTP response status code is 4xx or 5xx.

* The ResponseMetadata structure in the response body contains an Error field.


If an exception occurs in the response, the content of the response body is as follows. In this case, you can troubleshoot the issue based on the `CodeN`, `Code`, and `Message` information in the `Error` structure.

<span id="successful-api-response-example"></span>
## Successful API response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20240621110427F961A7CE518600259E6B",
        "Action": "StartRouting",
        "Version": "2023-01-01",
        "Service": "GTM",
        "Region": "ap-southeast-1"
    }
}
```


<span id="failed-api-response-example"></span>
## Failed API response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2024062111014665B8676790B979245583",
        "Action": "StartRouting",
        "Version": "2023-01-01",
        "Service": "GTM",
        "Region": "ap-southeast-1",
        "Error": {
            "CodeN": 600402,
            "Code": "Resource does not exist",
            "Message": "Resource does not exist",
            "Detail": ""
        }
    }
}   
```
