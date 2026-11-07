---
title: "AddNLBBackendServers - Adding a backend server"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/AddNLBBackendServers"
---

You can call the AddNLBBackendServers API to add backend servers to server groups.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddNLBBackendServers&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

In the table below, the "N" in the Servers.N.a type parameter represents the serial number of a backend server. Its value range is from 1 to 20. Separate multiple backend servers with ampersands (&).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|tqOPIn">必选</span> `Example: AddNLBBackendServers`

Action to execute. Set the value to AddNLBBackendServers.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|KmVkA7">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|SEbKMa">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Server group ID. You can call the [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) API to get the server group ID.



**Servers.N.Type ** <span data-label="purple">String </span><span data-api-tag="require|8JrW7o">必选</span> `Example: ecs`

Backend server type. Valid values:


* ecs: Elastic Compute Service instance.

* eni: Network interface.

* ip: IP address.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When the type of the Server Group is "instance" and the server to be added is the primary network interface of an Elastic Compute Service (ECS) instance, set the server type to "ecs".</div>


* <div data-tips="true" data-tips-type="tip">When the server to be added is the secondary network interface bound to an Elastic Compute Service (ECS) instance, set the server type to "eni".</div>


* <div data-tips="true" data-tips-type="tip">When the type of the Server Group is "ip", set the server type to "ip".</div>




**Servers.N.InstanceId ** <span data-label="purple">String </span><span data-api-tag="require|rs3qpE">必选</span> `Example: i-3tkuehz8oa3vj0wz****`

ID or IP address of the server instance.


* If the server type is **ecs**, pass the ID of the Elastic Compute Service (ECS) instance. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to get the ECS instance ID.

* If the server type is **eni**, pass the ENI ID associated with the ECS instance. You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to obtain the network interface ID.

* When the server type is **ip**, provide the IP address of the backend server.



**Servers.N.ZoneId ** <span data-label="purple">String </span>`optional` `Example: cn-beijing-a`

Specify the availability zone of the NLB instance associated with the backend server. The parameter is required when parameter `Servers.N.Type` is **ip**.


* When the NLB instance enables **Cross\-az forwarding**, the backend server can receive traffic from all availability zones of the NLB instance.

* When the NLB instance disables **Cross\-az forwarding**, the backend server can only receive traffic from the specified availability zones.



**Servers.N.Weight ** <span data-label="purple">Integer </span>`optional` `Example: 100`

Weight of the backend server, with a value range of 0 to 100.


* A weight of 0 indicates that requests will not be forwarded to this server.

* If this parameter is not passed in, it defaults to 0.



**Servers.N.Ip ** <span data-label="purple">String </span><span data-api-tag="require|YeJtnB">必选</span> `Example: 192.168.1.2`

Private IP address of the backend server.


* You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to obtain the private IP address of the backend server of type ecs.

* You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to obtain the private IP address of the backend server of type eni.



**Servers.N.Port** <span data-label="purple">Integer</span> <span data-api-tag="require|cSi76B">必选</span> `Example: 88`

Port number of the backend server for receiving requests. The value range is 1 to 65535.


* The parameter `AnyPortEnabled` is set to "false", indicating full port forwarding is disabled for the server group, this parameter is required.

* When the parameter `AnyPortEnabled` is set to "true", indicating full port forwarding is enabled for the server group, this parameter defaults to 0.



**Servers.N.Description ** <span data-label="purple">String </span>`optional` `Example: ecs1`

The backend server description, default: empty string.


* Must start with a letter, number, or Chinese character. It may contain the following special characters: comma ( , ), period ( . ), underscore ( _ ), space ( ), equal sign ( = ), hyphen ( \- ), full\-width comma ( ， ), and full\-width period ( 。 )

* The length limit is 0 to 255 characters.

* If this parameter is not provided, it defaults to an empty string.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024092952539010225146063030****`

Request ID.



**ServerIds ** <span data-label="purple">String[] </span>`Example: ["rs-3cig8e5o0kxs06c6rrsqn****", "rs-3cig8e7n1ozr46c6rrsfn****"]`

ID of all backend servers in the server group.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=AddNLBBackendServers&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea****&Servers.1.Type=ecs&Servers.1.InstanceId=i-3tkuehz8oa3vj0wz****&Servers.1.ZoneId=cn-beijing-a&Servers.1.Weight=100&Servers.1.Ip=192.168.1.2&Servers.1.Port=88&Servers.1.Description=ecs1 HTTP/1.1
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
        "Action": "AddNLBBackendServers",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024092952539010225146063030****",
        "ServerIds": [
            "rs-3cig8e5o0kxs06c6rrsqn****",
            "rs-3cig8e7n1ozr46c6rrsfn****"
        ]
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
|400 |InvalidBackendServer.ServerVpcMismatch |The specified BackendServer and Vpc are not matched. |The specified backend server does not match the VPC. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidEni.UnSupportAction |The specified Eni does not support this action. |The specified network interface does not support the current operation. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidServer.Type |The specified Server type not match with ServerGroup. |The specified backend server type does not match the server group type. |
|400 |InvalidServerGroup.InvalidLoadBalancerBillingStatus |The related LoadBalancers of the specified ServerGroup are not in the correct billing status for the request. |The Classic Load Balancer (CLB) billing method associated with the specified server group is in a status that cannot respond to the request. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidServerId.ServerIPMismatch |The specified serverIP and InstanceId are not matched. |The specified backend server ID does not match the IP. |
|400 |InvalidServerIp.UnSupportAction |The specified Server Ip does not support this action. |The specified backend server IP does not support the current action. |
|400 |InvalidServers.Description.Malformed |The specified Servers.Description is malformed. |The specified Servers.Description parameter format is invalid. |
|400 |InvalidServers.Ip.Malformed |The specified Servers.Ip is malformed. |The specified Servers.Ip parameter format is invalid. |
|400 |InvalidServers.Port.Malformed |The specified Servers.Port is malformed. |The specified Servers.Port parameter format is invalid. |
|400 |InvalidServers.Type.Malformed |The specified Servers.Type is malformed. |The specified Servers.Type parameter format is invalid. |
|400 |InvalidServers.Weight.Malformed |The specified Servers.Weight is malformed. |The specified Servers.Weight parameter format is invalid. |
|400 |InvalidServers.ZoneId.Malformed |The specified Servers.ZoneId is malformed. |The specified Servers.ZoneId parameter format is invalid. |
|400 |LimitExceeded.ServerNumber |You've reached the limit on the number of add servers that you can operate |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |QuotaExceed.ServerNumberEachInstance |You've reached the limit on the number of servers that you can mount on instance. |You have reached the quota limit for the number of backend servers that can be mounted on a single instance. |
|400 |QuotaExceed.ServerNumberEachServerGroup |You've reached the limit on the number of servers that you can create. |The quota limit for the number of backend servers that can be created in a single server group has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidServer.NotFound |The specified Server does not exist. |The specified backend server does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|404 |InvalidVPC.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The service\-attached role of the load balancer does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|409 |InvalidServer.Conflict |The specified Server already exists. |The specified backend server already exists. |
|409 |InvalidServerPort.Conflict |The specified Server Port already exists. |The specified backend server port already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
