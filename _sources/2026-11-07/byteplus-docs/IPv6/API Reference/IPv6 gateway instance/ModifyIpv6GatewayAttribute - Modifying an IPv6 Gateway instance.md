---
title: "ModifyIpv6GatewayAttribute - Modifying an IPv6 Gateway instance"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/ModifyIpv6GatewayAttribute"
---

Call the ModifyIpv6GatewayAttribute API to modify the name and description of a specified IPv6 Gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

If you do not configure the following optional parameters, their current values remain unchanged.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Y2gNPz">必选</span> `Example: ModifyIpv6GatewayAttribute`

The action to perform. Value: **ModifyIpv6GatewayAttribute**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|T4oIH0">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**Ipv6GatewayId ** <span data-label="purple">String </span><span data-api-tag="require|P00Uwv">必选</span> `Example: ipv6gw-hp3y0l3ln89j8****`

The ID of the IPv6 Gateway.

You can call the [DescribeIpv6Gateways](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6Gateways) API to query the ID of IPv6 Gateway.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

The description of the IPv6 Gateway instance.


* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or digit. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



**Name ** <span data-label="purple">String </span>`optional` `Example: ipv6GW-01`

The name of the IPv6 Gateway instance.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or digit. May include periods (.), underscores (_), and hyphens (\-).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ModifyIpv6GatewayAttribute&Version=2020-04-01&Ipv6GatewayId=ipv6gw-hp3y0l3ln89j8****&Name=ipv6GW-01 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: vpc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ModifyIpv6GatewayAttribute",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/IPv6/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidIpv6Gateway.InvalidStatus |The specified IPv6Gateway is not in the correct status for the request. |The specified IPv6 Gateway cannot respond to this request due to its status. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|404 |InvalidIpv6Gateway.NotFound |The specified Ipv6Gateway does not exist. |The specified IPv6 Gateway does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
