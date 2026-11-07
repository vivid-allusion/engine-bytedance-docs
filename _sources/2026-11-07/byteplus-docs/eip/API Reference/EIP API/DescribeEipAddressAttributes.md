---
title: "DescribeEipAddressAttributes"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/DescribeEipAddresses"
---

Call the DescribeEipAddressAttributes API to query the details about a specified elastic IP address (EIP).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeEipAddressAttributes&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeEipAddressAttributes |The action that you want to perform. Value: DescribeEipAddressAttributes. |
|Version |String |Yes |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|AllocationId |String |Yes |eip\-2ze7ujxscd\*\*\*\* |The EIP IDs to query. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |ID of the request. |
|AllocationId |String |eip\-2ze7ujxscd\*\*\*\* |ID of an EIP. |
|EipAddress |String |10.XX.XX.50 |The IP address of the EIP. |
|Name |String |eip\-1 |The name of the EIP. |
|Description |String |This is an eip |The description of the EIP. |
|DirectMode |boolean |false |Whether to enable pass\-through mode.<br><br><br>* true: Yes.<br><br>* false: No. |
|ISP |String |BGP |The line type.<br><br><br>* BGP: BGP (Multi\-ISP).<br><br>* ChinaMobile: China Mobile static single line.<br><br>* ChinaTelecom: China Telecom static single\-line.<br><br>* ChinaUnicom: Static single ISP for China Unicom<br><br>* SingleLine_BGP: BGP single line.<br><br>* Fusion_BGP: Fusion BGP.<br><br>* ChinaMobile_Value: China Mobile Offer static single line.<br><br>* China Unicom Offer static single line.<br><br>* China Telecom Offer static single line. |
|BillingType |Integer |2 |The metering method of the EIP.<br><br><br>* 1: Subscription.<br><br>* 2: Pay\-by\-bandwidth.<br><br>* 3: pay\-by\-data\-transfer. |
|Bandwidth |Integer |5 |Select the maximum bandwidth for the EIP, in Mbps. |
|ProjectName |String |Project_1 |The name of the project to which the EIP belongs. |
|Tags |Array of struct |\- |The tag information about the EIP. For more information, refer to the following **Tags structure** table. |
|InstanceType |String |EcsInstance |The type of the instance that is associated with the EIP.<br><br><br>* Nat: Internet NAT gateway.<br><br>* NetworkInterface: elastic network interface.<br><br>* ClbInstance: Cloud Load Balancer (CLB).<br><br>* Albinstance: Application Load Balancer (ALB).<br><br>* EcsInstance: Elastic Compute Service (ECS).<br><br>* HAVIP. |
|InstanceId |String |i\-2zebbhyczzaweeval\*\*\*\* |The ID of the instance that is associated with the EIP. |
|IpAddressPoolId |String |eip\-2zeerra\*\*\* |The ID of the IP address pool. |
|IsBlocked |Boolean |true |Indicates whether the EIP is blocked. Valid values:<br><br><br>* true: Yes.<br><br>* false: No. |
|ReleaseWithInstance |Boolean |true |Specify whether to delete the secondary network interface with the ECS instance. Only Pay\-as\-you\-go EIP is valid. After enabling, when an ECS instance is automatically reclaimed by the system (24 hours after Unsubscribe, expiration reclaim, overdue reclaim) or deleted through the [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) interface, the EIP will be released along with it.<br><br><br>* true: Yes.<br><br>* false: No. |
|BandwidthPackageId |String |bwp\-2zeo05qre24nhrqpy\*\*\*\* |The ID of the Bandwidth Package instance. |
|Status |String |Attaching |The state of the EIP.<br><br><br>* Attaching: Associate in progress.<br><br>* Detaching: being detached.<br><br>* Attached: attached.<br><br>* Available: The route entry is available.<br><br>* Deleting: The route entry is being deleted. |
|BusinessStatus |String |FinancialLocked |Indicates whether the EIP is locked.<br><br><br>* Normal: normal.<br><br>* FinancialLocked: Locked. |
|LockReason |String |financial |The reason why the EIP was locked. Valid values:<br><br><br>* financial: locked due to arrears.<br><br>* unlock: Suspended due to arrears and restored during recharge.<br><br>* Empty: normal, not locked. |
|VpcId<br><br> |String<br><br> |vpc\-257gqcdfvx6n\*\*\*\*<br><br> |VPC ID Associated with Elastic IP (EIP).<br><br>The EIP **InstanceType** argument is only backed if the value is IpAddress. |
|AllocationTime |String |2021\-07\-15T21:46:15+08:00 |The time when the EIP was created. |
|UpdatedAt |String |2021\-07\-23T11:55:12+08:00 |The time when the EIP was updated. |
|ExpiredTime |String |2021\-05\-07 23:59:59 |The time when the EIP expired.<br><br><br>* Subscription, the return value is the expiration time.<br><br>* Pay\-as\-you\-go, the return value is empty. |
|OverdueTime |String |2021\-04\-29 01:00:00 |The time when the resource was frozen. A value is returned only after the resource is frozen due to overdue payments. |
|DeletedTime |String |2021\-04\-30 01:00:00 |The time when the resource was forcibly reclaimed.<br><br><br>* Subscription EIP, this parameter has a return value.<br><br>* If the EIP is a usage\-based billing EIP, a value is returned only after the EIP is frozen due to arrears. |


**Tags structure**


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|Key |String |k1 |Tag key. |
|Value |String |v1 |Tag value. |


<span id=".6K-35rGC56S65L6L"></span>
## Request Examples

```Plain Text
GET /?Action=DescribeEipAddressAttributes&Version=2020-04-01&AllocationId=eip-2ze7ujxscd**** HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeEipAddressAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "AllocationId": "eip-2ze7ujxscd****",
        "EipAddress": "10.XX.XX.50",
        "Name": "eip-1",
        "Description": "This  is an eip",
        "DirectMode": "false",
        "ISP": "BGP",
        "BillingType": 2,
        "Bandwidth": 1,
        "ProjectName": "Project_1",
        "Tags":[
            {
                "Key":"k1",
                "Value":"v1"
            },
            {
                "Key":"k2",
                "Value":""
            }
        ],
        "InstanceType": "EcsInstance",
        "InstanceId": "i-2zebbhyczzaweeval****",
        "IpAddressPoolId":"ippool-2zeerra***",
        "IsBlocked": true,
        "ReleaseWithInstance": true,
        "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
        "Status": "Attached",
        "BusinessStatus": "Normal",
        "LockReason": "",
        "AllocationTime": "2019-04-29T01:37:38+08:00",
        "UpdatedAt": "2021-07-21T19:54:56+08:00",
        "ExpiredTime": "",
        "OverdueTime": "",
        "DeletedTime": ""
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Codes

The API operation has no specific error codes. For more information on common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).
