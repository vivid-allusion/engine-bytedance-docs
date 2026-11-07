---
title: "DisableAccessLog - Disabling the layer 7 access log collection"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DisableAccessLog"
---

Call the DisableAccessLog API to disable layer 7 access log collection for the specified CLB instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisableAccessLog&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|a813Iw">必选</span> `Example: DisableAccessLog`

Action to execute. Set the value to **DisableAccessLog**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|1hhRx6">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|5El0IO">必选</span> `Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB Instance ID.



**DeliveryType ** <span data-label="purple">String </span>`optional` `Example: tos`

Log delivery type. Valid values:


* tos (default): Disable log delivery to the Torch Object Storage (TOS).

* tls: Disable log delivery to the Torch Log Service (TLS).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DisableAccessLog&Version=2020-04-01&LoadBalancerId=clb-bp1b6c719dfa08ex****&DeliveryType=tos
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
        "Action": "DisableAccessLog",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancer.UnSupportAction |The specified LoadBalancer does not support this action. |The specified CLB does not support this action. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidAccessLog.NotFound |The specified AccessLog does not exist. |The specified CLB access log does not exist. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
