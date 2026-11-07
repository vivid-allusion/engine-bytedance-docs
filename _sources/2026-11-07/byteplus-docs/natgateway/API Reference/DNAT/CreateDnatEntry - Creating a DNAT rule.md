---
title: "CreateDnatEntry - Creating a DNAT rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/CreateDnatEntry"
---

Call the CreateDnatEntry API to create a Destination Network Address Translation (DNAT) rule.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

You can create a maximum of 100 DNAT rules for a single NAT gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateDnatEntry&groupName=DNAT%E8%A7%84%E5%88%99&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|rA5nnD">必选</span> `Example: CreateDnatEntry`

The action that you want to perform. Value: CreateDnatEntry.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|LZpo8Q">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**Protocol ** <span data-label="purple">string </span><span data-api-tag="require|DvHskL">必选</span> `Example: tcp`

Protocol type. Values:


* When PortType is set to "specified", the value can be:

   * tcp: Forward TCP messages.

   * udp: Forward UDP messages.

* When PortType is set to "any", this parameter must be set to "any", indicating that it forwards traffic for any protocol.​forward packets of any protocols.



**DnatEntryName ** <span data-label="purple">string </span>`optional` `Example: dnat-01`

The name of the DNAT rule. Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-). Must be 1 to 128 characters. If left blank, it defaults to the DNAT rule ID.



**ExternalIp ** <span data-label="purple">string </span><span data-api-tag="require|YGwCPs">必选</span> `Example: 12.XX.XX.34`

The IP address used by the NAT gateway for network address translation.


* If the NAT gateway is an Internet NAT gateway, specify its associated elastic IP address (EIP).

* If the NAT gateway is a VPC NAT gateway, provide its NAT IP address.



**InternalIp ** <span data-label="purple">string </span><span data-api-tag="require|q8GmBD">必选</span> `Example: 192.XX.XX.88`

The private IP address of the Elastic Compute Service (ECS) instance.



**InternalPort ** <span data-label="purple">string </span><span data-api-tag="require|Rf7gvi">必选</span> `Example: 12`

The port or port range of the private IP address in the Elastic Compute Service (ECS) instance.


* When PortType is set to "any", this parameter must be set to "any", indicating all ports.

* When PortType is set to "specified":

   * The valid range is 1 to 65535.

   * Use a hyphen (\-) to specify a port range, e.g., 20\-25.



**ExternalPort ** <span data-label="purple">string </span><span data-api-tag="require|1Px2ec">必选</span> `Example: 34`

The port or port range for receiving external requests.


* When PortType is set to "any", this parameter must be set to "any", indicating all ports.

* When PortType is set to "specified":

   * The valid range is 1 to 65535.

   * ​​If InternalPort is set to a port range, ExternalPort must also be set to a port range of equal length. Use a hyphen (\-) to specify the port range. For example, if setting InternalPort to 20\-25, you must also set ExternalPort to 30\-35.



**PortType ** <span data-label="purple">string </span>`optional` `Example: specified`

The port type of the DNAT rule.


* specified (default): The specified port.

* any: Any port. That is, DNAT IP mapping.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|L965yA">必选</span> `Example: ngw-2feq5xhimd88w59gp686****`

The ID of the NAT gateway to which the DNAT rule belongs. You can call the DescribeNatGateways API to query the ID of a NAT gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DnatEntryId ** <span data-label="purple">string </span>`Example: dnat-342abc3bc3****`

The ID of the DNAT rule.



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=CreateDnatEntry&Version=2020-04-01&NatGatewayId=ngw-2feq5xhimd88w59gp686****&Protocol=tcp&InternalIp=192.XX.XX.88&InternalPort=12&ExternalIp=12.XX.XX.34&ExternalPort=34 HTTP/1.1
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
        "Action": "CreateDnatEntry",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "DnatEntryId": "dnat-342abc3bc3****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. The specified elastic ip is in freeze. |The specified EIP or Virtual Private Cloud (VPC) cannot respond to this request due to its status. The current EIP is frozen. |
|400 |QuotaExceeded.DnatEntry |You've reached the limit on the number of DnatEntry that you can create. |You have reached the maximum number of DNAT rules that you can create. |
|400 |InvalidProtocol.Malformed |The specified protocol is malformed. |The specified protocol is invalid. |
|400 |InvalidPort.Malformed |The specified port is malformed. Ensure that you've specified the port in right form and internal port and external port must have the same number of ports. |The specified port is invalid. Ensure the port or port range is in the correct format, and the internal and external port ranges must be of identical length.​ |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidIPAddress.Malformed |The specified IP address is malformed. |The specified IP is invalid. |
|400 |InvalidEip.InstanceIdMismatch |The specified elastic ip and instance mismatch. |The specified EIP does not match the instance. |
|400 |InvalidExternalIP.InUse |The specified external ip has been used by another snat entry. |The specified EIP is already used by another Source Network Address Translation (SNAT) rule. |
|400 |InvalidNatGateway.UnSupportAction |The specified NAT gateway does not support this action. |The specified NAT gateway does not support the current action. |
|400 |InvalidPortType.Malformed |The specified port type is malformed. |The specified port type is invalid. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|403 |Forbidden |You are not authorized to create a dnat entry of ip mapping. |No permission to create DNAT rules for IP mapping. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|404 |InvalidNatIp.NotFound |The specified nat ip does not exist. |The specified NAT IP does not exist. |
|409 |InvalidDnatEntry.Conflict |The specified DNAT entry conflicts with that of another DNAT entry in your NAT gateway. |The specified DNAT rule conflicts with another entry of the same NAT gateway. |
|412 |InvalidNatGateway.Expired |The specified NAT gateway has expired. |The specified NAT gateway is expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
