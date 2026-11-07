---
title: "DescribeVortexIPAttributes"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPAttributes"
---

Call DescribeVortexIPAttributes to view details of a Vortex IP.

## Request parameters

|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeVortexIPAttributes |The action that you want to perform. Values: DescribeVortexIPAttributes. |
|Version |String |Yes |2020\-04\-01 |API version. The current version is 2020\-04\-01. |
|VortexId |String |Yes |vt\-bp1o94dp5i6ea\*\*\*\* |ID of a Vortex IP.<br><br>You can call the [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs) API to query the ID of the Vortex IP. |

## Response parameters

|Parameter name |Type |Example |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |Request ID. |
|VortexId |String |vt\-bp1o94dp5i6ea\*\*\*\* |ID of a Vortex IP. |
|AccessType |String |Private |Access type of a Vortex IP.<br><br><br>* Public: Internet mode.<br><br>* Private: VPC mode. |
|Endpoint |String |vt.\*\*\*.volces.com |Service domain.<br><br>This parameter returns a value only when the Vortex IP access mode is set to VPC (Private). |
|HttpsServicePort |Integer |443 |HTTPS service proxy port. |
|Socks5ServicePort |Integer |8082 |Socks service proxy port. |
|VortexName |String |VortexIP\-1 |Name of a Vortex IP instance. |
|Description |String |This is a VortexIP |Description of the Vortex IP. |
|Password |String |K29e!s0#57@% |Authentication password of a Vortex IP. |
|AutoRouteRules |Array |["youtube"] |Domain information of the Vortex IP smart routing. |
|Bandwidth |Integer |20 |The maximum bandwidth of a Vortex IP. |
|BillingType |Integer |3 |Billing method.<br><br><br>* 1: Subscription.<br><br>* 3: Pay\-as\-you\-go. |
|ServiceType |String |DataCenter |Service type of a Vortex IP.<br><br><br>* DataCenter: Dynamic data center proxy.<br><br>* ResidentialQuarter: Dynamic residential proxy.<br><br>* VideoOnly: Video\-specific proxy. |
|VpcId |String |vpc\-2feypfmenesqo59gp67yz\*\*\*\* |The ID of the Virtual Private Cloud (VPC) where the Vortex IP is deployed.<br><br>This parameter returns a value only when the Vortex IP access mode is set to VPC (Private). |
|SubnetId |String |subnet\-2feypga30rgg059gp67ag\*\*\*\* |The ID of the subnet where the Vortex IP is deployed.<br><br>This parameter returns a value only when the Vortex IP access mode is set to VPC (Private). |
|ServiceIP |String |12.XX.XX.89 |Service IP.<br><br>This parameter returns a value only when the Vortex IP access mode is set to VPC (Private). |
|ServicePort |Integer |8080 |Service port. |
|Status |String |Active |Status of a Vortex IP.<br><br><br>* Active: Running<br><br>* Creating<br><br>* Configuring<br><br>* Deleting<br><br>* Inactive: Being suspended.<br><br>* CreateFailed: Creation failed. |
|BusinessStatus |String |FinancialLocked |Billing status of a Vortex IP<br><br><br>* Normal<br><br>* FinancialLocked: Being locked. |
|LockReason |String |Financial |Reason of locked.<br><br><br>* Financial: Being locked due to payments.<br><br>* Empty: not locked. |
|CreateTime |String |2024\-05\-19T00:00:00Z |The time when the Vortex IP is created. |
|UpdateTime |String |2024\-05\-19T00:00:00Z |The time when the last action on Vortex IP is performed. |
|OverdueTime |String |2024\-05\-19T00:00:00Z |The time when the resource is overdue suspended. This parameter returns a value only if the resource is suspended due to overdue payments. |
|ReclaimTime |String |2024\-05\-19T00:00:00Z |The time when the resource is reclaimed forcibly. This parameter returns a value only when the resource is suspended due to overdue payments. |
|WhiteListEntries |Array of struct |\- |CIDR blocks listed as the allowlist entries for Vortex IP. For details, see the table: **WhiteListEntries**.<br><br>This parameter returns a value only when the Vortex IP access mode is set to Internet (Public). |

**WhiteListEntries structure**

|Parameter name |Type |Example |Explain |
|---|---|---|---|
|Cidr |String | 101.X.X.0/24 |Source CIDR in Allowlist |
|Description |String |Description of Cidr |Description of a CIDR block. |

## Request examples

```Plain Text
GET /?Action=DescribeVortexIPAttributes&Version=2020-04-01&VortexId=vt-bp1o94dp5i6ea**** HTTP/1.1
Host: open.volcengineapi.com
Service: fasttrack
Region: ap-southeast-1
```

## Response examples

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeEipAddressAttributes",
        "Version": "2020-04-01",
        "Service": "fasttrack",
        "Region": "ap-southeast-1"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "VortexId": "vt-bp1o94dp5i6ea****",
        "VortexName": "VortexIP-1",
        "Description": "This is a VortexIP",
        "Password":"K29e!s0#57@%",
        "AccessType": "Private",
        "AutoRouteRules":[ 
              "youtube" 
          ],
        "WhiteListEntries": ,
        "Endpoint": ,
        "HttpsServicePort":443, 
        "Bandwidth":20,
        "BillingType": 3,
        "ServiceType": "DataCenter",
        "VpcId": "vpc-2feypfmenesqo59gp67yz****",
        "SubnetId": "subnet-2feypga30rgg059gp67ag****", 
        "ServiceIP": "12.XX.XX.89", 
        "ServicePort": 8080,
        "Status": "Active",
        "BusinessStatus": "FinancialLocked",        
        "LockReason": "Financial",
        "CreateTime": "2024-05-19T00:00:00Z",
        "UpdateTime": "2024-05-19T00:00:00Z",
        "OverdueTime": "2024-05-19T00:00:00Z",
        "ReclaimTime": "2024-05-19T00:00:00Z"l,
        "ExpiredTime":"2024-05-19T00:00:00Z"
    }
}
```

## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/gavi-sept-test1/Public_error_codes).

|HttpCode |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidVortexIP.NotFound |The specified Vortex IP does not exist. |The specified Vortex IP does not exist. |
