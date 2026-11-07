---
title: "RemoveServerGroupBackendServers - Removing a backend server from the specified server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-RemoveServerGroupBackendServers"
---

Call the RemoveServerGroupBackendServers API to remove backend servers from the specified server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 5 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=RemoveServerGroupBackendServers&groupName=%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%84&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|qX81I9">必选</span> `Example: RemoveServerGroupBackendServers`

Action to execute. Set the value to RemoveServerGroupBackendServers.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|2ChmGb">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ServerIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|R6c2P5">必选</span> `Example: ServerIds.1=rs-3cig8e5o0kxs06c6rrsqn****&ServerIds.2=rs-3cig8e7n1ozr46c6rrsfn****`

ID of the backend server to be removed, identified by ServerId.


* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate multiple backend server IDs with ampersands (&).



**ServerGroupId ** <span data-label="purple">string </span><span data-api-tag="require|3cRIBV">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=RemoveServerGroupBackendServers&ServerGroupId=rsp-2fegt91****sw5oxruvs4ubo6&ServerIds.1=rs-1g0pv1****v408ibuxxr5z4qk&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "RemoveServerGroupBackendServers",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |OperationDenied.AccountArrears |The request on the specified resource is denied due to the account being in arrears status. |The request to operate on this resource was rejected because the account is in an overdue payment state. |
|400 |LimitExceed.BackendServer |You've reached the limit on the number of backend servers that you can operate at a time. |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'ServerIds'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ServerIds. |
|400 |InvalidServerIds.Duplicated |The specified ServerIds is duplicated. |The specified ServerId is duplicated. |
|400 |InvalidLoadBalancer.InvalidStatus |The related LoadBalancer is not in the correct status for the request. |The associated ALB instance is in a state that cannot respond to this request. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|404 |InvalidBackendServer.NotFound |The specified BackendServer does not exist. |The specified backend server does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
