---
title: "EnableTLSAccessLog - Enabling an access log delivery to TLS"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/EnableTLSAccessLog"
---

Call the EnableTLSAccessLog API to enable TLS access log delivery and bind the ALB to a Topic.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 5 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnableTLSAccessLog&serviceCode=alb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|07JiBJ">必选</span> `Example: EnableTLSAccessLog`

The interface name. The current API name is `EnableTLSAccessLog`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|kwN7yH">必选</span> `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.



**LoadBalancerId ** <span data-label="purple"> String  </span><span data-api-tag="require|QRKMil">必选</span> `Example: alb-bp1b6c719dfa08ex****`

ALB instance ID.



**TopicId ** <span data-label="purple"> String </span><span data-api-tag="require|TNze-t">必选</span> `Example: topic-j12hf23gb***`

Bound Topic ID.



**ProjectId ** <span data-label="purple"> String </span><span data-api-tag="require|dryxBe">必选</span> `Example: project-sdfhaj***`

The project corresponding to the Topic.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`Example: 20210811152539010225146063030****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=EnableTLSAccessLog&Version=2020-04-01&LoadBalancerId=alb-bp1b6c719dfa08ex****&ProjectId=pid-s87va8fa****&TopidId=tid-8fa78avd**** HTTP/1.1
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
        "Action": "EnableTLSAccessLog",
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
|400 |InvalidTopic.InUse |The specified Topic is being used by the health log. The health log and the access log can not be delivered to the same TLS at the same time. |The specified log topic is used by the health check log. Health check logs and access logs cannot be delivered to the same TLS topic. |
|400 |OperationFailed.QueryIAM |The request on the specified resource failed due to the query on IAM failed. |The request to operate on this resource failed because the IAM request failed. |
|400 |OperationFailed.QueryTls |The request on the specified resource failed due to the query on TLS failed. |The request to operate on this resource failed because the TLS request failed. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|404 |InvalidTopic.NotFound |The specified Topic does not exist. |The specified log topic does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified log project does not exist. |
