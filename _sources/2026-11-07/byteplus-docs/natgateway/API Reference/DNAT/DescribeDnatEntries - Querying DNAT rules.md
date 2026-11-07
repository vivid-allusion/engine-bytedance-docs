---
title: "DescribeDnatEntries - Querying DNAT rules"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeDnatEntries"
---

Call DescribeDnatEntries to query DNAT rules that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the system will query based on these parameters and return all DNAT rules that meet all the specified conditions. An empty list is returned if no qualified DNAT rules exist.

* If no optional parameters are provided, the system will query based on the currently logged\-in account, and return all DNAT rules under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeDnatEntries&groupName=DNAT%E8%A7%84%E5%88%99&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|60GQRV">必选</span> `Example: DescribeDnatEntries`

The action that you want to perform. Value: DescribeDnatEntries.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|KfukKb">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ExternalPort ** <span data-label="purple">string </span>`optional` `Example: 34`

The port or port range for receiving external requests.



**ExternalIp ** <span data-label="purple">string </span>`optional` `Example: 12.XX.XX.34`

The IP address used by the NAT gateway for network address translation.


* If the NAT gateway is an Internet NAT gateway, specify its associated elastic IP address (EIP).

* If the NAT gateway is a VPC NAT gateway, provide its NAT IP address.



**DnatEntryName ** <span data-label="purple">string </span>`optional` `Example: dnat-01`

The name of the DNAT rule.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 20`

The number of entries on each page. Maximum: 100. Default: 20.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**InternalIp ** <span data-label="purple">string </span>`optional` `Example: 192.XX.XX.88`

The private IP address of the Elastic Compute Service (ECS) instance.



**Protocol ** <span data-label="purple">string </span>`optional` `Example: tcp`

Protocol type.


* tcp: Forward TCP messages.

* udp: Forward UDP messages.



**InternalPort ** <span data-label="purple">string </span>`optional` `Example: 12`

The port or port range of the private IP address in the Elastic Compute Service (ECS) instance.



**PortType ** <span data-label="purple">string </span>`optional` `Example: specified`

The port type of the DNAT rule.


* specified: The specified port.

* any: Any port. That is, DNAT IP mapping.



**NatGatewayId ** <span data-label="purple">string </span>`optional` `Example: ngw-2feq5xhimd88w59gp686****`

ID of the NAT gateway.



**DnatEntryIds.N ** <span data-label="purple">string[] </span>`optional` `Example: dnat-342abc3bc3****`

ID of the DNAT rule.


* N represents the sequence number of a DNAT rule ID. You can specify a maximum of 20 IDs per call.

* Separate multiple IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DnatEntries ** <span data-label="purple">object[] </span>`Example: -`

The details of the DNAT rule.


**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-2feq5xhimd88w59gp686****`

The ID of the NAT gateway to which the DNAT rule belongs.



**DnatEntryId ** <span data-label="purple">string </span>`Example: dnat-342abc3bc3****`

The ID of the DNAT rule.



**DnatEntryName ** <span data-label="purple">string </span>`Example: dnat-01`

The name of the DNAT rule.



**Protocol ** <span data-label="purple">string </span>`Example: tcp`

Protocol type.


* tcp: Forward TCP messages.

* udp: Forward UDP messages.



**Status ** <span data-label="purple">string </span>`Example: Available`

The status of the DNAT rule.


* Creating

* Deleting

* Available



**InternalIp ** <span data-label="purple">string </span>`Example: 192.XX.XX.88`

The private IP address of the Elastic Compute Service (ECS) instance.



**InternalPort ** <span data-label="purple">string </span>`Example: 12`

The port or port range of the private IP address in the ECS instance.



**ExternalIp ** <span data-label="purple">string </span>`Example: 12.XX.XX.34`

The IP address used by the NAT gateway for network address translation.



**ExternalPort ** <span data-label="purple">string </span>`Example: 34`

The port or port range for receiving external requests.



**PortType ** <span data-label="purple">string </span>`Example: specified`

The port type of the DNAT rule.




**PageSize ** <span data-label="purple">integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">integer </span>`Example: 33`

The total number of DNAT rules that meet the conditions.



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeDnatEntries&Version=2020-04-01&NatGatewayId=ngw-2feq5xhimd88w59gp686****&DnatEntryIds.1=dnat-342abc3bc3**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
ServiceName: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeDnatEntries",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 20,
        "DnatEntries": [
            {
                "NatGatewayId": "ngw-2feq5xhimd88w59gp686****",
                "DnatEntryId": "dnat-342abc3bc3****",
                "DnatEntryName": "dnat-01",
                "Protocol": "tcp",
                "InternalIp": "192.XX.XX.88",
                "InternalPort": "12",
                "ExternalIp": "12.XX.XX.34",
                "ExternalPort": "34",
                "Status": "Available"
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
|400 |LimitExceeded.DnatEntryId |You've reached the limit on the number of DNAT entry IDs that you can describe. |You have reached the maximum number of DNAT rule IDs that can be queried. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
