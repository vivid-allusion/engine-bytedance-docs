---
title: "DescribeVpcGatewayEndpoints - Querying the list of qualified gateway endpoints"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints"
---

Call the DescribeVpcGatewayEndpoints API to query the list of gateway endpoints that meet the specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcGatewayEndpoints&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeVpcGatewayEndpoints`

Action to execute. Set the value to **DescribeVpcGatewayEndpoints**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**PageNumber** Integer `optional` `Example: 1`

Page number of the list. Default: 1.

**PageSize ** Integer`optional` `Example: 10`

The number of entries per page in a pagination query. Maximum: 100. Default: 10.

**VpcId ** String`optional` `Example: vpc-bp15zkdt37pq72zv****`

The ID of the VPC to which the gateway endpoint belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC ID.

**EndpointIds.N ** String`optional` `Example: gwep-273yuq6q7bgn47fap8squ****`

ID of the gateway endpoint.

You can call the [DescribeVpcGatewayEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints) API to obtain the gateway endpoint ID.

* Parameter \- N: Represents the serial number of the gateway endpoint ID, ranging from 1 to 100.

* Separate multiple gateway endpoint IDs with ampersands (&).

**EndpointName ** String`optional` `Example: endpoint-01`

Name of the gateway endpoint.

**ProjectName ** String `optional` `Example: default`

The project to which the gateway endpoint belongs.

**TagFilters.N.Key ** String`optional` `Example: k1`

The tag key.

* N specifies the serial number of the tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands (&). Multiple tag keys have a logical AND relationship. The query returns gateway endpoints tagged with all the specified keys.

* The tag key must be unique.

**TagFilters.N.Values.N ** String `optional` `Example: v1`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns gateway endpoints that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).

> **tip**

* > To provide this parameter, provide TagFilters.N.Key first.

* > Passing an empty string queries for gateway endpoints with an empty tag value.

## Response parameters

**RequestId ** String`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**PageNumber** Integer `optional` `Example: 1`

The current page number.

**PageSize ** Integer`optional` `Example: 10`

Number of entries per page in the current pagination.

**TotalCount ** Integer`optional` `Example: 2`

The total number of gateway endpoints matching the specified conditions.

**GatewayEndpoints ** Object[]`optional` `Example: -`

Details of the gateway endpoint.

**EndpointId ** String`optional` `Example: gwep-273yuq6q7bgn47fap8squ****`

ID of the gateway endpoint.

**EndpointName ** String`optional` `Example: endpoint-01`

Name of the gateway endpoint.

**Description ** String`optional` `Example: endpoint service`

The description of the gateway endpoint.

**ServiceId ** String`optional` `Example: gwepsvc-2fe630gurkl37k5gfuy33****`

The ID of the gateway endpoint service.

**ServiceName ** String`optional` `Example: com.volces.privatelink.cn-guangzhou.gwepsvc-2fe630gurkl37k5gfuy33****`

Name of the gateway endpoint service.

**VpcId ** String`optional` `Example: vpc-bp15zkdt37pq72zv****`

The ID of the VPC to which the gateway endpoint belongs.

**CreationTime ** String`optional` `Example: 2021-07-20T03:32:32+08:00`

The creation time of the gateway endpoint.

**UpdateTime ** String`optional` `Example: 2021-07-20T03:32:32+08:00`

The last operation time of the gateway endpoint.

**ProjectName ** String `optional` `Example: default`

Name of the project to which the gateway endpoint belongs.

**VpcPolicy ** String`optional` `Example: { "Statement": [ { "Effect": "Allow", "Principal": "*", "Action": "*", "Resource": "*" } ] }`

Access policy of the gateway endpoint. For detailed descriptions of each field in the access policy, see [Bucket policy parameter reference](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters).

**Tags ** Object[]`optional` `Example: -`

Tag information of the endpoint.

**Key ** String`optional` `Example: k1`

Tag key of the endpoint tag.

**Value ** String`optional` `Example: v1`

Tag value of the endpoint tag.

## Request examples

```JSON
GET /?Action=DescribeVpcGatewayEndpoints&Version=2020-04-01&EndpointName=endpoint-01 HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpcGatewayEndpoints",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "GatewayEndpoints": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "VpcId": "vpc-bp15zkdt37pq72zv****",
                "ServiceId": "gwepsvc-2fe630gurkl37k5gfuy33****",
                "VpcPolicy": "{\n        \"Statement\": [\n                {\n                        \"Effect\": \"Allow\",\n                        \"Principal\": \"*\",\n                        \"Action\": \"*\",\n                        \"Resource\": \"*\"\n                }\n        ]\n}",
                "EndpointId": "gwep-273yuq6q7bgn47fap8squ****",
                "UpdateTime": "2021-07-20T03:32:32+08:00",
                "Description": "endpoint service",
                "ProjectName": "default",
                "ServiceName": "com.volces.privatelink.cn-guangzhou.gwepsvc-2fe630gurkl37k5gfuy33****",
                "CreationTime": "2021-07-20T03:32:32+08:00",
                "EndpointName": "endpoint-01"
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "TotalCount": 2
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format of specified pagination parameter is invalid. |
|400 |LimitExceed.GatewayEndpointNumber |You've reached the limit on the number of gateway endpoints that you can operate. |You have reached the maximum number of gateway endpoints that can be queried in a single request. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue format is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
