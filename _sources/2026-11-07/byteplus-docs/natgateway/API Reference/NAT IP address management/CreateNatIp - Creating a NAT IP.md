---
title: "CreateNatIp - Creating a NAT IP"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/CreateNatIp"
---

Call the CreateNatIp API to add a Network Address Translation (NAT) IP address.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The subnet where the VPC NAT gateway is located has available private IP addresses.

* The number of NAT IPs added to the VPC NAT gateway has not reached the quota.

* The current account is not in arrears or has been in arrears for less than 2 hours.​


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateNatIp&groupName=%E7%A7%81%E7%BD%91NAT%E5%9C%B0%E5%9D%80&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|BMqMpj">必选</span> `Example: CreateNatIp`

The action that you want to perform. Value: CreateNatIp.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|xg0GYO">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**NAT IP name ** <span data-label="purple">string </span>`optional` `Example: nat_ip_1`

Name of the NAT IP address.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, this parameter defaults to the ID of the NAT IP.



**NatIpDescription ** <span data-label="purple">string </span>`optional` `Example: natip-1`

Description of the NAT IP.


* Must be 0 to 255 characters.

* If left blank, this parameter defaults to an empty string.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



**NatIp ** <span data-label="purple">string </span>`optional` `Example: 192.168.XX.34`

Address of the NAT IP.

If left blank, the system randomly assigns an available IP from the VPC NAT gateway subnet.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|WpQo6D">必选</span> `Example: ngw-2feq5xhimd88w59gp686****`

The ID of the VPC NAT gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**NatIpId ** <span data-label="purple">string </span>`Example: vpcnatip-gw8y7q3cpk3fggs8****`

The ID of the NAT IP address.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=CreateNatIp&Version=2020-04-01&NatGatewayId=ngw-2feq5xhimd88w59gp686****&NatIp=192.168.XX.34 HTTP/1.1
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
        "Action": "CreateNatIp",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "NatIpId": "vpcnatip-gw8y7q3cpk3fggs8****"
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
|400 |InvalidIPAddress.Malformed |The specified IP address is malformed. |The specified IP is invalid. |
|400 |InvalidNatGateway.NatIpNotSupported |The specified NAT gateway does not support creating nat ip. |The specified NAT gateway instance does not support creating NAT IPs. |
|400 |QuotaExceeded.NatIp |NAT IPs number of the cidr exceeded quota. |You have reached the maximum number of NAT IP addresses that you can create in a CIDR block. |
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed.Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidNatIp.AssignPrivateIpAddressFailed |The specified nat gateway assign private ip address failed. |Failed to assign a private IP address. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |InvalidNatGateway.Expired |The specified NAT gateway has expired. |The specified NAT gateway is expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
