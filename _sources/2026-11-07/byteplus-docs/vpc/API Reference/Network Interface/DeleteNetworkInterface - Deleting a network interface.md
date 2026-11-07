---
title: "DeleteNetworkInterface - Deleting a network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteNetworkInterface"
---

Call the DeleteNetworkInterface API to delete the secondary network interface.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Secondary network interface not mounted to an ECS instance.

   You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to check if the ENI is attached to an ECS instance. If it is, you can call the [DetachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DetachNetworkInterface) API to detach it.

* Primary ENIs cannot be deleted by calling this API. They are deleted only when the associated ECS instance is deleted.

* [Official BytePlus service ENI](https://docs.byteplus.com/en/docs/vpc/Network-interface-overview#.572R5Y2h57G75Z6L) cannot be deleted by calling this API. It is deleted along with the cloud resource it belongs to when that resource is deleted.

* A secondary network interface with Enabling Deleted with ECS instance will be automatically deleted when the associated ECS instance is deleted.

* DeleteNetworkInterface is an asynchronous API. When a request ID is returned, the system is still deleting in the background. You can call [DescribeNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) to check the status of the network interface. `Deleting` means deleting, and a failed query indicates deletion is complete.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteNetworkInterface&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|yXrBob">必选</span> `Example value: DeleteNetworkInterface`

The interface name. The current API name is `DeleteNetworkInterface`.



**Version ** <span data-label="purple"> string </span><span data-api-tag="require|i7cRmp">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**NetworkInterfaceId ** <span data-label="purple"> String  </span><span data-api-tag="require|EZWSb6">必选</span> `Example value: eni-bp1fgnh68xyz9****`

ID of the secondary network interface to be deleted.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the network interface ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteNetworkInterface&Version=2020-04-01&NetworkInterfaceId=eni-bp1fgnh68xyz9**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteNetworkInterface",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |IncorrectShuttleStatus |The specified Shuttle is not in the correct status for the request. |The specified Shuttle is in a state that cannot respond to this request. |
|400 |InvalidAnycastEip.InvalidStatus |The specified anycast elastic IP address is not in the correct status for the request. |The specified Anycast EIP is in a status that cannot respond to this request. |
|400 |InvalidBond.HasRelation |The specified ENI has a bond relation. |The specified bond ENI has active bindings. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of elastic network interface cannot process this request. |
|400 |InvalidFlowLog.InvalidStatus |The specified flow log is not in the correct status for the request. |The specified flow log is in a status that cannot respond to this request. |
|400 |InvalidInstanceGroup.InvalidStatus |The specified instance group is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTrafficMirrorSession.InvalidStatus |The specified traffic mirror session is not in the correct status for the request. |The specified traffic mirror session is in a state that cannot process this request. |
|400 |InvalidTrunk.InUse |The specified trunk eni has dependent resource of a branch eni. |The specified trunk ENI contains branch ENIs and cannot be deleted. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot process this request. |
|400 |InvalidVpcEip.InUse |The specified vpc eip is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |QuotaExceeded.IPv6Bandwidth |You've reached the limit on the number of IPv6 bandwidth that you can create. |The limit for enabling IPv6 internet bandwidth has been reached. |
|400 |QuotaExceeded.InstanceMember |You've reached the limit on the number of members per instance group. |The maximum number of member instances allowed for the server group has been reached. |
|400 |QuotaExceeded.ShuttleClient |Shuttle client number of the account exceeded quota. |The current user has reached the maximum number of Shuttle Client that can be created. |
|400 |QuotaExceeded.ShuttleServer |Shuttle server number of the account exceeded quota. |The current user has reached the maximum number of Shuttle Server that can be created. |
|403 |Forbidden |You are not authorized to perform operations on ESI related resources. |Insufficient permissions to manage resources associated with the Elastic Reservation Instance. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified elastic network interface. The specified elastic network interface is managed by a cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified elastic network interface does not exist. |
|404 |InvalidInstanceGroup.NotFound |The specified instance group does not exist. |The specified server group does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
