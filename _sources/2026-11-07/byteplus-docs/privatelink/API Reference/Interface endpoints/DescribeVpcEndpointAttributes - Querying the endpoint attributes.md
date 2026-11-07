---
title: "DescribeVpcEndpointAttributes - Querying the endpoint attributes"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointAttributes"
---

Call the DescribeVpcEndpointAttributes API to query detailed information of endpoints that meet the specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcEndpointAttributes&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeVpcEndpointAttributes`

Action to execute. Set the value to **DescribeVpcEndpointAttributes**.

**Version ** String必选 `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.

**EndpointId ** String必选 `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.

## Response parameters

**RequestId ** String`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**Endpoint ID** String `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

**EndpointName ** String`Example: endpoint-01`

The name of the endpoint.

**EndpointType ** String`Example: Interface`

Endpoint type.

* Interface: Interface endpoint.

**IpAddressVersions** String[] `Example: ipv4`

IP protocol type of the endpoint.

* If the return value contains only **ipv4**, it means the endpoint is of the IPv4 type.

* If the return value contains both **ipv4** and **ipv6**, it means the endpoint is of the dual\-stack type.

**Payer ** String`Example: Endpoint`

The account that pays for PrivateLink.

* Endpoint: Endpoint account.

* EndpointService: Endpoint service account.

**EndpointDomain ** String`Example: ep-273yuq6q7bgn47fap8squ****.epsvc-273yuqembrojk7fap8sbf****.cn-guangzhou.privatelink.volces.com`

Domain name of the endpoint. Format: <endpointID\>.<endpointserviceID\>.<regionID\>.privatelink.volces.com.

**Status ** String`Example: Available`

Status of the endpoint.

* Creating

* Pending: Modifying configuration.

* Available: Available for use.

* Deleting

**BusinessStatus ** String`Example: Normal`

Whether the endpoint is locked.

* Normal

* FinancialLocked: Being locked.

> **tip**

> When this parameter returns empty, it indicates that the endpoint is not locked.

**ConnectionStatus ** String`Example: Connecting`

Status of the endpoint connection.

* PendingAcceptance: Waiting for connection

* Connecting

* Connected

* Disconnecting

* Rejected: Connection denied.

* Failed: Connection failed.

* PartialFailed: Partial connection failure.

* ServiceDeleted: The service has been deleted.

**Description ** String`Example: endpoint service`

The description of the endpoint.

**ServiceId** String `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

**ServiceName ** String`Example: com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****`

Endpoint service name.

**ServiceManaged ** Boolean`Example: false`

Indicates whether this is a managed endpoint.

* false: Non\-managed endpoint.

* true: Managed endpoint.

**VpcId ** String`Example: vpc-bp15zkdt37pq72zv****`

The ID of the VPC to which the endpoint belongs.

**PrivateDNSEnabled ** Boolean`Example: false`

Whether private DNS name is enabled for the endpoint.

* false: Disabled.

* true: Enabled.

**PrivateDNSName ** String`Example: www.example.com`

Private DNS name of the endpoint.

This parameter returns empty when the `PrivateDNSEnabled` parameter returns **false**.

**Bps ** Integer`Example: 1000`

The maximum bandwidth of the endpoint connection, measured in Mbps.

**EndpointZoneNums** Integer `Example: 2`

Number of endpoint availability zone.

**CreationTime** String `Example: 2021-07-20T03:32:32+08:00`

The creation time of the endpoint.

**UpdateTime ** String`Example: 2021-07-20T03:32:32+08:00`

Last operation time of the endpoint.

**DeletedTime ** String`Example: 2021-08-20T03:32:32+08:00`

Deletion time of the endpoint.

**ProjectName ** String`Example: default`

Name of the project to which the endpoint belongs.

**Tags ** Object[]`Example: -`

Tag information of the endpoint.

**Key ** String`Example: k1`

Tag key of the endpoint tag.

**Value ** String`Example: v1`

Tag value of the endpoint tag.

**ServiceRegion ** String`Example: cn-beijing`

The region to which the endpoint service belongs.

## Request examples

```json
GET /?Action=DescribeVpcEndpointAttributes&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpcEndpointAttributes",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "Bps": 1000,
        "BusinessStatus": "Normal",
        "ConnectionStatus": "Connecting",
        "CreationTime": "2021-07-20T03:32:32+08:00",
        "DeletedTime": "2021-08-20T03:32:32+08:00",
        "Description": "endpoint service",
        "EndpointDomain": "ep-273yuq6q7bgn47fap8squ****.epsvc-273yuqembrojk7fap8sbf****.cn-guangzhou.privatelink.volces.com",
        "EndpointId": "ep-273yuq6q7bgn47fap8squ****",
        "EndpointName": "endpoint-01",
        "EndpointType": "Interface",
        "EndpointZoneNums": 2,
        "IpAddressVersions": [
            "ipv4",
            "ipv6"
        ],
        "Payer": "Endpoint",
        "PrivateDNSEnabled": false,
        "PrivateDNSName": "www.example.com",
        "ProjectName": "default",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "ServiceId": "epsvc-2fe630gurkl37k5gfuy33****",
        "ServiceManaged": false,
        "ServiceName": "com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****",
        "Status": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2021-07-20T03:32:32+08:00",
        "VpcId": "vpc-bp15zkdt37pq72zv****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
