---
title: "DescribeVortexIPs"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs"
---

Call DescribeVortexIPs to query Vortex IP instances that meet the specified conditions.

## Request parameters

|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeVortexIPs |The action to perform. Value: DescribeVortexIPs. |
|Version |String |Yes |2020\-04\-01 |API version. The current version is 2020\-04\-01. |
|VortexIds.N |String |No |VortexIds.1=vt\-bp1o94dp5i6ea\*\*\*\*&VortexIds.2=vt\-bp1o94dp5abcde\*\*\*\* |The ID of the Vortex IP.<br><br><br>* N in this parameter represents the sequence number of a Vortex IP ID. You can specify a maximum of 100 IDs in a single request.<br><br>* Separate multiple Vortex IP IDs with ampersands (&). |
|VortexName |String |No |VortexIP\-1 |The name of the Vortex IP instance. |
|AccessType |String |No |Private |The access type of Vortex IP.<br><br><br>* Public: Internet mode.<br><br>* Private: VPC mode.<br><br><br>> **tip**<br><br><br>> Vortex IP in Internet mode is currently in the beta stage. To request a trial, please contact your account manager.<br> |
|ServiceType |String |No |DataCenter |The service type of the Vortex IP.<br><br><br>* DataCenter: Dynamic data center proxy.<br><br>* ResidentialQuarter: Dynamic residential proxy.<br><br>* VideoOnly: Video\-specific proxy. |
|PageNumber |Integer |No |1 |The page number of the list. Default: 1. |
|PageSize |Integer |No |20 |The number of entries per page in a pagination query. Valid values: 1–100. Default: 10. |

## Response parameters

|Parameter name |Type |Example |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |The request ID. |
|TotalCount |Integer |33 |The number of Vortex IPs that meet the specified conditions. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |20 |The number of entries on the current page. |
|VortexIPs |Array of struct |\- |The details of the Vortex IP. For details, see the table below: **VortexIP structure**. |

**VortexIP structure**

|Parameter name |Type |Example |Description |
|---|---|---|---|
|VortexId |String |vt\-bp1o94dp5i6ea\*\*\*\* |The ID of the Vortex IP. |
|VortexName |String |VortexIP\-1 |The name of the Vortex IP instance. |
|Description |String |This is a VortexIP |The description of the Vortex IP. |
|Password |String |K29e!s0#57@% |The authentication password of the Vortex IP. |
|AccessType |String |Private |The access mode of Vortex IP.<br><br><br>* Public: Internet mode.<br><br>* Private: VPC mode. |
|Endpoint |String |vt.\*\*\*.volces.com |The service domain name.<br><br>This parameter returns a value only when the Vortex IP access mode is set to Public. |
|HttpsServicePort |Integer |443 |HTTPS service proxy port. |
|Socks5ServicePort |Integer |8082 |Socks service proxy port. |
|AutoRouteRules |Array |["youtube"] |The domain information of the Vortex IP intelligent routing. |
|Bandwidth |Integer |20 |The maximum bandwidth of the Vortex IP. |
|BillingType |Integer |3 |The metering method.<br><br><br>* 1: Subscription.<br><br>* 3: Pay\-as\-you\-go. |
|ServiceType |String |DataCenter |The service type of the Vortex IP.<br><br><br>* DataCenter: Dynamic data center proxy.<br><br>* ResidentialQuarter: Dynamic residential proxy.<br><br>* VideoOnly: Video\-specific proxy. |
|VpcId |String |vpc\-2feypfmenesqo59gp67yz\*\*\*\* |The ID of the Virtual Private Cloud (VPC) where the Vortex IP is deployed.<br><br>This parameter returns a value only when the Vortex IP access mode is set to Private. |
|SubnetId |String |subnet\-2feypga30rgg059gp67ag\*\*\*\* |The ID of the subnet where the Vortex IP is deployed.<br><br>This parameter returns a value only when the Vortex IP access mode is set to Private. |
|ServiceIP |String |12.XX.XX.89 |The service IP.<br><br>This parameter returns a value only when the Vortex IP access mode is set to Private. |
|ServicePort |Integer |8080 |The service port. |
|Status |String |Active |The status of the Vortex IP.<br><br><br>* Active: Running.<br><br>* Creating<br><br>* Configuring<br><br>* Deleting<br><br>* Inactive: Suspended.<br><br>* CreateFailed: Creation failed. |
|BusinessStatus |String |FinancialLocked |The billing status of the Vortex IP<br><br><br>* Normal<br><br>* FinancialLocked: Locked |
|LockReason |String |Financial |The reason of locking.<br><br><br>* Financial: Being locked due to payments.<br><br>* Empty: Not locked. |
|WhiteListEntries |Array of struct |\- |The CIDR blocks listed as the allowlist entries for Vortex IP. For details, see the table below: **WhiteListEntries**.<br><br>This parameter returns a value only when the Vortex IP access mode is set to Public. |
|VortexAccessLog |Array of struct |\- |The access log information of the Vortex IP. For details, see the table below: **VortexAccessLog**. |
|CreateTime |String |2024\-05\-19T00:00:00Z |The time when the Vortex IP is created. |
|UpdateTime |String |2024\-05\-19T00:00:00Z |The time when the last action on Vortex IP is performed. |
|OverdueTime |String |2024\-05\-19T00:00:00Z |The time when the resource is suspended due to arrears. This parameter returns a value only when the resource is suspended due to arrears. |
|ReclaimTime |String |2024\-05\-19T00:00:00Z |The time when the resource is reclaimed forcibly. This parameter returns a value only when the resource is suspended due to arrears. |

**WhiteListEntries** ** structure**

|Parameter name |Type |Example |Description |
|---|---|---|---|
|Cidr |String | 101.X.X.0/24 |The source CIDR blocks in Allowlist |
|Description |String |Description of Cidr |The description of the CIDR block. |

**VortexAccessLog**

|Parameter name |Type |Example |Description |
|---|---|---|---|
|Enabled |Boolean |true |Describe whether Vortex IP access log is enabled.<br><br><br>* true: Access log is enabled.<br><br>* false: Access log is not enabled.<br><br><br>`TlsProjectName`, `TlsProjectID`, `TlsTopicName`, and `TlsTopicID` return values only when this parameter returns `true`. |
|TlsProjectName |String |test\-project |The log project name of the Vortex IP. |
|TlsProjectID |String |f3\*\*\*\*\*\*\*\*\*\*\*\* |The log project ID of the Vortex IP. |
|TlsTopicName |String |test\-topic |The log topic name of the Vortex IP. |
|TlsTopicID |String |bc\*\*\*\*\*\*\*\*\*\*\* |The log topic ID of the Vortex IP. |

## Request example

```Plain Text
GET /?Action=DescribeVortexIPs&Version=2020-04-01&AllocationId=eip-2ze7ujxscd**** HTTP/1.1
Host: open.volcengineapi.com
Service: fasttrack
Region: ap-southeast-1
```

## Response example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeVortexIPs",
        "Version": "2020-04-01",
        "Service": "fasttrack",
        "Region": "ap-southeast-1"
     }
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount":2,
        "PageNumber": 1,
        "PageSize": 20,
        "VortexIPs": [
            {
                 "VortexId": "vt-bp1o94dp5i6ea****",
                 "VortexName": "VortexIP-1",
                 "Description": "This is a VortexIP",
                 "Password":"K29e!s0#57@%",
                 "AccessType": "Private",
                 "AutoRouteRules":[ 
                       "youtube" 
                   ],
                 "WhiteListEntries": ,
                 "VortexAccessLog":{
                      "Enabled":"true",
                      "TlsProjectName":"test-project",
                      "TlsProjectID":"f3************",
                      "TlsTopicName":"test-topic",
                      "TlsTopicID":"bc***********"
                    },
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
                 "BusinessStatus": "Normal",
                 "LockReason": "",  
                 "CreateTime": "2024-05-19T00:00:00Z",
                 "UpdateTime": "2024-05-19T00:00:00Z",           
                 "OverdueTime": "2024-05-19T00:00:00Z",
                 "ReclaimTime": "2024-05-19T00:00:00Z"d,
                 "ExpiredTime":"2024-05-19T00:00:00Z"
            }
         ]
    }
}
```

## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/gavi-sept-test1/Public_error_codes).

|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidAccessType.Malformed |The specified AccessType is malformed. |The format specified for AccessType is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidVortexName.Malformed |The specified VortexName is malformed. |The format specified for VortexName is invalid. |
|400 |LimitExceeded.VortexIPNumber |You've reached the limit on the number of VortexIPs that you can operate. |You have reached the maximum number of resources that can be processed in a single request. |
