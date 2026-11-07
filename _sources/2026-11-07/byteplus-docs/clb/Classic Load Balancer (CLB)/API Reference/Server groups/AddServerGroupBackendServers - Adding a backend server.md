---
title: "AddServerGroupBackendServers - Adding a backend server"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/AddServerGroupBackendServers"
---

Call the AddServerGroupBackendServers API to add backend servers to the specified server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

In parameters of the type a.N.b, N represents the serial number of the backend server, ranging from 1 to 20, meaning that a maximum of 20 backend servers can be added in a single API call. Separate multiple backend servers with ampersands (&).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddServerGroupBackendServers&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|A9cLzA">必选</span> `Example: AddServerGroupBackendServers`

Action to execute. Set the value to **AddServerGroupBackendServers**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|FD5m5z">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServerGroupId ** <span data-label="purple">String </span><span data-api-tag="require|6Y1g1z">必选</span> `Example: rsp-bp1o94dp5i6ea****`

Backend server group ID.

You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to query the backend server group ID.



**Servers.N.Type ** <span data-label="purple">String </span><span data-api-tag="require|CVYkHT">必选</span> `Example: ecs`

Type of backend server.


* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* When the parameter `ServerGroupId` is set to instance, the values are as follows:

   * ecs: Elastic Compute Service instance.

   * eni: A secondary network interface attached to an ECS.

* When the Type of the parameter `ServerGroupId` is ip, this parameter takes the value ip.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CLB supports adding IP addresses as backend servers is currently in beta stage. If you need a trial, please contact your account manager.</div>




**Servers.N.InstanceId ** <span data-label="purple">String </span><span data-api-tag="require|hBMI0f">必选</span>`Example: i-3tkuehz8oa3vj0wz****`

Backend server.


* Values:

   * When `Servers.N.Type` is set to ecs, pass the ID of the ECS instance. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to query the ECS instance ID.

   * When `Servers.N.Type` is set to eni, pass the ID of the secondary ENI attached to the ECS. You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the network interface ID.

   * When `Servers.N.Type` is set to ip, pass the IP address as the backend server.

* Parameter \- N: Indicates the serial number of the backend server. Value range: 1 to 20.

* Separate multiple backend server IDs with ampersands (&).



**Servers.N.Weight ** <span data-label="purple">Integer </span>`optional` `Example: 100`

Weight of the backend server, with a value range of 0 to 100.


* If the weight is set to 0, no requests will be forwarded to that backend server.

* If this parameter is omitted or left unset, the default value is 0.



**Servers.N.Ip ** <span data-label="purple">String </span><span data-api-tag="require|qFfhN7">必选</span> `Example: 192.XX.XX.2`

Private IP address of the backend server.

You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to query the private IP addresses of backend servers of type "ecs", and call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the private IP addresses of backend servers of type "eni".



**Servers.N.Port ** <span data-label="purple">Integer </span><span data-api-tag="require|9IsAH3">必选</span> `Example: 88`

Port number on which the backend server receives requests. Value range: 1 to 65535.



**Servers.N.Description ** <span data-label="purple">String </span>`optional` `Example: ecs1`

Description of the backend server.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**ServerIds ** <span data-label="purple">String[] </span>`Example: ["rs-3cig8e5o0kxs06c6rrsqn****", "rs-3cig8e7n1ozr46c6rrsfn****"]`

The backend server IDs are the set of IDs of backend servers that were successfully added.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=AddServerGroupBackendServers&Version=2020-04-01&ServerGroupId=rsp-bp1o94dp5i6ea****&Servers.1.Type=ecs&Servers.1.InstanceId=i-3tkuehz8oa3vj0wz****&Servers.1.Weight=100&Servers.1.Ip=192.XX.XX.2&Servers.1.Port=88&Servers.1.Description=ecs1
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
        "Action": "AddServerGroupBackendServers",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****",
        "ServerIds": [
            "rs-3cig8e5o0kxs06c6rrsqn****",
            "rs-3cig8e7n1ozr46c6rrsfn****"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidBackendServer.ServerVpcMismatch |The specified BackendServer and Vpc are not matched. |The specified backend server does not match VPC. |
|400 |InvalidEni.UnSupportAction |The specified Eni does not support this action. |The specified network interface does not support the current operation. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidServer.Type |The specified Server type not match with ServerGroup. |The specified backend server type does not match the server group type. |
|400 |InvalidServerGroup.UnSupportAction |The specified ServerGroup does not support this action. |The specified Server Group does not support the current action. |
|400 |InvalidServerId.ServerIPMismatch |The specified serverIP and InstanceId are not matched. |The specified backend server ID does not match the IP. |
|400 |InvalidServerIp.UnSupportAction |The specified Server Ip does not support this action. |The specified backend server IP does not support the current operation. |
|400 |InvalidServers.Description.Malformed |The specified Servers.Description is malformed. |The specified Servers.Description parameter format is invalid. |
|400 |InvalidServers.Ip.Malformed |The specified Servers.Ip is malformed. |The specified Servers.Ip parameter format is invalid. |
|400 |InvalidServers.Port.Malformed |The specified Servers.Port is malformed. |The specified Servers.Port parameter format is invalid. |
|400 |InvalidServers.Type.Malformed |The specified Servers.Type is malformed. |The specified Servers.Type parameter format is invalid. |
|400 |InvalidServers.Weight.Malformed |The specified Servers.Weight is malformed. |The specified Servers.Weight parameter format is invalid. |
|400 |LimitExceeded.ServerNumber |You've reached the limit on the number of add servers that you can operate |The maximum number of backend servers that can be operated on in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'InstanceId'. |This request is missing a required parameter. Please ensure your API request includes all required parameters, such as InstanceId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ServerGroupId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ServerGroupId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |QuotaExceed.ServerNumberEachInstance |You've reached the limit on the number of Servers that you can create. |The quota limit for the number of backend servers that can be created has been reached. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidServer.NotFound |The specified Server does not exist. |The specified backend server does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidServer.Conflict |The specified Server already exists. |The specified backend server already exists. |
|409 |InvalidServerPort.Conflict |The specified Server Port already exists. |The specified server port already exists. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
