---
title: "DescribeSnatEntryAttributes - Viewing details of a SNAT rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeSnatEntryAttributes"
---

Call the DescribeSnatEntryAttributes API to view the details of a SNAT rule.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSnatEntryAttributes&groupName=SNAT%E8%A7%84%E5%88%99&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|LG3FZk">必选</span> `Example: DescribeSnatEntryAttributes`

The action that you want to perform. Value: DescribeSnatEntryAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ZapBuc">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**SnatEntryId** <span data-label="purple">string</span> <span data-api-tag="require|54n5mF">必选</span>`Example: snat-342abc3bc3****`

ID of the SNAT rule.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**SourceCidr ** <span data-label="purple">string </span>`Example: 192.XX.XX.0/24`

The CIDR block associated with the SNAT rule.



**SubnetId** <span data-label="purple">string</span> `Example: subnet-6o5smt1b9****`

ID of the subnet associated with the SNAT rule.



**SnatEntryName ** <span data-label="purple">string </span>`Example: snat-test`

Name of the SNAT rule.



**SnatEntryId ** <span data-label="purple">string </span>`Example: snat-3fvhk47kf56****`

ID of the SNAT rule.



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-1sm2t10buei****`

The ID of the NAT gateway to which the SNAT rule belongs.



**EipId ** <span data-label="purple">string </span>`Example: eip-12af342dca34****, eip-12af342dca35****`

The ID of the EIP associated with the SNAT rule.



**EipAddress ** <span data-label="purple">string </span>`Example: 180.XX.XX.195,180.XX.XX.196`

The address of the EIP associated with the SNAT rule.



**Status ** <span data-label="purple">string </span>`Example: Available`

The status of the SNAT rule.


* Creating

* Deleting

* Available



**NatIpId ** <span data-label="purple">string </span>`Example: vpcnatip-gw8y7q3cpk3fggs8****`

The ID of the NAT IP address used by the VPC NAT gateway.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeSnatEntryAttributes&Version=2020-04-01&SnatEntryId=snat-2fedi096gdiww59gp680**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeSnatEntryAttributes",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",    
        "NatGatewayId": "ngw-2feq5xhimd88w59gp686****",   
        "SnatEntryId": "snat-2fedi096gdiww59gp680r****",    
        "SnatEntryName": "snat-01",    
        "SubnetId": "subnet-2fe1vf6cq44cg59gp687k****",
        "SourceCidr": "192.XX.XX.0/24",     
        "EipId": "eip-2feq2yc0hcv0g59gp680w****",
        "EipAddress": "180.XX.XX.195",
        "Status": "Available",
        "NatIpId": ""
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|404 |InvalidSnatEntry.NotFound |The specified SNAT entry does not exist. |The specified SNAT rule does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
