---
title: "DescribeEipAddresses"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes"
---

Call the DescribeEipAddresses API to query elastic IP addresses (EIPs) that meet the specified conditions.

<span id=".6LCD55So6K-05piO"></span>
## Instructions


* If multiple request parameters are passed in, the system queries based on these parameters and returns the EIP meeting all conditions. If no EIPs meet the conditions, an empty value is returned.

* If no request parameters (including optional ones) are passed in, the system queries based on the currently logged\-in account, and returns all EIPs under that account.

* When using a tag to filter EIP instances, you can query up to 1,000 instances associated with the specified tag. If the count of EIP instances associated with a specified tag exceeds 1,000, use the [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources) API to query.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeEipAddresses&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter


|Parameter name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeEipAddresses |The action that you want to perform. Value: DescribeEipAddresses. |
|Version |String |Yes |2020\-04\-01 |The API version. The current version is 2020\-04\-01. |
|EipAddresses.N |String |No |EipAddresses.1=12.XX.XX.89&EipAddresses.2=12.XX.XX.35 |The address of the EIP.<br><br><br>* N specifies the serial number of an address for the EIP. You can call a maximum of 100 IP addresses in a single request.<br><br>* Separate multiple IP addresses with ampersands (&). |
|AllocationIds.N |String |No |AllocationIds.1=eip\-2zeewb7ujxscd\*\*\*\*&AllocationIds.2=eip\-2wrfgeb3efghxs\*\*\*\* |The ID of the EIP to be queried.<br><br><br>* N specifies the serial number of an EIP ID. You can call a maximum of 100 IDs in a single request.<br><br>* Separate multiple IDs with ampersands (&). |
|Name |String |No |eip\-1 |The name of the EIP, supporting fuzzy query. |
|ISP |String |No |BGP |Internet Service Provider (ISP) Values:<br><br><br>* BGP: BGP (Multi\-ISP).<br><br>* If your account has applied for and enabled permission for the static single\-ISP, you can pass in the following values:<br><br>   * ChinaMobile: China Mobile static single\-ISP.<br><br>   * ChinaTelecom: China Telecom static single\-ISP.<br><br>   * ChinaUnicom: China Unicom static single\-ISP.<br><br>* If your account has applied for and enabled permission for the BGP single\-ISP, you can pass in SingleLine_BGP.<br><br>* If your account has applied for and enabled permission for the premium BGP, you can pass in Premium_BGP.<br><br>* If your account has applied for and enabled permission for the fusion BGP, you can pass in Fusion_BGP.<br><br>* If your account has applied for and enabled permission for the static preferential single\-ISP, you can pass in the following values:<br><br>   * ChinaMobile_Value: The static preferential single\-ISP provided by China Mobile.<br><br>   * ChinaUnicom_Value: The static preferential single\-ISP provided by China Unicom.<br><br>   * ChinaTelecom_Value: The static preferential single\-ISP provided by China Telecom. |
|IpAddressPoolId |String |No |ippool\-2zeerra\*\*\* |The ID of the IP address pool.<br><br>You can call [DescribeIpAddressPools](https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPools) to query the ID of the IP address pool.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The IP address pool is in the beta stage. If you need a trial, please contact your account manager.</div><br> |
|BillingType |Integer |No |2 |The metering method of the EIP. Values:<br><br><br>* 1: Subscription.<br><br>* 2: Pay\-as\-you\-go (Pay\-by\-bandwidth).<br><br>* 3: Pay\-as\-you\-go (Pay\-by\-data\-transfer). |
|ProjectName |String |No |Project_1 |The name of the project to which the EIP belongs. |
|TagFilters.N.Key |String |No |TagFilters.1.Key=k1&TagFilters.2.Key=k2&TagFilters.3.Key=k3 |The tag key of the tag<br><br><br>* N specifies the serial number of the tag key. Valid values: 1–50.<br><br>* Separate multiple tag keys with ampersands (&). The relationship between multiple tag keys is a logical "AND". That is, the query returns EIPs that have all specified tags simultaneously.<br><br>* The tag key must be unique. |
|TagFilters.N.Values.N |String |No |TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2&TagFilters.3.Values.1=v1 |The tag value of the tag.<br><br><br>* The first N specifies the serial number of a tag key. Valid values: 1–10.<br><br>* The second N specifies the serial number of a tag value. Valid values: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns EIPs tagged with any one of the specified values for that key.<br><br>* Separate multiple tag values with ampersands (&).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When passing in an empty string, you query EIPs whose tag value is empty.</div><br> |
|AssociatedInstanceType |String |No |EcsInstance |The type of the cloud product currently associated. Values:<br><br><br>* Nat: Internet NAT Gateway.<br><br>* NetworkInterface: Secondary network interface.<br><br>* ClbInstance: Cloud Load Balancer.<br><br>* Albinstance: Application Load Balancer.<br><br>* EcsInstance: Elastic Compute Service.<br><br>* HaVip: High\-Availability Virtual IP Address<br><br>* IpAddress: Private IP address.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The feature of associating IP addresses for the EIP is in the beta stage. If you need a trial, please contact your account manager to apply.</div><br> |
|AssociatedInstanceId |String |No |i\-2zebbhyczzaweeval\*\*\*\* |The ID of the cloud product instance currently associated. |
|Status |String |No |Available |The status of the EIP. Values:<br><br><br>* Attaching: In the associating process.<br><br>* Detaching: In the disassociating process.<br><br>* Attached: Already associated.<br><br>* Available: Available for use.<br><br>* Deleting: In the deleting process. |
|PageNumber |Integer |No |1 |Page number of the list. Default: 1.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is about to be deprecated. <code>NextToken</code> and <code>MaxResults</code> are recommended for pagination queries.</div><br> |
|PageSize |Integer |No |20 |The number of entries per page. Maximum: 100. Default: 20.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is about to be deprecated. <code>NextToken</code> and <code>MaxResults</code> are recommended for pagination queries.</div><br> |
|NextToken |String |No |caeba0bbb2be03f84eb48b699f0a\*\*\*\* |The pagination token that is used to mark the position in pagination queries.<br><br><br>* If left blank, start querying from the beginning.<br><br>* Pass in the `NextToken` returned by the previous call of this API. The query starts from the pagination position marked by that API call onward. |
|MaxResults |Integer |No |50 |The number of query results. Default: 10. Maximum: 100. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Parameter name |Type |Example value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |The request ID |
|TotalCount |Integer |2 |Total number of EIPs that meet the conditions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is about to be deprecated. When paginating with <code>NextToken</code> and <code>MaxResults</code>, this parameter is meaningless.</div><br> |
|PageNumber |Integer |1 |The current page number.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is about to be deprecated. <code>NextToken</code> and <code>MaxResults</code> are recommended for pagination queries.</div><br> |
|PageSize |Integer |10 |The count of entries per page in the current pagination.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is about to be deprecated. <code>NextToken</code> and <code>MaxResults</code> are recommended for pagination queries.</div><br> |
|NextToken |String |caeba0bbb2be03f84eb48b699f0a\*\*\*\* |The query token returned by this API call, marking the pagination position for the next query. An empty return indicates no next page. |
|EipAddresses |Array of struct |\- |List of EIP information. For details, see the table **EipAddresses structure**. |


**EipAddresses structure**


|Parameter name |Type |Example value |Description |
|---|---|---|---|
|AllocationId |String |eip\-2ze7ujxscd\*\*\*\* |The ID of the EIP. |
|EipAddress |String |12.XX.XX.89 |The address of the EIP. |
|Name |String |eip\-1 |The name of the EIP. |
|Description |String |This is an eip |The description of the EIP. |
|DirectMode |boolean |false |Specify whether to enable directly\-connect.<br><br><br>* true: Yes<br><br>* false: No. |
|ISP |String |BGP |Internet Service Provider (ISP) |
|BillingType |Integer |2 |The billing method of the EIP. |
|Bandwidth |Integer |5 |The bandwidth of the EIP. Unit: Mbps |
|ProjectName |String |Project_1 |The name of the project to which the EIP belongs. |
|Tags |Array of struct |\- |Tag information of the EIP instance. For details, see the table **Tags structure**. |
|InstanceType |String |EcsInstance |The type of the instance currently associated. |
|InstanceId |String |i\-2zebbhyczzaweeval\*\*\*\* |The ID of the instance currently associated. |
|IpAddressPoolId |String |eip\-2zeerra\*\*\* |The ID of the IP address pool. |
|IsBlocked |Boolean |true |Indicate whether it is blocked.<br><br><br>* true: Yes<br><br>* false: No. |
|ReleaseWithInstance |Boolean |true |Specify whether to delete along with the Elastic Compute Service (ECS) instance. Only available for Pay\-as\-you\-go EIPs. When enabled, the EIP will be automatically released when the ECS instance is reclaimed by the system (in 24 hours after unsubscription, due to expiration, or due to arrears) or when the [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API is called.<br><br><br>* true: Yes<br><br>* false: No. |
|BandwidthPackageId |String |bwp\-2zeo05qre24nhrqpy\*\*\*\* |The ID of the Bandwidth Package instance. |
|Status |String |Attaching |The status of the EIP. |
|BusinessStatus |String |FinancialLocked |Indicate whether the EIP is locked.<br><br><br>* Normal: In normal status.<br><br>* FinancialLocked: Being locked. |
|LockReason |String |financial |Indicate the status and cause of the EIP.<br><br><br>* financial: Being locked due to arrears.<br><br>* unlock: In the process of recharge recovery after being suspended due to arrears.<br><br>* empty: Not locked. |
|VpcId<br><br> |String<br><br> |vpc\-257gqcdfvx6n\*\*\*\*<br><br> |The ID of the VPC associated with the EIP.<br><br>This parameter returns a value only when the value of **InstanceType** for the EIP is IpAddress. |
|AllocationTime |String |2021\-07\-15T21:46:15+08:00 |The time when the EIP is created. |
|UpdatedAt |String |2021\-07\-23T11:55:12+08:00 |The time when the EIP is updated. |
|ExpiredTime |String |2021\-05\-07 23:59:59 |The time when the EIP expires.<br><br><br>* For Subscription EIPs, the return value is the expiration time.<br><br>* For Pay\-as\-you\-go EIPs, the return value is empty. |
|OverdueTime |String |2021\-04\-29 01:00:00 |The time when the resource is frozen. This parameter returns a value only when the resource is frozen due to overdue payments. |
|DeletedTime |String |2021\-04\-30 01:00:00 |The scheduled time when the resource is reclaimed forcefully.<br><br><br>* This parameter returns a value for Subscription EIPs.<br><br>* For Pay\-as\-you\-go EIPs, this parameter returns a value only when arrears\-related freezing occurs. |


**Tags structure**


|Parameter name |Type |Example value |Description |
|---|---|---|---|
|Key |String |k1 |Tag key |
|Value |String |v1 |Tag value. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```Plain Text
GET /?Action=DescribeEipAddresses&Version=2020-04-01&BillingType=2&PageNumber=1&PageSize=20 HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeEipAddresses",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
     },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount":2,
        "PageNumber": 1,
        "PageSize": 20,
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "EipAddresses": [
            {
                 "AllocationId": "eip-2ze7ujxscd****",
                 "EipAddress": "12.XX.XX.89",
                 "Name": "eip-1",
                 "Description": "This  is an eip",
                 "DirectMode": "false",
                 "ISP": "BGP",
                 "BillingType": 2,
                 "Bandwidth": 112,
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
                "IpAddressPoolId":"eip-2zeerra***",
                "IsBlocked": true,
                "ReleaseWithInstance": true,
                "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
                "Status": "Attached",
                "BusinessStatus": "Normal",
                "LockReason": "",
                "AllocationTime": "2021-07-22T10:51:41+08:00",
                "UpdatedAt": "2021-07-23T11:55:12+08:00",
                "ExpiredTime": "2021-05-07 23:59:59",
                "OverdueTime": "",
                "DeletedTime": ""
            }
         ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For the common error code, see [Common error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken queried is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order of the specified tag filters is malformed. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag key for filtering is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag value for filtering is invalid. |
|400 |LimitExceeded.AllocationId |You've reached the limit on the number of allocation IDs that you can describe. |The maximum Allocation IDs that you can query have been reached. |
|400 |LimitExceeded.EipAddresses |You've reached the limit on the number of elastic IP addresses that you can describe. |The maximum EIPs that you can query have been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |The maximum tag keys for filtering in a single request have been reached. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |The maximum tag values for filtering in a single request have been reached. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name is malformed. The name cannot be more than 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name is malformed. Correct the name format and try again. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported, or cannot be used. Specified resource with maximum limit 100. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
