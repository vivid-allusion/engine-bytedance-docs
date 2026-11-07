---
title: "DescribeNatIps - Querying NAT IPs"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeNatIps"
---

Call the DescribeNatIps API to query N​​etwork ​​A​​ddress ​​T​​ranslation (NAT) IP addresses that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the system will query based on these parameters and return all NAT IP addresses that meet all the specified conditions. An empty list is returned if no qualified NAT IP addresses exist.

* If no optional parameters are provided, the system will query based on the currently logged\-in account, and return all NAT IPs under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeNatIps&groupName=%E7%A7%81%E7%BD%91NAT%E5%9C%B0%E5%9D%80&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|mHgdsX">必选</span> `Example: DescribeNatIps`

The action that you want to perform. Value: DescribeNatIps.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|QrGaEy">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**NAT IP name ** <span data-label="purple">string </span>`optional` `Example: nat_ip_1`

Name of the NAT IP address.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1 to 100. Default: 20.



**NatIpIds.N ** <span data-label="purple">string[] </span>`optional` `Example: vpcnatip-3a4b****`

ID of the NAT IP address.


* N represents the sequence number of a NAT IP ID. You can specify a maximum of 100 IDs per call.

* Separate multiple IDs with ampersands (&).



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|rnjpak">必选</span> `Example: ngw-2feq5xhimd88w59gp686****`

The ID of the VPC NAT gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

Number of entries per page in the current pagination.



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**NatIps ** <span data-label="purple">object[] </span>`Example: -`

Details of the NAT IP.


**NatIpId ** <span data-label="purple">string </span>`Example: vpcnatip-gw8y7q3cpk3fggs87****`

The ID of the NAT IP address.



**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-2feq5xhimd88w59gp686****`

The ID of the VPC NAT gateway.



**NatIpName ** <span data-label="purple">string </span>`Example: nat_ip_1`

Name of the NAT IP address.



**NatIpDescription ** <span data-label="purple">string </span>`Example: natip-1`

Description of the NAT IP address.



**NatIp ** <span data-label="purple">string </span>`Example: 192.168.XX.34`

Address of the NAT IP.



**IsDefault ** <span data-label="purple">boolean </span>`Example: true`

Describe whether the NAT IP address is the default one.


* true: Yes.

* false: No.



**Status ** <span data-label="purple">string </span>`Example: Creating`

The status of the NAT IP address.


* Creating

* Available

* Deleting

* Deleted



**UsingStatus ** <span data-label="purple">string </span>`Example: Idle`

The usage status of the NAT IP address.


* Idle: Not in use.

* UsedBySnat: Occupied by an SNAT rule.

* UsedByDnat: Occupied by a DNAT rule.

* UsedByNat: Occupied by NAT.




**TotalCount ** <span data-label="purple">integer </span>`Example: 2`

The total number of NAT IP addresses that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeNatIps&Version=2020-04-01&NatGatewayId=ngw-2feq5xhimd88w59gp686**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
ServiceName: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeNatIps",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
      "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 2,
        "PageNumber": 1,
        "PageSize": 20,
        "NatIps": [
            {
                "NatIpId": "vpcnatip-gw8y7q3cpk3fggs87****",
                "NatGatewayId": "ngw-2feq5xhimd88w59gp686****",
                "NatIpName": "nat_ip_1",
                "NatIpDescription": "natip-1",
                "NatIp":"192.168.XX.34",
                "IsDefault": true,
                 "UsingStatus":"Idle"
            },
            {
                "NatIpId": "vpcnatip-gw8y7q3cpk3fg666****",
                "NatGatewayId": "ngw-2feq5xhimd88w59gp686****",
                "NatIpName": "nat_ip_2",
                "NatIpDescription": "natip-2",
                "NatIp":"192.168.XX.12",
                "IsDefault": false,
                "Status":"Available",
                 "UsingStatus":"UsedBySnat"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.NatIpId |You've reached the limit on the number of nat ip IDs that you can describe. |You have reached the maximum number of NAT IP IDs that you can query. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
