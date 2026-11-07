---
title: "EnableAccessLog - Enabling an access log"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-EnableAccessLog"
---

Call the EnableAccessLog API to enable the access log.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 5 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnableAccessLog&serviceCode=alb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|dzgIsr">必选</span> `Example: EnableAccessLog`

The interface name. The current API name is `EnableAccessLog`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|zKapF-">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**LoadBalancerId ** <span data-label="purple"> String  </span><span data-api-tag="require|gbgDAi">必选</span> `Example: alb-bp1b6c719dfa08ex****`

ALB instance ID.



**BucketName ** <span data-label="purple"> String  </span><span data-api-tag="require|ko8vNP">必选</span> `Example: alb-tos1`

The name of the Torch Object Storage (TOS) bucket used to store access logs.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`Example: 20210811152539010225146063030****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=EnableAccessLog&Version=2020-04-01&LoadBalancerId=alb-bp1b6c719dfa08ex****&BucketName=alb-tos1 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202108171522560****524314701095A5A",
        "Action": "EnableAccessLog",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-test"
    },
    "Result": {
        "RequestId": "202108171522560****524314701095A5A"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |OperationDenied.AccountArrears |The request on the specified resource is denied due to the account being in arrears status. |The request to operate on this resource was rejected because the account is in an overdue payment state. |
|409 |InvalidAccessLog.Conflict |The specified AccessLog of the LoadBalancer already exists. |The access log delivery feature for the specified ALB instance already exists. |
|400 |OperationFailed.QueryIAM |The request on the specified resource failed due to the query on IAM failed. |The request to operate on this resource failed because the IAM request failed. |
|400 |InvalidBucketName.NotFound |The specified Bucket does not exist. |The specified bucket does not exist. |
|400 |OperationFailed.QueryTos |The request on the specified resource failed due to the query on TOS failed. |The request to operate on this resource failed because the TOS request failed. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|403 |Forbidden |You are not authorized to delivery access log to TOS. |You do not have permission to enable access log delivery to TOS. |
