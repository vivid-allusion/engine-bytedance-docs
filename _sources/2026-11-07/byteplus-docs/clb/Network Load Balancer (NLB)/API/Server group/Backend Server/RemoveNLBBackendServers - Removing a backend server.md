---
title: "RemoveNLBBackendServers - Removing a backend server"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/RemoveNLBBackendServers"
---

Call the RemoveNLBBackendServers API to remove backend servers from the specified server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Up to 20 servers can be removed in a single API call.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RemoveNLBBackendServers&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|946jlV">必选</span> `Example: RemoveNLBBackendServers`

Action to execute. Set the value to RemoveNLBBackendServers.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|k8mxd7">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|uT7goN">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Server group ID.

You can call the [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) API to get the server group ID.



**ServerIds.N ** <span data-label="purple">String </span><span data-api-tag="require|p2uaDf">必选</span> `Example: rs-3cig8e5o0kxs06c6rrsqn****`

Backend server ID.

You can call the [DescribeNLBServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/DescribeServerGroupAttributes) API to obtain backend server IDs.


* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate backend server IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024092952539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=RemoveNLBBackendServers&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea****&ServerIds.1=rs-3cig8e5o0kxs06c6rrsqn**** HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "RemoveNLBBackendServers",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024092952539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidServerGroup.ServerMismatch |The specified Server and ServerGroup are not matched. |The specified backend server does not exist in the backend server group. |
|400 |LimitExceeded.ServerNumber |You've reached the limit on the number of add servers that you can operate |The maximum number of backend servers that can be operated on in a single request has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
