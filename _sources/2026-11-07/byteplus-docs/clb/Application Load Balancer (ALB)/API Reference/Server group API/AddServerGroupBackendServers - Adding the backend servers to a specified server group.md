---
title: "AddServerGroupBackendServers - Adding the backend servers to a specified server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-AddServerGroupBackendServers"
---

Call the AddServerGroupBackendServers API to add backend servers to the specified server group.

## Instructions

* Each server group can have up to 200 backend servers added.

* Submit up to 5 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=AddServerGroupBackendServers&groupName=%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%84&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: AddServerGroupBackendServers`

Action to execute. Set the value to AddServerGroupBackendServers.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**Servers.N.InstanceId ** string[]必选 `Example: Servers.1.InstanceId=i-3tkuehz8oa3vj0wz****&Servers.2.InstanceId=i-&2feo5qd3orri85oxruvxv****`

Backend server.

* Valid values:

   * When `Servers.N.Type` is set to ecs, pass the ID of the ECS instance. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to query the ECS instance ID.

   * When `Servers.N.Type` is set to eni, pass the ID of the secondary ENI attached to the ECS. You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the network interface ID.

   * When `Servers.N.Type` is set to ip, pass the IP address as the backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate multiple backend server IDs with ampersands (&).

**Servers.N.Description ** string[]`optional` `Example: Servers.1.Description=ecs1&Servers.2.Description=ecs2`

Backend server description.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Must start with a letter or Chinese character and may include numbers, commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Must be 1 to 255 characters.

**Servers.N.Type ** string[]必选 `Example: Servers.1.Type=ecs&Servers.2.Type=ecs`

Type of backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1\-20.

* When the server group is of type "instance", the values are as follows:

   * ecs: Elastic Compute Service instance.

   * eni: secondary network interface; the primary ENI is not supported.

* When the server group is of type "ip", the value of this parameter is "ip".

**Servers.N.Ip ** string[]必选 `Example: Servers.1.Ip=192.168.1.66&Servers.2.Ip=192.168.1.88`

The private IP address of the ECS or secondary ENI.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1\-20.

* You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to query the private IP addresses of backend servers of type "ecs";

* Call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the private IP addresses of backend servers of type "eni".

**Servers.N.RemoteEnabled ** string[]`optional` `Example: Servers.1.RemoteEnabled=off&Servers.2.RemoteEnabled=off`

Enable the remote IP feature.

* When the backend server instance type is IP address (i.e., Type takes the value ip), this field is valid.

* Valid values:

   * on: Enable.

   * off (default): Do not enable.

**Servers.N.Weight ** integer[]`optional` `Example: Servers.1.Weight=100&Servers.2.Weight=100`

Weight of the backend server, with a value range of 0 to 100.

* If the weight is set to 0, no requests will be forwarded to that backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* If not specified, it defaults to 0.

**Servers.N.Port ** integer[]必选 `Example: Servers.1.Port=88&Servers.2.Port=443`

Port number on which the backend server receives requests.

* Value range: 1\-65535.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1\-20.

**ServerGroupId ** string必选 `Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210811152539010225146063030****`

Request ID.

**ServerIds ** string[]`Example: ["rs-3ciynux6i1x4w****rszh49sj"]`

Returns the IDs of the added backend servers.

## Request example

```text
GET /?Action=AddServerGroupBackendServers&ServerGroupId=rsp-2ff2u22****ww5oxruwe33hdz&Servers.1.InstanceId=i-3tli51****3vj0wuvaeh&Servers.1.Ip=172.**.**.242&Servers.1.Port=1&Servers.1.Type=ecs&Servers.1.Weight=100&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "AddServerGroupBackendServers",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C",
        "ServerIds": [
            "rs-3ciynux6i1x4w****rszh49sj"
        ]
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |LimitExceed.BackendServer |You've reached the limit on the number of backend servers that you can operate at a time. |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |QuotaExceed.ServerPerInstance |You've reached the limit on the number of backend servers per ALB you can associate with, resource xxx, usage xx/xx. |The maximum number of backend servers that can be associated with a single instance has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.ServerPerGroup |You've reached the limit on the number of backend servers per server group you can add in, resource xxx, usage xx/xx. |The maximum number of backend servers that can be added to each server group has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidLoadBalancer.InvalidStatus |The related LoadBalancer is not in the correct status for the request. |The associated ALB instance is in a state that cannot respond to this request. |
|400 |InvalidServers.Port.Duplicated |The specified Servers.Port is duplicated. |The specified server port is duplicated. |
|400 |InvalidServers.RemoteEnabled.Malformed |The specified Servers.RemoteEnabled is malformed. |The specified Servers.RemoteEnabled parameter format is invalid. |
|400 |InvalidEni.InvalidStatus |The specified Eni is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidEcs.Server.IpMismatch |The specified Ecs and Server.Ip do not match. |The specified IP address does not match the primary ENI IP address of the corresponding ECS instance. |
|400 |InvalidIp.InstanceIdMismatch |The specified Server.Ip and Server.InstanceId do not match. |The specified IP address does not match the instance ID. |
|400 |OperationDenied.AccountArrears |The request on the specified resource is denied due to the account being in arrears status. |The request to operate on this resource was rejected because the account is in an overdue payment state. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidServers.Type.Malformed |The specified Servers.Type is malformed. |The specified Servers.Type parameter format is invalid. |
|400 |InvalidServers.Weight.Malformed |The specified Servers.Weight is malformed. |The specified Servers.Weight parameter format is invalid. |
|400 |InvalidServers.Port.Malformed |The specified Servers.Port is malformed. |The specified Servers.Port parameter format is invalid. |
|400 |InvalidServers.Ip.Malformed |The specified Servers.Ip is malformed. |The specified Servers.Ip parameter format is invalid. |
|400 |InvalidServers.Description.Malformed |The specified Servers.Description is malformed. |The specified Servers.Description parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'Servers.InstanceId'. |This request does not contain the required parameter. Please ensure the request includes all required parameters, such as Servers.InstanceId. |
|400 |InvalidVpcForServerGroup.ServerMismatch |The specified Vpc of ServerGroup and Server do not match. |The VPC of the specified server group does not match that of the backend server. |
|400 |InvalidEni.Server.IpMismatch |The specified Eni and Server.Ip do not match. |The specified IP address does not match the corresponding elastic network interface (ENI) IP address. |
|400 |OperationDenied.EniTypeNotSupport |The request on the specified Eni is denied due to the eni type is not allowed for this action. |The operation request for this ENI is rejected because the ENI does not support this operation. |
|400 |OperationFailed.QueryArkClaw |The request on the specified resource failed due to the query on ArkClaw failed. |The request to operate on this resource failed because the ArkClaw request failed. |
|400 |OperationFailed.QueryEcs |The request on the specified resource failed due to the query on ECS failed. |The request to operate on this resource failed because the ECS request failed. |
|400 |InvalidServers.InstanceId.Malformed |The specified Servers.InstanceId is malformed. |The specified Servers.InstanceId parameter format is invalid. |
|400 |OperationDenied.DomainServerGroupOnlyOneServer |The request on the specified ServerGroup is denied due to domain type server group only supports one backend server. |Because a domain‑type server group only supports adding one backend server, the operation request for this server group has been rejected. |
|400 |OperationDenied.DomainServerNotSupportIp |The request on the specified Server is denied due to domain type backend server does not support Ip parameter. |Because a domain‑type backend server does not support the Ip parameter, the operation request for this backend server has been rejected. |
|400 |OperationDenied.DomainServerNotSupportRemoteEnabled |The request on the specified Server is denied due to domain type backend server does not support RemoteEnabled parameter. |Because a domain‑type backend server does not support the RemoteEnabled parameter, the operation request for this backend server has been rejected. |
|404 |InvalidServer.NotFound |The specified Server does not exist. |The specified server does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|404 |InvalidClaw.NotFound |The specified Claw does not exist. |The specified Claw does not exist. |
|409 |InvalidServers.Port.Conflict |The specified Servers.Port already exists. |The specified server port already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
