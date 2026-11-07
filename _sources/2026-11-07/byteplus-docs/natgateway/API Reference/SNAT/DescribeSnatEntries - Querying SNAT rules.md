---
title: "DescribeSnatEntries - Querying SNAT rules"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeSnatEntries"
---

Call the DescribeSnatEntries API to query SNAT rules that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

If multiple request parameters are provided, the system will query based on these parameters and return all SNAT rules that meet all the specified conditions. An empty list is returned if no qualified SNAT rules exist.

If no optional parameters are provided, the system will query based on the currently logged\-in account, and return all SNAT rules under that account.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSnatEntries&groupName=SNAT%E8%A7%84%E5%88%99&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|0p3zl5">必选</span> `Example: DescribeSnatEntries`

The action that you want to perform. Value: DescribeSnatEntries.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|yKn1Fu">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**SubnetId ** <span data-label="purple">string </span>`optional` `Example: subnet-9f33a3bdc24****`

The ID of the subnet associated with the SNAT rule.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.



**EipId ** <span data-label="purple">string </span>`optional` `Example: eip-2a3d4c5a837****`

The ID of the EIP used by the SNAT rule. Separate multiple EIP IDs with commas (,).

You can call [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) to query the EIP ID.


* Returns all of SNAT rules associated with this EIP if a single EIP ID is specified.

* Returns SNAT rules that are associated with any of these EIPs if multiple EIP IDs are specified.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid range: 1–100. Default: 20.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**SourceCidr ** <span data-label="purple">string </span>`optional` `Example: 192.XX.XX.0/24`

The CIDR block associated with the SNAT rule.



**SnatEntryName ** <span data-label="purple">string </span>`optional` `Example: snat-01`

Name of the SNAT rule.



**NatIpId ** <span data-label="purple">string </span>`optional` `Example: vpcnatip-gw8y7q3cpk3fggs8****`

The ID of the NAT IP address used by the SNAT rule.

You can call the [DescribeNatIps](https://docs.byteplus.com/en/docs/natgateway/DescribeNatIps) API to query the NAT IP ID.



**NatGatewayId ** <span data-label="purple">string </span>`optional` `Example: ngw-2fedgzyvtzaio59gp675l****`

ID of the NAT gateway.

You can call the [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways) API to query the ID of a NAT gateway.



**SnatEntryIds.N** <span data-label="purple">string[]</span> `optional` `Example: snat-2fedi22b12iv459gp68****`

ID of the SNAT rule.


* N represents the sequence number of a SNAT rule ID. You can call a maximum of 20 IDs in a single request.

* Separate multiple IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The current page number.



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple">integer </span>`Example: 33`

The total number of SNAT rules that meet the conditions.



**SnatEntries ** <span data-label="purple">object[] </span>`Example: -`

The details of the SNAT rule.


**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-2feq5xhimd88w59gp687****`

The ID of the NAT gateway to which the SNAT rule belongs.



**SnatEntryId ** <span data-label="purple">string </span>`Example: snat-2fedhzdlyknb459gp676o****`

ID of the SNAT rule.



**SnatEntryName ** <span data-label="purple">string </span>`Example: snat-02`

Name of the SNAT rule.



**SubnetId ** <span data-label="purple">string </span>`Example: subnet-2fe1vklp295a859gp6766****`

ID of the subnet associated with the SNAT rule.



**SourceCidr ** <span data-label="purple">string </span>`Example: 192.XX.XX.0/24`

The CIDR block associated with the SNAT rule.



**EipId ** <span data-label="purple">string </span>`Example: eip-2feaac9wtccn459gp67qe****`

The ID of the elastic IP address (EIP) used by the SNAT rule.


* Returns the ID of a single EIP.

* Returns the IDs of multiple EIPs.



**EipAddress ** <span data-label="purple">string </span>`Example: 180.XX.XX.69`

The address of EIP used by the SNAT rule.


* Returns the address of a single EIP.

* Returns the addresses of multiple EIPs.



**Status ** <span data-label="purple">string </span>`Example: Available`

The status of the SNAT rule.


* Available

* Creating

* Deleting



**NatIpId ** <span data-label="purple">string </span>`Example: vpcnatip-gw8y7q3cpk3fggs8****`

The ID of the NAT IP address used by the VPC NAT gateway.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeSnatEntries&Version=2020-04-01&SnatEntryIds.1=snat-2fedi22b12iv459gp68****&NatGatewayId=ngw-2fedgzyvtzaio59gp675l**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeSnatEntries",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 2,
        "PageNumber": 1,
        "PageSize": 20,
        "SnatEntries": [
            {
               "NatGatewayId": "ngw-2feq5xhimd88w59gp686****",
                "SnatEntryId": "snat-2fedi22b12iv459gp68****",
                "SnatEntryName": "snat-01",
                "SubnetId": "subnet-2fe1vf6cq44cg59gp687k****",
                "SourceCidr":"192.XX.XX.0/24",
                "EipId": "eip-ac321ea98****,eip-ac321ea98****",
                "EipAddress": "180.XX.XX.69,180.XX.XX.68",
                "Status": "Available",
                "NatIpId": ""
            },
            {
                "NatGatewayId": "ngw-2feq5xhimd88w59gp687****"
                "SnatEntryId": "snat-2fedhzdlyknb459gp676o****",
                "SnatEntryName": "snat-02",
                "SubnetId": "subnet-2fe1vklp295a859gp6766****",
                "SourceCidr":" ",
                "EipId": "eip-2feaac9wtccn459gp67qe****",
                "EipAddress": "180.XX.XX.69",
                "Status": "Available",
                "NatIpId": "vpcnatip-gw8y7q3cpk3fggs8****"
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
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.SnatEntryId |You've reached the limit on the number of SNAT entry IDs that you can describe. |You have reached the maximum IDs of SNAT rule that can be queried. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
