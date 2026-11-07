---
title: "AssociateHaVip"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AssociateHaVip"
---

Call the AssociateHaVip interface to Associate the HAVIP to an ECS instance or a network interface.

<span id=".6LCD55So6K-05piO"></span>
## Instructions


* An HAVIP can be bound to a maximum of 10 ECS instances or 10 network interfaces, but cannot be bound to ECS instances and network interfaces at the same time.

* You need to ensure that the ECS instance or network interface to be associated is in the same subnet as the HAVIP.

* If the HAVIP is to be associated with an Elastic IP (EIP), you can call [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress) to associate it, with the `InstanceType` value set to `HaVip`.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter |Type  |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes   |AssociateHaVip |The action that you want to perform. Value: AssociateHaVip. |
|Version |String |Yes   |2020\-04\-01 |API version information, value is: 2020\-04\-01. |
|HaVipId<br><br> |String<br><br> |Yes  <br><br> |havip\-2zeo05qre24nhrqpy\*\*\*\*<br><br> |ID of the high\-availability virtual IP address you want to associate.<br><br>You can call the [DescribeHaVips](https://docs.byteplus.com/en/docs/vpc/DescribeHaVips) interface to query the ID of the high\-availability virtual IP address. |
|InstanceType<br><br> |String<br><br> |No <br><br> |EcsInstance<br><br> |The Type of instance to associate a high availability virtual IP. Valid value:<br><br><br>* EcsInstance (default): Elastic Compute Service (ECS) instance<br><br>* NetworkInterface: network interface |
|InstanceId<br><br> |String<br><br> |Yes  <br><br> |i\-faf344422ffsfad\*\*\*\*<br><br> |The ID of the instance to associate with the high\-availability virtual IP address.<br><br>You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) or [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) interface to query the ID of the Elastic Compute Service (ECS) instance or the ID of the network interface.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>InstanceType</code> is not specified, pass in the ID of the Elastic Compute Service (ECS) instance for this parameter; if <code>InstanceType</code> is specified, pass in the ID of the instance of the corresponding type for this parameter.</div><br> |
|ClientToken<br><br> |String<br><br> |No <br><br> |123e4567\-e89b\-12d3\-a456\-42665544\*\*\*\*<br><br> |The client token that is used to ensure the request idempotency.<br><br><br>* You can use the client to generate the token, but you must make sure that the token is unique among different requests. This prevents repeated operations due to multiple client retries when the call of the API operation times out or an internal server error occurs.<br><br>* It cannot exceed 64 ASCII characters in length.<br><br>* If you do not specify any value for ClientToken, the API call does not check for idempotency. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter |Type  |Example Value |Description |
|---|---|---|---|
|RequestId |String |F3CD6886\-D8D0\-4FEE\-B93E\-1B732396\*\*\*\* |ID of the request. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=AssociateHaVip&Version=2020-04-01&HaVipId=havip-2zeo05qre24nhrqpy****&InstanceId=i-faf344422ffsfad****&InstanceType=EcsInstance HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B732396****",
        "Action": "AssociateHaVip",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B732396****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table displays only the error codes of the current API. For more error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/vpc/Public-error-codes).


|HttpCode |Error codes |Error Message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters in this idempotent request are inconsistent with those in the previous request. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified elastic network interface is not in the correct status for the request. |
|400 |InvalidHaVip.InvalidStatus |The specified HaVip is not in the correct status for the request. |The specified high availability virtual IP cannot respond to the request due to its current status. |
|400 |InvalidHaVip.NotSupport |The specified HaVip does not support this operation |The specified high availability virtual IP does not support this action. |
|400 |InvalidInstance.HaVipMismatch |The specified instance and HaVip are in different subnets. |The specified instance and high availability virtual IP are not in the same subnet. |
|400 |InvalidInstance.InvalidStatus |The specified instance is not in the correct status for the request. |The specified ECS is not in the correct status for the request. |
|400 |InvalidInstanceType.Malformed |The specified instance type is malformed. |The specified instance Type is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified client token is invalid and cannot exceed 64 ASCII characters in length. |
|400 |LimitExceeded.HaVipsPerInstance |You've reached the limit on the number of HaVips that you can associate with an instance. |Reached the upper limit of high availability virtual IPs that can be associated with each instance. |
|400 |LimitExceeded.InstancesPerHaVip |You've reached the limit on the number of instances that you can associate with a HaVip. |The instance limit for each high availability virtual IP has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is not attached to ECS. |You are not authorized to perform operations on the specified ENI. The specified elastic network interface's associated type is not ECS. |
|403 |Forbidden |You are not authorized to perform operations on the specified HaVip. Cannot bind HaVip to multiple instance types. |No permission to perform actions on the specified high availability virtual IP. The specified high availability virtual IP cannot be associated with both ECS and an elastic network interface simultaneously. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. Cannot associate HaVip with two elastic network interface in the same ECS instance. |You are not authorized to perform operations on the specified ENI. Associating a high availability virtual IP with two network interfaces on the same ECS is not allowed. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |You are not authorized to perform operations on the specified ENI. The elastic network interface is the elastic network interface managed by the cloud product. |
|403 |Forbidden |You are not authorized to perform operations on the specified instance. The specified instance is associated with a HaVip. |No permission to perform actions on the specified instance. The specified instance has already Associated a high availability virtual IP. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|404 |InvalidHaVip.NotFound |The specified HaVip does not exist. |The specified high availability virtual IP does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as previous one that is still in process. |The idempotent request is being processing. |
