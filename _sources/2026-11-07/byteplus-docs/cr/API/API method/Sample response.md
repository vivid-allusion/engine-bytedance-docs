---
title: "Sample response"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/sample-response"
---

All responses of Container Registry (CR) OpenAPI contain the RequestId, Action, Version, Service, and Region fields.

<span id="正常返回示例"></span>
## Sample of a normal response

If an API call is successful, the response contains the request ID and response parameters. This kind of response is considered normal. The HTTP status code for a normal response is 2xx.

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202004011722300102****", //Obtained from the header of X-Top-Request-Id.
        "Action": "{Action}",//Obtained from the query of the request Action.
        "Version": "{Version}",//Obtained from the query of the request Version.
        "Service": "{Service}",//Obtained from the header of X-Top-Service.
        "Region": "{Region}" //Obtained from the header of X-Top-Region.
    },
    "Result":"..."
}

```


<span id="异常返回示例"></span>
## Sample of an abnormal response

If an error occurs when you call an API action, the request ID and an error message are returned. This kind of response is considered abnormal. The HTTP status code for an abnormal response is 4xx or 5xx.

Find the returned error code in the common error codes and API\-specific error codes and take troubleshooting measures accordingly.

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202010201722300102****",
        "Action": "{Action}",
        "Version": "{Version}",`
        "Service": "{Service}",
        "Region": "{Region}",
        "Error": {
            "Code": "InvalidActionOrVersion",
            "Message": "Could not find operation GetUserById for version 2020-04-01"
        }
    }
}
```
