---
title: "DescribeIpv6AddressBandwidthAttributes - Querying details of a specified IPv6 Internet bandwidth"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6AddressBandwidthAttributes"
---

Call the DescribeIpv6AddressBandwidthAttributes API to query the detailed information of a specified IPv6 Internet bandwidth.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|IPO4Zx">必选</span> `Example: DescribeIpv6AddressBandwidthAttributes`

The action to perform. Value: **DescribeIpv6AddressBandwidthAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|gONGHB">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**AllocationId ** <span data-label="purple">String </span><span data-api-tag="require|OrBH6G">必选</span> `Example: eip-2zaiwb7ujxscd****`

The ID of the IPv6 Internet bandwidth.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



**Ipv6GatewayId ** <span data-label="purple">String </span>`Example: ipv6gw-hp3y0l3ln89j8cdvf****`

The ID of the IPv6 Gateway.



**IsBlocked ** <span data-label="purple">Boolean </span>`Example: true`

Describe whether the instance is blocked.


* true: Yes.

* false: No.



**AllocationId ** <span data-label="purple">String </span>`Example: eip-2zaiwb7ujxscd****`

The ID of the IPv6 Internet bandwidth.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2019-04-29T01:37:38+08:00`

The time when the IPv6 Internet bandwidth is last updated.



**CreationTime ** <span data-label="purple">String </span>`Example: 2019-04-29T01:37:38+08:00`

The time when the IPv6 Internet bandwidth is enabled.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2021-05-07 23:23:23`

The time when IPv6 Internet bandwidth is suspended due to overdue payment.



**DeleteTime ** <span data-label="purple">String </span>`Example: 2021-05-07 23:23:23`

The time when the IPv6 Internet bandwidth is deleted.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 5`

The bandwidth cap of the IPv6 Internet bandwidth.



**BandwidthPackageId ** <span data-label="purple">String </span>`Example: bwp-2zeo05qre24nhrqpy****`

The ID of the IPv6 Bandwidth Package.



**ISP ** <span data-label="purple">String </span>`Example: BGP`

The ISP of the IPv6 Internet bandwidth.


* BGP (Multi\-ISP).



**InstanceId ** <span data-label="purple">String </span>`Example: i-3tm18xqalm4e8i4q****`

The instance ID associated with the IPv6 Internet bandwidth.



**InstanceType ** <span data-label="purple">String </span>`Example: EcsInstance`

The instance type associated with IPv6 Internet bandwidth.


* EcsInstance: Elastic Compute Service (ECS) instance.



**Ipv6Address ** <span data-label="purple">String </span>`Example: 2408::153:3921:XX:XX:7b12:1c5f`

The IPv6 address.



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

Describe whether the IPv6 Internet bandwidth is locked.


* Normal

* FinancialLocked: Being locked.



**NetworkType ** <span data-label="purple">String </span>`Example: Public`

The communication type of the IPv6 address.


* Private: Private network communication.

* Public: Public network communication.



**LockReason ** <span data-label="purple">String </span>`Example: Financial`

The reason for the IPv6 Internet bandwidth being locked.

This parameter is returned only when the IPv6 Internet bandwidth is in the `FinancialLocked` status.


* Financial: Being locked due to arrears.

* Security: Being locked due to security.



**BillingType ** <span data-label="purple">Integer </span>`Example: 3`

The metering method of the IPv6 Internet bandwidth.


* 2: Pay\-by\-bandwidth\-cap.

* 3: Pay\-by\-data\-transfer.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the IPv6 Internet bandwidth.


* Creating

* Available



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the IPv6 Internet bandwidth.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeIpv6AddressBandwidthAttributes&Version=2020-04-01&AllocationId=eip-2zaiwb7ujxscd**** HTTP/1.1
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
        "Action": "DescribeIpv6AddressBandwidthAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllocationId": "eip-2zaiwb7ujxscd****",
        "Bandwidth": 5,
        "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
        "BillingType": 3,
        "BusinessStatus": "Normal",
        "CreationTime": "2019-04-29T01:37:38+08:00",
        "DeleteTime": "2021-05-07 23:23:23",
        "ISP": "BGP",
        "InstanceId": "i-3tm18xqalm4e8i4q****",
        "InstanceType": "EcsInstance",
        "Ipv6Address": "2408::153:3921:XX:XX:7b12:1c5f",
        "Ipv6GatewayId": "ipv6gw-hp3y0l3ln89j8cdvf****",
        "IsBlocked": true,
        "LockReason": "Financial",
        "NetworkType": "Public",
        "OverdueTime": "2021-05-07 23:23:23",
        "RequestId": "2021062415303301022514515207C4****",
        "SpecificEgress": "",
        "Status": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2019-04-29T01:37:38+08:00"
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
|404 |InvalidIpv6.AddressIpNotFound |The specified IPv6 address can not be found |The specified IPv6 address was not found. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
