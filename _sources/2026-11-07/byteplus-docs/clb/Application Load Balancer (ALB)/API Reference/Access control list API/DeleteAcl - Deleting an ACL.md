---
title: "DeleteAcl - Deleting an ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DeleteAcl"
---

Call the DeleteAcl API to delete an ACL.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 5 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteAcl&serviceCode=alb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|Uu2G0w">必选</span> `Example: DeleteAcl`

The interface name. The current API name is `DeleteAcl`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|0n9RZY">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**AclId ** <span data-label="purple"> String  </span><span data-api-tag="require|oWuG0H">必选</span> `Example: acl-3cj44nv0jhhxc6c6rrtet***`

ACL ID to be deleted.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String </span>`Example: 20210811152539010225146063030****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteAcl&AclId=acl-33txelibucdfk57uhwmviq46o&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202108161140290****514606305E9FC1F",
        "Action": "DeleteAcl",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210816114029****2514606305E9FC1F"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |InvalidAclListener.InUse |The specified ACL is being used by listeners. |The specified ACL is in use by the listener. |
|400 |InvalidAcl.InvalidStatus |The specified ACL is not in the correct status for the request. |The specified ACL is in a state that cannot respond to the request. |
|400 |OperationFailed.QueryProject |The request on the specified resource failed due to the query on project failed. |The request to operate on this resource failed because the project query failed. |
|400 |OperationFailed.RemoveFromProjectFailed |The request on the specified resource failed due to removing it from the project failed. |The operation request for the resource failed because removing it from the project was unsuccessful. |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
