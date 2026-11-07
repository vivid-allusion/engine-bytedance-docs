---
title: "CreateHealthCheckLogProject - Creating a health check log project"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateHealthCheckLogProject"
---

Call the CreateHealthCheckLogProject API to create a log project for CLB health check.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

For TLS, the number of log projects that can be created per account per region is 20.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateHealthCheckLogProject&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|2Q3XF9">必选</span> `Example: CreateHealthCheckLogProject`

Action to execute. Set the value to **CreateHealthCheckLogProject**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|0a4cWJ">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**LogProjectId ** <span data-label="purple">String </span>`Example: fc6953c1-fe50-43aa-9d26-c1e0a207****`

ID of the log project.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateHealthCheckLogProject&Version=2020-04-01
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateHealthCheckLogProject",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "LogProjectId": "fc6953c1-fe50-43aa-9d26-c1e0a207****",
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidProject.InvalidStatus |The specified Project is not in the correct status for the request. |The specified Project is in a state that cannot respond to the request. |
|403 |Forbidden |You are not authorized to perform operations on the TLS. |No permission to operate on the specified TLS. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidProject.Conflict |The specified Project already exists. |The specified Project already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
