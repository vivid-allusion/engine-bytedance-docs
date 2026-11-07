---
title: "DescribeIpAddressPoolCidrBlocks"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPoolCidrBlocks"
---

Call the DescribeIpAddressPoolCidrBlocks interface to query information about the specified IP address pool CIDR block.

<span id="E4u3mfmJ"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateIpAddressPool&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeIpAddressPoolCidrBlocks |The action that you want to perform. Value:**DescribeIpAddressPoolCidrBlocks**. |
|Version |String |Yes |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|IpAddressPoolId |String |Yes |ippool\-fda83op\*\*\*\* |ID of the IP address pool.<br><br>You can call the [DescribeIpAddressPools](https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPools) interface to query the ID of the IP address pool. |
|CidrBlock |String |No |101.0.XX.XX/24 |CIDR block of IP address. |
|NextToken |String |No |caeba0bbb2be03f84eb48b699f0a\*\*\*\* |The pagination token. This parameter identifies the starting point for the next page of results.<br><br><br>* If not specified, start querying from the beginning.<br><br>* Pass in the `NextToken` returned by the previous API call, then start querying from the marked pagination position of that API call onward. |
|MaxResults |Integer |No |50 |The maximum number of entries to return. Default value: 10. Maximum value: 100. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|RequestId |String |20210624153033015207C4\*\*\*\* |ID of the request. |
|NextToken |String |caeba0bbb2be03f84eb48b699f0a\*\*\*\* |The credentials for the query returned by this API call, marking the pagination position for the next query. Returning empty indicates there is no next page. |
|IpAddressPooCidrBlocks |Array of Struct |\- |CIDR block information of the IP address pool. For details, refer to the following table “**IpAddressPooCidrBlocks structure**”. |


**IpAddressPooCidrBlocks**


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|CidrBlock |String |101.x.x.x/24 |IP address pool CIDR block. |
|Status |String |Available |Status of the CIDR block of the IP address pool. Valid value:<br><br><br>* Creating: It is being created.<br><br>* Available: The route entry is available.<br><br>* Deleting: The route entry is being deleted.<br><br>* Pending: It is being configured. |
|UsedIpCount |Integer |1 |Number of IP addresses allocated as EIP in the IP address pool. |
|TotalIpCount |Integer |256 |Total number of IP addresses contained in the IP address pool. |
|CreationTime |String |2021\-07\-15T21:46:15+08:00 |Created Time of the IP address pool. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=DescribeIpAddressPoolCidrBlocks&Version=2020-04-01&CidrBlock=101.0.XX.XX/24&IpAddressPoolId=ippool-fda83op\*\*\*\* HTTP/1.1
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
        "Action": "DescribeIpAddressPoolCidrBlocks",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
         "RequestId": "20210624153033015207C4****",
         "IpAddressPooCidrBlocks": [
        {
             "CidrBlock": "101.0.XX.XX/24",
             "Status":"Available",
             "UsedIpCount":1,
             "TotalIpCount":256,
             "CreationTime":"2021-07-15T21:46:15+08:00"
         
         }
            ]
  
          "NextToken":"caeba0bbb2be03f84eb48b699f0a****"
          
     }
    
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

Public error codes, refer to [Public error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HTTP Code |Error codes |Error Message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters in this idempotent request are inconsistent with those in the previous request. |
||InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The MaxResults parameter is invalid. |
||InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken parameter is invalid. |
||InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
||InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified client token is invalid and cannot exceed 64 ASCII characters in length. |
|404 |InvalidIPPool.NotFound |The specified IP address pool does not exist. |The specified IP address pool does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as previous one that is still in process. |The idempotent request is being processing. |
