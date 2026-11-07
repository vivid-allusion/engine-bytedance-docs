---
title: "ModifyServerGroupAttributes - Modifying the server group attributes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyServerGroupAttributes"
---

Call the ModifyServerGroupAttributes API to modify a specified backend server group, including the name, description, and related information of the specified servers.

## Instructions

When calling this API, if an optional parameter is not configured, its existing configuration remains unchanged.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyServerGroupAttributes&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: ModifyServerGroupAttributes`

Action to execute. Set the value to **ModifyServerGroupAttributes**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**ServerGroupId ** String必选 `Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.

You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to query the backend server group ID.

**ServerGroupName ** String`optional` `Example: myservergroup`

Name of the backend server group.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.

**Description ** String`optional` `Example: This is a servergroup.`

Description of the backend server group.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

**Servers.N.ServerId ** String必选 `Example: rs-mjc9b2p0v6rk5smt1b27****`

Backend server ID.

You can call the [DescribeServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/DescribeServerGroupAttributes) API to query the backend server ID.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate multiple backend server IDs with ampersands (&).

**Servers.N.Weight ** Integer`optional` `Example: 100`

Weight of the backend server, with a value range of 0 to 100.

* If the weight is set to 0, no requests will be forwarded to that backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

**Servers.N.Port ** Integer`optional` `Example: 88`

Port number on which the backend server receives requests. Value range: 1 to 65535.

Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

**Servers.N.Description ** String`optional` `Example: ecs1`

Description of the backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

## Response parameters

**RequestId ** String`Example: 20210811152539010225146063030****`

Request ID.

## Request examples

```json
GET /?Action=ModifyServerGroupAttributes&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea****&ServerGroupName=myservergroup&Description=This is a servergroup.&Servers.1.ServerId=rs-mjc9b2p0v6rk5smt1b27****&Servers.1.Weight=100&Servers.1.Port=88&Servers.1.Description=ecs1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyServerGroupAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidPort.Malformed |The specified Port is malformed. |The format of the specified Port is invalid. |
|400 |InvalidServerGroupName.Malformed |The specified ServerGroupName is malformed. |The specified ServerGroupName format is invalid. |
|400 |InvalidServers.Description.Malformed |The specified Servers.Description is malformed. |The specified Servers.Description parameter format is invalid. |
|400 |InvalidServers.Port.Malformed |The specified Servers.Port is malformed. |The specified Servers.Port parameter format is invalid. |
|400 |InvalidServers.Weight.Malformed |The specified Servers.Weight is malformed. |The specified Servers.Weight parameter format is invalid. |
|400 |LimitExceeded.ServerNumber |You've reached the limit on the number of add servers that you can operate |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ServerGroupId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ServerGroupId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidServer.NotFound |The specified Server does not exist. |The specified backend server does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidServer.Conflict |The specified Server already exists. |The specified backend server already exists. |
|409 |InvalidServerPort.Conflict |The specified Server Port already exists. |The specified backend server port already exists. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
