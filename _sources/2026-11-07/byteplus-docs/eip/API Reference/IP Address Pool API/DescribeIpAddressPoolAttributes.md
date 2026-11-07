---
title: "DescribeIpAddressPoolAttributes"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPoolAttributes"
---

Use the DescribeIpAddressPoolAttributes interface to view the detailed information of the specified IP address pool.

<span id="uiSe4vGc"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateIpAddressPool&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeIpAddressPoolAttributes |The action that you want to perform. Value: **DescribeIpAddressPoolAttributes**. |
|Version |String |Yes |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|IpAddressPoolId |String |Yes |ippool\-fda83op\*\*\*\* |ID of the IP address pool.<br><br>You can call the [DescribeIpAddressPools](https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPools) interface to query the ID of the IP address pool. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |ID of the request. |
|IpAddressPoolId |String |ippool\-fda83op\*\*\*\* |The ID of the IP address pool. |
|BusinessStatus |String |Normal |Whether the IP address pool is locked.<br><br><br>* Normal: normal.<br><br>* FinancialLocked: Locked. |
|ISP |String |BGP |ISP. Values are as follows:<br><br><br>* BGP: BGP (Multi\-ISP).<br><br>* ChinaMobile: China Mobile static single line.<br><br>* ChinaTelecom: China Telecom static single\-line.<br><br>* ChinaUnicom: China Unicom static single line.<br><br>* SingleLine_BGP: BGP single line.<br><br>* Fusion_BGP: Fusion BGP.<br><br>* ChinaMobile_Value: China Mobile Offer static single line.<br><br>* China Unicom Offer static single line.<br><br>* China Telecom Offer static single line. |
|Name |String |IpAddressPool01 |Name of the IP address pool. |
|Description |String |This is an IpAddressPool |Description of the IP address pool. |
|CidrBlocks |Array of struct |["101.x.x.x/24"] |Information about the CIDR block in the IP address pool. |
|CreationTime |String |2024\-10\-10T14:17:28+08:00 |Created Time of the IP address pool. |
|UpdateTime |String |2024\-10\-10T14:17:28+08:00 |Update time of the IP address pool. |
|DeletedTime |String |2024\-10\-11 01:00:00 |Resource reclaim time. A return value is available only when the resource is Suspended due to Overdue payments. |
|OverdueTime |String |2024\-10\-11 01:00:00 |The time when the resource was frozen. This parameter will only have a return value when the resource is overdue frozen. |
|ProjectName |String |Project_1 |The name of the project to which the IP address pool belongs. |
|Tags |Array of struct |\- |Tag information of the IP address pool. Specifically, please refer to the table “**Tags**”. |
|Status |String |Available |The status of the IP address pool.<br><br><br>* Creating: It is being created.<br><br>* Available: The route entry is available.<br><br>* Deleting: The route entry is being deleted.<br><br>* Pending: It is being configured. |
|TotalIpCount |Integer |256 |The total number of IP addresses contained in the IP address pool. |
|UsedIpCount |Integer |0 |The number of IP addresses in the IP address pool allocated as EIP. |


**Tags**


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Key |String |k1 |Tag key. |
|Value |String |v1 |Tag value. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=DescribeIpAddressPoolAttributes&Version=2020-04-01&IpAddressPoolId=ippool-fda83op**** HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20210624153033015207C4****",
        "Action": "DescribeIpAddressPoolAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "IpAddressPoolId": "ippool-fda83op****",
        "BusinessStatus":"Normal",
        "ISP": "BGP",
        "Name": "IpAddressPool01",
        "Description": "This is an IpAddressPool",
        "CidrBlocks": [
            "101.0.XX.XX/24"
        ]
        "ProjectName": "Project_1",
        "Tags":[
            {
                "Key":"k1",
                "Value":"v1"
            }
        ]
        "Status": "Available",
        "BusinessStatus": "Normal",
        "TotalIpCount":256,
        "UsedIpCount":0,
        "CreationTime": "2024-10-10T14:17:28+08:00",
        "UpdateTime": "2024-10-10T14:17:28+08:00",
        "OverdueTime": "2024-10-11 01:00:00",
        "DeletedTime": "2024-10-11 01:00:00"
         
         
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Codes

For common error codes, refer to [Public error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HTTP Code |Error codes |Error Message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters in this idempotent request are inconsistent with those in the previous request. |
||InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified client token is invalid and cannot exceed 64 ASCII characters in length. |
|404 |InvalidIPPool.NotFound |The specified IP address pool does not exist. |The specified IP address pool does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as previous one that is still in process. |The idempotent request is being processing. |
