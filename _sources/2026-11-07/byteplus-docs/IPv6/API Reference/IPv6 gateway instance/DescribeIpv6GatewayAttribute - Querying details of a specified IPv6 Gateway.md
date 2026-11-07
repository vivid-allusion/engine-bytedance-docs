---
title: "DescribeIpv6GatewayAttribute - Querying details of a specified IPv6 Gateway"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6GatewayAttribute"
---

Call the DescribeIpv6GatewayAttribute API to view the details of a specified IPv6 Gateway instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|oJqb6q">必选</span> `Example: DescribeIpv6GatewayAttribute`

The action to perform. Value: **DescribeIpv6GatewayAttribute**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|lAatli">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**Ipv6GatewayId ** <span data-label="purple">String </span><span data-api-tag="require|OaoUs3">必选</span> `Example: ipv6gw-hp3y0l3ln89j8****`

The ID of the IPv6 Gateway instance.

You can call the [DescribeIpv6Gateways](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6Gateways) API to query the ID of IPv6 Gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



**Name ** <span data-label="purple">String </span>`Example: ipv6GW-01`

The name of the IPv6 Gateway instance.



**CreationTime ** <span data-label="purple">String </span>`Example: 2017-12-05T22:40:00+08:00`

The time when the IPv6 Gateway instance is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2017-12-05T22:40:00+08:00`

The time when the IPv6 Gateway instance is modified.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the IPv6 gateway instance. Values:


* Creating

* Deleting

* Available



**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp67acfmxazb4p****`

The VPC ID associated with the IPv6 gateway instance.



**Description ** <span data-label="purple">String </span>`Example: descriptionforIPv6GW`

The description of the IPv6 Gateway instance.



**Ipv6GatewayId ** <span data-label="purple">String </span>`Example: ipv6gw-hp3rwmtmfhgis****`

The ID of the IPv6 Gateway instance.



**RouteTableId ** <span data-label="purple">String </span>`Example: rt-3tbe3o0tn849ovie****`

The route table ID associated with the IPv6 Gateway instance.



**ProjectName ** <span data-label="purple">String </span>`Example: Project_1`

The name of the project to which the IPv6 Gateway belongs.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeIpv6GatewayAttribute&Version=2020-04-01&Ipv6GatewayId=ipv6gw-hp3y0l3ln89j8**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: vpc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeIpv6GatewayAttribute",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "CreationTime": "2017-12-05T22:40:00+08:00",
        "Description": "descriptionforIPv6GW",
        "Ipv6GatewayId": "ipv6gw-hp3rwmtmfhgis****",
        "Name": "ipv6GW-01",
        "ProjectName": "Project_1",
        "RequestId": "2021062415303301022514515207C4****",
        "RouteTableId": "rt-3tbe3o0tn849ovie****",
        "Status": "Available",
        "UpdateTime": "2017-12-05T22:40:00+08:00",
        "VpcId": "vpc-bp67acfmxazb4p****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/IPv6/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain the required parameter. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
