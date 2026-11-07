---
title: "DescribeDnatEntryAttributes - Viewing details of a DNAT rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeDnatEntryAttributes"
---

Call the DescribeDnatEntryAttributes API to view the details of a DNAT rule.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the system will query based on these parameters and return all DNAT rules that meet all the specified conditions. An empty list is returned if no qualified DNAT rules exist.

* If no optional parameters are provided, the system will query based on the currently logged\-in account, and return all DNAT rules under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeDnatEntryAttributes&groupName=DNAT%E8%A7%84%E5%88%99&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|jK2zco">必选</span> `Example: DescribeDnatEntryAttributes`

The action that you want to perform. Value: DescribeDnatEntryAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|MkKFSg">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**DnatEntryId ** <span data-label="purple">string </span><span data-api-tag="require|94Pq50">必选</span> `Example: dnat-342abc3bc3****`

ID of the DNAT rule.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ExternalPort ** <span data-label="purple">string </span>`Example: 34`

The port or port range for receiving external requests from the internet.



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-2feq5xhimd88w59gp686****`

The ID of the NAT gateway to which the DNAT rule belongs.



**DnatEntryId ** <span data-label="purple">string </span>`Example: dnat-342abc3bc3****`

The ID of the DNAT rule.



**DnatEntryName ** <span data-label="purple">string </span>`Example: dnat-01`

The name of the DNAT rule.



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


* If the NAT gateway is an Internet NAT gateway, specify its associated elastic IP address (EIP).

* If the NAT gateway is a VPC NAT gateway, provide its NAT IP address.



**Protocol ** <span data-label="purple">string </span>`Example: tcp`

Protocol type.


* tcp: Forward TCP messages.

* udp: Forward UDP messages.



**PortType ** <span data-label="purple">string </span>`Example: specified`

The port type of the DNAT rule.


* specified: The specified port.

* any: Any port. That is, IP mapping.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeDnatEntryAttributes&Version=2020-04-01&DnatEntryId=dnat-342abc3bc3**** HTTP/1.1
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
        "Action": "DescribeDnatEntryAttributes",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "NatGatewayId": "ngw-2feq5xhimd88w59gp686****",
        "DnatEntryId": "dnat-342abc3bc3****",
        "PortType": "specified",
        "Protocol": "tcp",
        "InternalIp": "192.XX.XX.88",
        "InternalPort": "12",
        "ExternalIp": "12.XX.XX.34",
        "ExternalPort": "34",
        "Status": "Available"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|404 |InvalidDnatEntry.NotFound |The specified DNAT entry does not exist. |The specified DNAT rule does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
