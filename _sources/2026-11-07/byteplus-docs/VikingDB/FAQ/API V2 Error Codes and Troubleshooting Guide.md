---
title: "API V2 Error Codes and Troubleshooting Guide"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FAQnew"
---

<span id="API v2"></span>
# API v2

<span id="Data Plane API"></span>
## Data Plane API

<span id="Request Success"></span>
### Request Success

In this case, the HTTP response status code is 200, and the `code` value in the response body is `Success`.

Response body example:

```json
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "req_t_1754903451200",
    "result": {
        ......
    }
}
```


<span id="Request Failure"></span>
### Request Failure

In this case, the HTTP response status code is not 200. The `code` field is a string error code, with enumerated values as described in the "Error Code" section. The `message` field is a string that contains a detailed error description.

Response body example:

```json
{
    "code": "NotFound.VikingdbCollection",
    "message": "The specified collection 'test_coll_xx' of VikingDB does not exist.",
    "request_id": "req_t_1754903615941",
    "result": null
}
```


<span id="Control Plane API"></span>
## Control Plane API

<span id="Request Success"></span>
### Request Success

In this case, the HTTP response status code is 200, and there is no `Error` field in the `ResponseMetadata` of the response body.

Response body example:

```json
{
    "ResponseMetadata": {
        "Action": "GetVikingdbCollection",
        "Region": "cn-beijing",
        "RequestId": "20250811170347F97382CA6AA2194B7E4C",
        "Service": "vikingdb",
        "Version": "2025-06-09"
    },
    "Result": {
        "ProjectName": "default",
        "CollectionName": "my_coll_1",
        ......
    }
}
```


<span id="Request Failure"></span>
### Request Failure

In this case, the HTTP response status code is not 200, and the `ResponseMetadata` of the response body includes an `Error` field. The `Code` field is a string error code, with enumerated values as described in the "Error Code" section.

Response body example:

```json
{
    "ResponseMetadata": {
        "Action": "GetVikingdbCollection",
        "Error": {
            "Code": "NotFound.VikingdbCollection",
            "Message": "The specified collection 'my_coll_1_xx' of VikingDB does not exist."
        },
        "Region": "cn-beijing",
        "RequestId": "202508111705278269DB3C6ED5DD706B24",
        "Service": "vikingdb",
        "Version": "2025-06-09"
    }
}
```


<span id="Error Codes (Code)"></span>
## Error Codes

The control plane and data plane use a unified set of error codes, which are of type `string` and briefly describe the cause of the error. Error codes follow the format of "Error Type" or "Error Cause.Error Element". You can locate the root cause of the error based on the error code (Code) and error details (Message).

Common error code enumerated values are as follows:


|Error Code |Meaning |Trigger Conditions |Handling Recommendations |
|---|---|---|---|
|MissingParameter |Missing Parameter |Necessary request parameters are missing. |Complete the request parameters according to the error message. |
|InvalidParameter |Illegal Parameter |The type or format of the input request parameter is incorrect. |Check the request parameters according to the error message. If the error message is unclear, please provide feedback. |
|AccessDenied |<ins>Authentication</ins> Failed |Lack of access rights to resources. |Check whether the <ins>AK</ins>, <ins>SK</ins> are correct, whether the request signature is correct, and whether the sub\-account associated with the AK has access rights to resources in this project. |
|TooManyRequests |Request <ins>Throttling</ins> |Too many requests within a unit of time. |If <ins>throttling</ins> occurs in the retrieval request, increase the CPU Quota. If throttling occurs in other interfaces, check whether there is a problem with the calling method. For information on the throttling quotas for each interface, refer to: [https://www.volcengine.com/docs/84313/1478243](https://www.volcengine.com/docs/84313/1478243) |
|InternalError |Internal Service Error |An unexpected error occurs on the server\-side. |Contact customer service promptly. |
|OperationDenied.Xxx |Operation Denied for Xxx |Although the interface request <ins>authentication</ins> is successful, it does not conform to the internal execution logic. |For example, OperationDenied.VikingdbCollection means that you must delete the associated indexes before you can delete the collection. |
|NotFound.Xxx |Xxx Resource Not Found |The resource in the request parameter cannot be found. |For example, NotFound.VikingdbIndex means that the index cannot be found, and you need to create this index first before performing related operations. |
|AlreadyExists.Xxx |Xxx Resource Already Exists |Resources that must be unique cannot be created more than once. |For example, NotFound.ResourceId means that the ResourceId value in the request already exists and cannot be created repeatedly. |
