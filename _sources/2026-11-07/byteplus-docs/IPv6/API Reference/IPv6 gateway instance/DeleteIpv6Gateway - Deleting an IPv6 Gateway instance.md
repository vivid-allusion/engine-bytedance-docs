---
title: "DeleteIpv6Gateway - Deleting an IPv6 Gateway instance"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/DeleteIpv6Gateway"
---

Call the DeleteIpv6Gateway API to delete a specified IPv6 Gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

The IPv6 Gateway instance has not enabled IPv6 Internet bandwidth for its IPv6 address. This means the Virtual Private Cloud (VPC) associated with the IPv6 Gateway has no IPv6 Internet bandwidth. You can call the [DescribeIpv6AddressBandwidths](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6AddressBandwidths) API to check if the VPC has IPv6 Internet bandwidth. If it does, you can call the [ReleaseIpv6AddressBandwidth](https://docs.byteplus.com/en/docs/IPv6/ReleaseIpv6AddressBandwidth) API to release it.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|tmA5EM">必选</span> `Example: DeleteIpv6Gateway`

The action to perform. Value: **DeleteIpv6Gateway**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|fOaUES">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**Ipv6GatewayId ** <span data-label="purple">String </span><span data-api-tag="require|NIi2D3">必选</span> `Example: ipv6gw-hp3y0l3ln89j8****`

The ID of the IPv6 Gateway to delete.

You can call the [DescribeIpv6Gateways](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6Gateways) API to query the ID of IPv6 Gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DeleteIpv6Gateway&Version=2020-04-01&Ipv6GatewayId=ipv6gw-hp3y0l3ln89j8**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: vpc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteIpv6Gateway",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/IPv6/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DependencyViolation.Ipv6 |Ipv6 address bandwidth is dependent. |The IPv6 Gateway has dependent IPv6 Internet bandwidth resources. |
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidIpv6Gateway.InvalidStatus |The specified IPv6Gateway is not in the correct status for the request. |The specified IPv6 Gateway cannot respond to this request due to its status. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC cannot respond to this request due to its status. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|404 |InvalidIpv6Gateway.NotFound |The specified Ipv6Gateway does not exist. |The specified IPv6 Gateway does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |InvalidIpv6Gateway.DependenceRouteTableExist |The specified Ipv6Gateway has a dependency on route table. |The specified IPv6 Gateway has a dependent route table. The request cannot be processed. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
