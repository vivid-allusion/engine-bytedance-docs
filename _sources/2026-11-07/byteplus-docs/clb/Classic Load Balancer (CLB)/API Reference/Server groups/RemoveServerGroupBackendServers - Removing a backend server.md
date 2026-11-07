---
title: "RemoveServerGroupBackendServers - Removing a backend server"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/RemoveServerGroupBackendServers"
---

Call the RemoveServerGroupBackendServers API to remove backend servers from a specified backend server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

You can remove up to 20 backend servers in a single API call.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RemoveServerGroupBackendServers&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|TIHiZ6">必选</span> `Example: RemoveServerGroupBackendServers`

Action to execute. Set the value to **RemoveServerGroupBackendServers**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|7u5v5x">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|rqCydG">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.

You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to query the backend server group ID.



**ServerIds.N ** <span data-label="purple">String </span><span data-api-tag="require|8XgwiO">必选</span>`Example: rs-3cig8e5o0kxs06c6rrsqn****`

ID of the backend server to be removed, identified by ServerId.

You can call the [DescribeServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/DescribeServerGroupAttributes) API to query the backend server ID.


* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate multiple backend server IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=RemoveServerGroupBackendServers&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea****&ServerIds.1=rs-3cig8e5o0kxs06c6rrsqn**** HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210811152539010225146063030****",
        "Action": "RemoveServerGroupBackendServers",
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
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidServerGroup.ServerMismatch |The specified Server and ServerGroup are not matched. |The specified backend server does not exist in the backend server group. |
|400 |InvalidServerGroup.UnSupportAction |The specified ServerGroup does not support this action. |The specified Server Group does not support the current action. |
|400 |LimitExceeded.ServerNumber |You've reached the limit on the number of add servers that you can operate |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ServerGroupId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ServerGroupId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ServerIds'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ServerIds. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidServer.Conflict |The specified Server already exists. |The specified backend server already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
