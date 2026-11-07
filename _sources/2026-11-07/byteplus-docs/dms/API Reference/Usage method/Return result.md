---
title: "Return result"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Return_result"
---

All returned results include the following fields: `RequestId`, `Action`, `Version`, `Service`, and `Region`. This article describes the return information from the DMS API.

<span id="72dde9ff"></span>
## Example of a successful response

After a successful API call, RequestId and interface return parameters are included in the response. This is considered a normal response. The HTTP status code is 2xx.

```Plain
{
    "ResponseMetadata": {
        "RequestId": "202010201722300102****", 
        "Action": "CreateDataMigrateTask",
        "Version": "2018-01-01",
        "Service": "dms",
        "Region": "cn-beijing" 
    },
    "Result":"..."
}
```


When the request is processed successfully, the response contains `ResponseMetadata` and `Result`. The `Result` varies depending on the requested interface, and different interfaces return different `Result`. Field descriptions are as follows:


|**Field** |**Explanation** |
|---|---|
|RequestId |RequestId is a unique identifier for each API request. |
|Action |The requested interface name is a public parameter for the request. |
|Version |The requested version number is a common parameter in requests. |
|Service |The requested service is a common parameter for requests. |
|Region |Service location information is a common parameter in requests. |


<span id="b1c41735"></span>
## Example of exception response

If the API call fails, RequestId and error information are returned. This is referred to as an exception response. The HTTP status code is 4xx or 5xx.

You can troubleshoot errors based on the error code and message by referring to the common error codes and API error codes.

```Plain
{
    "ResponseMetadata": {
        "RequestId": "202010201722300102****",
        "Action": "CreateDataMigrateTask",
        "Version": "2018-01-01",
        "Service": "dms",
        "Region": "cn-beijing",
        "Error": {
            "Code": "InvalidStorageType",
            "Message": "Not support this source type."
        }
    }
}
```


Compared with a successful result, the error result does not contain the `Result` section. Instead, the `ResponseMetadata` includes an additional `Error` field, which contains `Code` and `Message`. The fields are explained as follows:


|**Field** |**Explanation** |
|---|---|
|Error |Error indicates that the request has failed. |
|Code |The content of Code indicates the specific error code. You can consult the documentation to resolve the problem based on the error code. |
|Message |Message describes the specific reason for the error, which can help you troubleshoot. |
|RequestId |RequestId is the unique identifier for each API request. If you encounter a problem that cannot be resolved independently, you can contact us through the ticketing system and provide the RequestId for your request. We will help investigate the issue. |
