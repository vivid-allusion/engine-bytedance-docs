---
title: "DeleteSnatEntry - Deleting a SNAT rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DeleteSnatEntry"
---

Call the DeleteSnatEntry API to delete a SNAT rule.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteSnatEntry&groupName=SNAT%E8%A7%84%E5%88%99&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|nRqDR1">必选</span> `Example: DeleteSnatEntry`

The action that you want to perform. Value: DeleteSnatEntry.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Sd9Rux">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**SnatEntryId ** <span data-label="purple">string </span><span data-api-tag="require|bWL5Vm">必选</span> `Example: snat-2fedi096gdiww59gp680****`

The ID of the SNAT rule to be deleted.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteSnatEntry&Version=2020-04-01&SnatEntryId=snat-2fedi096gdiww59gp680**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteSnatEntry",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidSnatEntry.InvalidStatus |The specified snat entry is not in the correct status for the request. |The specified SNAT rule cannot respond to this request due to its status. |
|404 |InvalidSnatEntry.NotFound |The specified SNAT entry does not exist. |The specified SNAT rule does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
