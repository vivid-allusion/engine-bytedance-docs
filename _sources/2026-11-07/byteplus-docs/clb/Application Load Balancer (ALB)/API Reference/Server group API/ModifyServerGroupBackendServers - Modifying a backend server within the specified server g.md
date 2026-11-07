---
title: "ModifyServerGroupBackendServers - Modifying a backend server within the specified server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyServerGroupBackendServers"
---

Call the ModifyServerGroupBackendServers API to modify backend servers within the specified server group.

## Instructions

Submit up to 5 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyServerGroupBackendServers&groupName=%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%84&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ModifyServerGroupBackendServers`

Action to execute. Set the value to ModifyServerGroupBackendServers.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**Servers.N.Weight ** integer[]必选 `Example: Servers.1.Weight=100&Servers.2.Weight=100`

Weight of the backend server, with a value range of 0 to 100.

* If the weight is set to 0, no requests will be forwarded to that backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

**Servers.N.Port ** integer[]必选 `Example: Servers.1.Port=88&Servers.2.Port=443`

Port number on which the backend server receives requests.

* Value range: 1\-65535.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

**Servers.N.Description ** string[]`optional` `Example: Servers.1.Description=ecs1&Servers.2.Description=ecs2`

Backend server description.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Must start with a letter or Chinese character and may include numbers, commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Must be 1 to 255 characters.

**Servers.N.Type ** string[]`optional` `Example: Servers.1.Type=ecs&Servers.2.Type=eni`

Backend server type.

* Values: ecs, eni, ip

* Parameter \- N: Indicates the serial number of the backend server.

**Servers.N.Ip ** string[]`optional` `Example: Servers.1.Ip=10.10.10.10&Servers.2.Ip=10.10.10.11`

Specify IP address.

* Parameter \- N: Indicates the serial number of the specified IP.

**Servers.N.InstanceId ** string[]`optional` `Example: Servers.1.InstanceId=i-ydk3icc9ogobz******&Servers.2.InstanceId=i-jl4kd9b0ws******`

Backend instance ID.

* Parameter \- N: Indicates the serial number of the backend server.

* When ServerType is ecs or eni, this parameter is the resource ID of the ECS instance or ENI, respectively.

* When ServerType is ip, this parameter is an IP address.

**ServerGroupId ** string必选 `Example: rsp-bp1o94dp5i6ea********`

Backend server group ID.

**Servers.N.ServerId ** string[]`optional` `Example: Servers.1.ServerId=rs-3tm2xa50h63vj0x0********&Servers.2.ServerId=rs-l8u2az8md58lltkk********`

Backend server ID.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate multiple backend server IDs with ampersands (&).

* This parameter is optional if the backend instance is specified via parameters like InstanceId.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210811152539010225146063030****`

Request ID.

## Request example

```text
GET /?Action=ModifyServerGroupBackendServers&ServerGroupId=rsp-1g1f1g8rwii****uxxxn4h9n&Servers.1.ServerId=rs-3tm2xa50h63vj0x0****&Servers.1.Port=12&Servers.1.Weight=2&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ModifyServerGroupBackendServers",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain the required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |OperationDenied.AccountArrears |The request on the specified resource is denied due to the account being in arrears status. |The request to operate on this resource was rejected because the account is in an overdue payment state. |
|400 |LimitExceed.BackendServer |You've reached the limit on the number of backend servers that you can operate at a time. |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidServers.Weight.Malformed |The specified Servers.Weight is malformed. |The specified Servers.Weight parameter format is invalid. |
|400 |InvalidServers.Port.Malformed |The specified Servers.Port is malformed. |The specified Servers.Port parameter format is invalid. |
|400 |InvalidServers.Description.Malformed |The specified Servers.Description is malformed. |The specified Servers.Description parameter format is invalid. |
|400 |InvalidServers.ServerId.Duplicated |The specified Servers.ServerId is duplicated. |The specified Servers.ServerId is duplicated. |
|400 |InvalidServers.Port.Duplicated |The specified Servers.Port is duplicated. |The specified server port is duplicated. |
|400 |InvalidLoadBalancer.InvalidStatus |The related LoadBalancer is not in the correct status for the request. |The associated ALB instance is in a state that cannot respond to this request. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|404 |InvalidBackendServer.NotFound |The specified BackendServer does not exist. |The specified backend server does not exist. |
|409 |InvalidServers.Port.Conflict |The specified Servers.Port already exists. |The specified server port already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
