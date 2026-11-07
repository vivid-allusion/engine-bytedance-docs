---
title: "ModifyNLBBackendServersAttributes - Modifying the backend server information"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNLBBackendServersAttributes"
---

Call the ModifyNLBBackendServersAttributes API to modify the weight, port, or description of backend servers in the server group.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNLBBackendServersAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

In the Servers.N.a type parameters in the table below, "N" represents the serial number of the backend server information. Value range: 1 to 20. Separate multiple backend servers with ampersands (&).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|KvFW6u">必选</span> `Example: ModifyNLBBackendServersAttributes`

Action to execute. Set the value to ModifyNLBBackendServersAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ChKhdj">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|8gQCOq">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Server group ID. You can call the [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) API to get the server group ID.



**Servers.N.ServerId ** <span data-label="purple">String </span><span data-api-tag="require|QBMW0r">必选</span> `Example: rs-124e87shgdqwrc****`

Backend server ID.

You can call the [DescribeNLBServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/DescribeServerGroupAttributes) API to get the backend server ID.



**Servers.N.Port ** <span data-label="purple">Integer </span><span data-api-tag="require|NS0qZG">必选</span> `Example: 1234`

Port used by the backend server to process requests. Value range: 1 to 65535.


* When the server group has not enabled full port forwarding, this parameter is required.

* When the server group has enabled full port forwarding, this parameter defaults to 0.



**Servers.N.Weight ** <span data-label="purple">Integer </span><span data-api-tag="require|QdC3KJ">必选</span>`Example: 100`

Weight of the backend server, with a value range of 0 to 100.


* A weight of 0 indicates that the NLB will not forward requests to this backend server.

* If this parameter is not passed in, it defaults to 0.



**Servers.N.Description ** <span data-label="purple">String </span>`optional` `Example: ecs1`

Description of the backend server.


* Must start with a letter or a Chinese character. May include numbers, commas ( , ), periods ( . ), underscores ( _ ), spaces ( ), equal signs ( = ), hyphens ( \- ), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 1 to 255 characters.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024092952539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyNLBBackendServersAttributes&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea****&Servers.1.ServerId=rs-124e87shgdqwrc****&Servers.1.Port=1234&Servers.1.Weight=100&Servers.1.Description=ecs1 HTTP/1.1
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
        "Action": "ModifyNLBBackendServersAttributes",
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
|400 |InvalidPort.Malformed |The specified Port is malformed. |The format of the specified Port is invalid. |
|400 |InvalidServerGroup.InvalidLoadBalancerBillingStatus |The related LoadBalancers of the specified ServerGroup are not in the correct billing status for the request. |The Classic Load Balancer (CLB) billing method associated with the specified server group is in a status that cannot respond to the request. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidServers.Description.Malformed |The specified Servers.Description is malformed. |The specified Servers.Description parameter format is invalid. |
|400 |InvalidServers.Port.Malformed |The specified Servers.Port is malformed. |The specified Servers.Port parameter format is invalid. |
|400 |InvalidServers.Weight.Malformed |The specified Servers.Weight is malformed. |The specified Servers.Weight parameter format is invalid. |
|400 |LimitExceeded.ServerNumber |You've reached the limit on the number of add servers that you can operate |The maximum number of backend servers that can be operated on in a single request has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidServer.NotFound |The specified Server does not exist. |The specified backend server does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|409 |InvalidServer.Conflict |The specified Server already exists. |The specified backend server already exists. |
|409 |InvalidServerPort.Conflict |The specified Server Port already exists. |The specified backend server port already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
