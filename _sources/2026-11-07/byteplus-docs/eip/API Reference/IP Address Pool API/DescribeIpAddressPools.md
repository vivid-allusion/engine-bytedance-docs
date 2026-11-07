---
title: "DescribeIpAddressPools"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPools"
---

Call the DescribeIpAddressPools interface to query details of created IP address pools by condition.

<span id="XmWwbrmT"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateIpAddressPool&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeIpAddressPools |The action that you want to perform. Value: **DescribeIpAddressPools**. |
|Version |String |Yes |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|IpAddressPoolIds.N |String |No |ippool\-fda83op\*\*\*\* |The ID of the IP address pool. |
|ISP |String |Yes |BGP |ISP. Values are as follows:<br><br><br>* BGP: BGP (Multi\-ISP).<br><br>* If your Account has applied for and enabled static single\-line permission, you can pass in the following values:<br><br>   * ChinaMobile: China Mobile static single\-line.<br><br>   * ChinaTelecom: China Telecom static single\-line.<br><br>   * ChinaUnicom: China Unicom static single\-line.<br><br>* If your Account has applied for and enabled BGP single\-line permission, you can pass in SingleLine_BGP.<br><br>* If your Account has applied for and activated the Fusion BGP permission, you can pass in Fusion_BGP.<br><br>* If your Account has applied for and enabled Offer static single\-line permission, you can pass in the following values:<br><br>   * ChinaMobile_Value: China Mobile Offer static single\-line.<br><br>   * China Unicom Offer static single line.<br><br>   * China Telecom Offer static single line. |
|Name |String |No |IpAddressPool01 |Name of the IP address pool, fuzzy query is not supported currently.<br><br><br>* Length is limited to 1 ~ 128 characters.<br><br>* Must start with a letter or number and cannot start with http:// or https://. May contain letters, numbers, quotes (:), underscores (_), and hyphens (\-). |
|Status |String |No |Available |Status of the IP address pool. Valid value:<br><br><br>* Creating: It is being created.<br><br>* Available: The route entry is available.<br><br>* Deleting: The route entry is being deleted.<br><br>* Pending: It is being configured. |
|ProjectName |String |No |Project_1 |The name of the project to which the IP address pool belongs. |
|TagFilters.N.Key |String |No |TagFilters.1.Key=k1&TagFilters.2.Key=k2&TagFilters.3.Key=k3 |The keys of one or more tags.<br><br><br>* The parameter \- N specifies the number of the tag key. Valid values: 1–10.<br><br>* Separate tag keys with ampersands ( & ). Tag keys are in a logical AND relationship. In other words, IP address pools with all the tag keys are queried. |
|TagFilters.N.Values.N |String |No |TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2&TagFilters.3.Values.1=v1 |The values of one or more tags.<br><br><br>* The first N specifies the serial number of the Tag key.<br><br>* The second N specifies the serial number of the tag value. Valid values: 1–3. Tag values of the same Tag key are in the logical OR relationship. In other words, IP address pools with any one of the Tag values for the Tag key are queried.<br><br>* Separate multiple tag values with ampersands ( & ).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If an empty string is specified, the IP address pools whose Tag values are null are queried.</div><br> |
|NextToken |String |No |caeba0bbb2be03f84eb48b699f0a\*\*\*\* |The pagination token. This parameter identifies the starting point for the next page of results.<br><br><br>* If not specified, start querying from the beginning.<br><br>* Pass in the `NextToken` returned by the previous API call, then start querying from the marked pagination position of that API call onward. |
|MaxResults |Integer |No |50 |The maximum number of queries. Maximum value: 100. Default value: 10. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|RequestId |String |20210624153033015207C4\*\*\*\* |ID of the request. |
|NextToken |String |caeba0bbb2be03f84eb48b699f0a\*\*\*\* |The credentials for the query returned by this API call, marking the pagination position for the next query. Returning empty indicates there is no next page. |
|IpAddressPools |Array of Struct |\- |CIDR block information of the IP address pool. For details, refer to the table "**IpAddressPools structure**". |


**IpAddressPools**


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|IpAddressPoolId |String |ippool\-fda83op\*\*\*\* |The ID of the IP address pool. |
|BusinessStatus |String |Normal |Whether the IP address pool is locked.<br><br><br>* Normal: normal.<br><br>* FinancialLocked: Locked. |
|ISP |String |BGP |ISP. Values are as follows:<br><br><br>* BGP: BGP (Multi\-ISP).<br><br>* ChinaMobile: China Mobile static single line.<br><br>* ChinaTelecom: China Telecom static single\-line.<br><br>* ChinaUnicom: China Unicom static single line.<br><br>* SingleLine_BGP: BGP single line.<br><br>* Fusion_BGP: Fusion BGP.<br><br>* ChinaMobile_Value: China Mobile Offer static single line.<br><br>* China Unicom Offer static single line.<br><br>* China Telecom Offer static single line. |
|Status |String |Available |The status of the IP address pool.<br><br><br>* Creating: It is being created.<br><br>* Available: The route entry is available.<br><br>* Deleting: The route entry is being deleted.<br><br>* Pending: It is being configured. |
|Name |String |IpAddressPool01 |Name of the IP address pool. |
|Description |String |This is an IpAddressPool |Description of the IP address pool. |
|TotalIpCount |Integer |256 |Total number of IP addresses in the IP address pool. |
|UsedIpCount |Integer |0 |The number of IP addresses in the IP address pool allocated as EIP. |
|CidrBlocks |Array of String |["101.x.x.x/24"] |IP address pool CIDR block. |
|ProjectName |String |Project_1 |The name of the project to which the IP address pool belongs. |
|Tags |Array of struct |\- |Tag information of the IP address pool. For more information, refer to the following **Tags structure** table. |
|CreationTime |String |2024\-10\-10T14:17:28+08:00 |Created Time of the IP address pool. |
|UpdateTime |String |2024\-10\-10T14:17:28+08:00 |Update time of the IP address pool. |
|DeletedTime |String |2024\-10\-11 01:00:00 |Resource reclaim time. A return value is available only when the resource is Suspended due to Overdue payments. |
|OverdueTime |String |2024\-10\-11 01:00:00 |The time when the resource was frozen. A value is returned only after the resource is frozen due to overdue payments. |


**Tags**


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Key |String |k1 |Tag key. |
|Value |String |v1 |Tag value. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=DescribeIpAddressPools&Version=2020-04-01&IpAddressPoolId=ippool-fda83op**** HTTP/1.1
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
        "Action": "DescribeIpAddressPools",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
       "RequestId": "2021062415303301022514515207C4****",
       "NextToken":"caeba0bbb2be03f84eb48b699f0a****",
       "IpAddressPools":[
       {
         "IpAddressPoolId": "ippool-fda83op****",
         "BusinessStatus":"Normal",
         "ISP": "BGP",
         "Status": "Available",
         "Name": "IpAddressPool01",
         "Description": "This is an IpAddressPool",
         "TotalIpCount":256,
         "UsedIpCount":0,
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
        "CreationTime": "2024-10-10T14:17:28+08:00",
        "UpdateTime": "2024-10-10T14:17:28+08:00",
        "OverdueTime": "2024-10-11 01:00:00",
        "DeletedTime": "2024-10-11 01:00:00"
            }
            ]
         
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

Public error codes, please [refer to Public error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HTTP Code |Error Codes |Error Message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters in this idempotent request are inconsistent with those in the previous request. |
||InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The MaxResults parameter is invalid. |
||InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken parameter is invalid. |
||InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
||InvalidParameter |A parameter specified in the request is not valid, is unsupported, or cannot be used. |The request contains an invalid or unsupported parameter. |
||InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified client token is invalid and cannot exceed 64 ASCII characters in length. |
||InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order of the tag used for filtering is invalid. |
||InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag key used for filtering is invalid. |
||InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag value used for filtering is invalid. |
||LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of resources you can operate on at one time. |
||LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys you can filter at a time. |
||LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values you can filter at a time. |
|412 |IdempotentProcessing |The request uses the same client token as previous one that is still in process. |The idempotent request is being processing. |
