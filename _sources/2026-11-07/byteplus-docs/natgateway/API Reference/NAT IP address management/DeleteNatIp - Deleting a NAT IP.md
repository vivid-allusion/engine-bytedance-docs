---
title: "DeleteNatIp - Deleting a NAT IP"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DeleteNatIp"
---

Call the DeleteNatIp API to delete a NAT IP address.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The NAT IP is not attached to any SNAT or DNAT rules. If attached, delete the SNAT or DNAT rules first.

* Default NAT IPs cannot be deleted.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteNatIp&groupName=%E7%A7%81%E7%BD%91NAT%E5%9C%B0%E5%9D%80&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|bWkHMy">必选</span> `Example: DeleteNatIp`

The action that you want to perform. Value: DeleteNatIp.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|0ROZnP">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**NatIpId ** <span data-label="purple">string </span><span data-api-tag="require|eHAi7w">必选</span> `Example: vpcnatip-1wzww8z77uxog8ny6hgb0****`

The ID of the NAT IP address.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteNatIp&Version=2020-04-01&NatIpId=vpcnatip-gw8y7q3cpk3fggs87**** HTTP/1.1
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
        "Action": "DeleteNatIp",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidNatIp.Default |The specified default nat ip can't be deleted. |The specified NAT IP cannot be deleted because it is a default NAT IP. |
|400 |InvalidNatIp.InUse |The specified nat ip is in use, and can't be deleted. |The specified NAT IP is in use and cannot be deleted. |
|404 |InvalidNatIp.NotFound |The specified nat ip does not exist. |The specified NAT IP does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
