---
title: "DescribeVpcGatewayEndpointServices - Querying the list of gateway endpoint services"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpointServices"
---

Call the DescribeVpcGatewayEndpointServices API to query the list of gateway endpoint services that meet specific criteria.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcGatewayEndpointServices&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeVpcGatewayEndpointServices`

Action to execute. Set the value to **DescribeVpcGatewayEndpointServices**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**PageNumber** Integer `optional` `Example: 1`

Page number of the list. Default: 1.

**PageSize ** Integer`optional` `Example: 10`

The number of entries per page in a pagination query. Maximum: 100. Default: 10.

## Response parameters

**RequestId ** String`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**PageNumber** Integer `optional` `Example: 1`

The current page number.

**PageSize ** Integer`optional` `Example: 10`

Number of entries per page in the current pagination.

**TotalCount ** Integer`optional` `Example: 2`

The total number of gateway endpoint services matching the specified conditions.

**VpcGatewayEndpointServices ** Object[]`optional` `Example: -`

Details of the gateway endpoint service.

**ServiceId ** String`optional` `Example: gwepsvc-2fe630gurkl37k5gfuy33****`

Endpoint service ID.

**ServiceName ** String`optional` `Example: com.volces.privatelink.cn-guangzhou.gwepsvc-2fe630gurkl37k5gfuy33****`

Endpoint service name.

**Description ** String`optional` `Example: endpoint service`

Description of the gateway endpoint service.

**CreationTime ** String`optional` `Example: 2021-07-20T03:32:32+08:00`

Creation time of the gateway endpoint service.

**UpdateTime ** String`optional` `Example: 2021-07-20T03:32:32+08:00`

Last operation time of the gateway endpoint service.

**Status ** String`optional` `Example: Available`

Status of the gateway endpoint service.

* Creating

* Pending: Modifying configuration.

* Available: Available for use.

* Deleting: In the deleting process.

## Request examples

```JSON
GET /?Action=DescribeVpcGatewayEndpointServices&Version=2020-04-01&PageNumber=1&PageSize=10
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpcGatewayEndpointServices",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "TotalCount": 2,
        "VpcGatewayEndpointServices": [
            {
                "Status": "Available",
                "ServiceId": "gwepsvc-2fe630gurkl37k5gfuy33****",
                "UpdateTime": "2021-07-20T03:32:32+08:00",
                "Description": "endpoint service",
                "ServiceName": "com.volces.privatelink.cn-guangzhou.gwepsvc-2fe630gurkl37k5gfuy33****",
                "CreationTime": "2021-07-20T03:32:32+08:00"
            }
        ]
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format of specified pagination parameter is invalid. |
