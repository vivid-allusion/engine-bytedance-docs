---
title: "DescribeVpcGatewayEndpointAttributes - Querying the gateway endpoint attribute"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpointAttributes"
---

Call the DescribeVpcGatewayEndpointAttributes API to query the details of gateway endpoints that meet specific criteria.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcGatewayEndpointAttributes&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeVpcGatewayEndpointAttributes`

Action to execute. Set the value to **DescribeVpcGatewayEndpointAttributes**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**EndpointId ** String必选 `Example: gwep-273yuq6q7bgn47fap8squ****`

ID of the gateway endpoint.

You can call the [DescribeVpcGatewayEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints) API to obtain the ID of the gateway endpoint.

## Response parameters

**RequestId ** String`optional` `Example value: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**EndpointId ** String`optional` `Example: gwep-273yuq6q7bgn47fap8squ****`

ID of the gateway endpoint.

**EndpointName ** String`optional` `Example: endpoint-01`

Name of the gateway endpoint.

**Status ** String`optional` `Example: Available`

Status of the gateway endpoint.

* Creating

* Pending: Modifying configuration.

* Available

* Deleting: In the deleting process.

**Description ** String`optional` `Example: endpoint service`

The description of the gateway endpoint.

**ServiceId ** String`optional` `Example: gwepsvc-2fe630gurkl37k5gfuy33****`

ID of the gateway endpoint service.

**ServiceName ** String`optional` `Example: com.volces.privatelink.cn-guangzhou.gwepsvc-2fe630gurkl37k5gfuy33****`

Name of the gateway endpoint service.

**VpcId ** String`optional` `Example: vpc-bp15zkdt37pq72zv****`

The ID of the VPC to which the gateway endpoint belongs.

**CreationTime ** String`optional` `Example: 2021-07-20T03:32:32+08:00`

Creation time of the gateway endpoint.

**UpdateTime ** String`optional` `Example: 2021-07-20T03:32:32+08:00`

Last operation time of the gateway endpoint.

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
GET /?Action=DescribeVpcGatewayEndpointAttributes&Version=2020-04-01&EndpointId=gwep-273yuq6q7bgn47fap8squ**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpcGatewayEndpointAttributes",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "CreationTime": "2021-07-20T03:32:32+08:00",
        "Description": "endpoint service",
        "EndpointId": "gwep-273yuq6q7bgn47fap8squ****",
        "EndpointName": "endpoint-01",
        "ProjectName": "default",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "ServiceId": "gwepsvc-2fe630gurkl37k5gfuy33****",
        "ServiceName": "com.volces.privatelink.cn-guangzhou.gwepsvc-2fe630gurkl37k5gfuy33****",
        "Status": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2021-07-20T03:32:32+08:00",
        "VpcId": "vpc-bp15zkdt37pq72zv****",
        "VpcPolicy": "{\n        \"Statement\": [\n                {\n                        \"Effect\": \"Allow\",\n                        \"Principal\": \"*\",\n                        \"Action\": \"*\",\n                        \"Resource\": \"*\"\n                }\n        ]\n}"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|404 |InvalidGatewayEp.NotFound |The specified GatewayEndpoint does not exist. |The specified gateway endpoint does not exist. |
