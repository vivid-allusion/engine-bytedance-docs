---
title: "Response structure"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Response-examples"
---

Each response from OpenAPIs will carry fields such as `RequestId`, `Action`, `Version`, `Service`, and `Region`.

<span id=".5q2j5bi46L-U5Zue56S65L6L"></span>
## Normal response samples

A request ID and response parameters will be returned if the API is called successfully. The HTTP status code will be `2xx`. Example:

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "202211302208xxxx",
        "Action": "CreateWorkspace",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": " e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
    }
}
```


<span id=".5byC5bi46L-U5Zue56S65L6L"></span>
## Error response samples

A request ID and error message will be returned if errors occur when calling the API. The HTTP status code will be `4xx` or `5xx`. Example:

```json
{
    "ResponseMetadata": {
        "RequestId": "202010201722300102****",
        "Action": "DeleteWorkspace",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing",
        "Error": {
            "Code": "NotFound.Workspace",
            "Message": "The specified Workspace demo is not found."
        }
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can troubleshoot errors based on the API error information <code>Code</code> and <code>Message</code>, and by referring to <a href="https://docs.byteplus.com/en/docs/vmp/Common-error-codes">Pulibc error codes</a> and the error codes of the specific API. </div>
