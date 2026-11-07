---
title: "ModifyNatIpAttributes - Modifying a NAT IP"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/ModifyNatIpAttributes"
---

Call the ModifyNatIpAttributes API to modify the name and description of a NAT IP address.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyNatIpAttributes&groupName=%E7%A7%81%E7%BD%91NAT%E5%9C%B0%E5%9D%80&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|kT5pqB">必选</span> `Example: ModifyNatIpAttributes`

The action that you want to perform. Value: ModifyNatIpAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|YzLIHa">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**NAT IP name ** <span data-label="purple">string </span>`optional` `Example: nat_ip_1`

Name of the NAT IP address.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).



**NatIpDescription ** <span data-label="purple">string </span>`optional` `Example: natip-1`

Description of the NAT IP.


* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



**NatIpId ** <span data-label="purple">string </span><span data-api-tag="require|NvjVsY">必选</span> `Example: vpcnatip-1wzww8z77uxog8ny6hgb0****`

ID of the NAT IP address.



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
GET /?Action=ModifyNatIpAttributes&Version=2020-04-01&NatIpId=vpcnatip-gw8y7q3cpk3fggs87****&NatIpName=nat_ip_1 HTTP/1.1
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
        "Action": "ModifyNatIpAttributes",
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
|400 |InvalidDescription.Malformed |The specified description is malformed.Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|404 |InvalidNatIp.NotFound |The specified nat ip does not exist. |The specified NAT IP does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
