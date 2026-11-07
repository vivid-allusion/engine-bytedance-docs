---
title: "ListNatGatewayAvailableZones - Querying NAT gateway availability zones"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/ListNatGatewayAvailableZones"
---

Call the ListNatGatewayAvailableZones API to query the availability zones where NAT gateway resources are deployed in the current region.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ListNatGatewayAvailableZones&groupName=NAT%E7%BD%91%E5%85%B3&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|LmFehi">必选</span> `Example: ListNatGatewayAvailableZones`

The action that you want to perform. Value: ListNatGatewayAvailableZones.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|4lFDMp">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**Product** <span data-label="purple">string</span> `optional` `Example: INTERNET_NAT`

The type of the NAT gateway.


* VPC_NAT: VPC NAT Gateway.

* INTERNET_NAT (default): Internet NAT Gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Zones ** <span data-label="purple">object[] </span>`Example: -`

Details of the NAT gateway.


**ZoneId ** <span data-label="purple">string </span>`Example: cn-beijing-a`

The ID of the availability zone where the NAT gateway cluster is deployed in the current region.




**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ListNatGatewayAvailableZones&Version=2020-04-01 HTTP/1.1
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
        "Action": "ListNatGatewayAvailableZones",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"，
        "Zones": [
            {
                "ZoneId": "cn-beijing-a"
            },
            {
                 "ZoneId": "cn-beijing-b"
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
|400 |InvalidProduct.Malformed |The specified product of NAT is malformed. |The specified NAT product is invalid. |
|404 |InvalidZoneId.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
