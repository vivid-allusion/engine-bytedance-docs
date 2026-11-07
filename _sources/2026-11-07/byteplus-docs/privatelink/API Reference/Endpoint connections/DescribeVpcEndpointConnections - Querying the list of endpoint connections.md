---
title: "DescribeVpcEndpointConnections - Querying the list of endpoint connections"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointConnections"
---

Call the DescribeVpcEndpointConnections API to query the list of endpoint connections that meet the specified criteria.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcEndpointConnections&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeVpcEndpointConnections`

Action to execute. Set the value to **DescribeVpcEndpointConnections**.

**Version ** String必选 `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.

**PageNumber ** Integer`optional` `Example: 1`

Page number of the list. Default: 1.

**PageSize ** Integer`optional` `Example: 10`

The number of rows per page for paginated queries. Maximum: 100. Default: 10.

**ServiceId ** String必选 `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.

**EndpointId ** String`optional` `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.

**EndpointOwnerAccountId ** String`optional` `Example: 21000****`

The account ID to which the endpoint belongs.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to get the account ID of the endpoint owner.

**EndpointRegion ** String`optional` `Example: cn-beijing`

The ID of the region to which the endpoint belongs.

## Response parameters

**RequestId ** String`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**PageNumber ** Integer`Example: 1`

Current page number.

**PageSize ** Integer`Example: 10`

The number of rows on the current page.

**TotalCount ** Integer`Example: 2`

The total number of endpoint connections matching the specified conditions.

**EndpointConnections ** Object[]`Example: -`

Details of the endpoint connection.

**ServiceId** String `Example: epsvc-2fe630gurkl37k5gfuy33****`

The ID of the endpoint service associated with the endpoint connection.

**Endpoint ID** String `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint associated with the endpoint connection.

**EndpointOwnerAccountId ** String`Example: 21000****`

The account ID to which the endpoint belongs.

**EndpointVpcId ** String`Example: vpc-2744trcju7sw07fap8u05****`

The ID of the VPC to which the endpoint network interface belongs.

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

**Bps ** Integer`Example: 1000`

The maximum bandwidth of the endpoint connection, measured in Mbps.

**Zones ** Object[]`Example: -`

Details of the endpoint availability zone.

**ZoneId ** String`Example: cn-guangzhou-a`

ID of the endpoint availability zone.

**ZoneDomain ** String`Example: ep-273yuq6q7bgn47fap8squ****.cn-guangzhou-a.epsvc-273yuqembrojk7fap8sbf****.cn-guangzhou.privatelink.volces.com`

Domain name of the endpoint availability zone. Format: <Endpoint ID\>.<Availability zones ID\>.<Endpoint Service ID\>.<region ID\>.privatelink.volces.com.

**ZoneStatus ** String`Example: Connected`

Status of the endpoint availability zone.

* PendingAcceptance: Waiting for connection

* Connecting

* Connected

* Disconnecting

* Rejected: Connection denied.

* Failed: Connection failed.

**SubnetId ** String`Example: subnet-2744ts087kglc7fap8tu6****`

The ID of the subnet to which the endpoint network interface belongs.

**NetworkInterfaceId ** String`Example: eni-273w2q67fwq9s7fap8t1a****`

ID of the endpoint network interface.

If undergoing seamless service resource replacement, this represents the ID of the endpoint network interface connected to the service resource being replaced.

**NetworkInterfaceIP ** String`Example: 192.XX.XX.1`

Private IPv4 address of the endpoint network interface.

If undergoing seamless service resource replacement, this represents the IPv4 address of the endpoint network interface connected to the service resource being replaced.

**NetworkInterfaceIpv6 ** String`Example: 2408::153:3921:XX:XX:7b12:1c5f`

Private IPv6 address of the endpoint network interface.

If undergoing seamless service resource replacement, this represents the IPv6 address of the endpoint network interface connected to the service resource being replaced.

This parameter is not returned if the endpoint only supports IPv4.

**Resource ID ** String`Example: clb-bp1o94dp5i6ea****`

Service resource ID.

If in the process of a seamless service resource replacement, it indicates the service resource being replaced.

**ReplacingResource ** Boolean`Example: true`

Whether a seamless replacement is in progress.

* true

* false

**ReplacedResourceId ** String`Example: clb-w2q642dr1ge5a****`

The new service resource ID.

If the endpoint is not undergoing seamless service resource replacement, this parameter returns empty.

**ReplacedNetworkInterfaceId ** String`Example: eni-273w2q67fwq9s7fap8t1a****`

The ID of the endpoint network interface used to connect to the new service resource.

If the endpoint is not undergoing seamless service resource replacement, this parameter returns empty.

**ReplacedNetworkInterfaceIp ** String`Example: 192.XX.XX.1`

The IPv4 address of the endpoint network interface used to connect to the new service resource.

If the endpoint is not undergoing seamless service resource replacement, this parameter returns empty.

**ReplacedNetworkInterfaceIpv6 ** String`Example: 192.XX.XX.1`

The IPv6 address of the endpoint network interface used to connect to the new service resource.

If the endpoint is not undergoing seamless service resource replacement, this parameter returns empty.

**ResourceZoneIds ** String[]

**CreationTime ** String`Example: 2021-04-09T08:36:47+08:00`

The creation time of the endpoint connection.

**UpdateTime ** String`Example: 2021-04-09T08:36:47+08:00`

The last operation time of the endpoint connection.

**EndpointRegion ** String

## Request examples

```json
GET /?Action=DescribeVpcEndpointConnections&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&ServiceId=epsvc-2fe630gurkl37k5gfuy33**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpcEndpointConnections",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "EndpointConnections": [
            {
                "Bps": 1000,
                "Zones": [
                    {
                        "ZoneId": "cn-guangzhou-a",
                        "SubnetId": "subnet-2744ts087kglc7fap8tu6****",
                        "ResourceId": "clb-bp1o94dp5i6ea****",
                        "ZoneDomain": "ep-273yuq6q7bgn47fap8squ****.cn-guangzhou-a.epsvc-273yuqembrojk7fap8sbf****.cn-guangzhou.privatelink.volces.com",
                        "ZoneStatus": "Connected",
                        "ReplacingResource": true,
                        "NetworkInterfaceIP": "192.XX.XX.1",
                        "NetworkInterfaceId": "eni-273w2q67fwq9s7fap8t1a****",
                        "ReplacedResourceId": "clb-w2q642dr1ge5a****",
                        "NetworkInterfaceIpv6": "2408::153:3921:XX:XX:7b12:1c5f",
                        "ReplacedNetworkInterfaceId": "eni-273w2q67fwq9s7fap8t1a****",
                        "ReplacedNetworkInterfaceIp": "192.XX.XX.1",
                        "ReplacedNetworkInterfaceIpv6": "192.XX.XX.1"
                    }
                ],
                "ServiceId": "epsvc-2fe630gurkl37k5gfuy33****",
                "EndpointId": "ep-273yuq6q7bgn47fap8squ****",
                "UpdateTime": "2021-04-09T08:36:47+08:00",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "EndpointVpcId": "vpc-2744trcju7sw07fap8u05****",
                "ConnectionStatus": "Connecting",
                "EndpointOwnerAccountId": "21000****"
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

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidParameter.BatchQueryForFuzzySearch |Batch query parameters and precise search parameters are passed in at the same time. |Batch query parameters and exact search parameters cannot be passed simultaneously. |
|400 |LimitExceed.EndpointNumber |You've reached the limit on the number of endpoints that you can operate. |You have reached the maximum number of endpoints that can be queried in a single request. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
