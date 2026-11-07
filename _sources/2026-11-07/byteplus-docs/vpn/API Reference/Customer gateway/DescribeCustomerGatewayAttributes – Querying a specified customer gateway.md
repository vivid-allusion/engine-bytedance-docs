---
title: "DescribeCustomerGatewayAttributes – Querying a specified customer gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGatewayAttributes"
---

Call DescribeCustomerGatewayAttributes to query information of a specified customer gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeCustomerGatewayAttributes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|9QFEHf">必选</span> `Example: DescribeCustomerGatewayAttributes`

The action that you want to perform. Value: DescribeCustomerGatewayAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|35sMGF">必选</span> `Example: 2020-04-01`

The API version.



**CustomerGatewayId ** <span data-label="purple">String </span><span data-api-tag="require|syxIhN">必选</span> `Example: cgw-3tehy13n2l4c6c0v****`

ID of the customer gateway. You can call [DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) to query the customer gateway ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 202203211611080102121461940900****`

Request ID.



**AccountId ** <span data-label="purple">String </span>`Example: 20005****`

The account ID associated with the customer gateway.



**CustomerGatewayId ** <span data-label="purple">String </span>`Example: cgw-3tehy13n2l4c6c0v****`

ID of the customer gateway.



**IpAddress ** <span data-label="purple">String </span>`Example: 8.XX.XX.8`

The egress IP address of the customer gateway.



**ConnectionCount ** <span data-label="purple">Integer </span>`Example: 8`

The number of IPsec\-VPN connections associated with the customer gateway.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the customer gateway is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-09T10:30:04+08:00`

The time when the customer gateway is created.



**CustomerGatewayName ** <span data-label="purple">String </span>`Example: CGW-q04n`

The name of the customer gateway.



**Description ** <span data-label="purple">String </span>`Example: This is a sample description`

Description of the customer gateway.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the customer gateway.


* Creating

* Deleting

* Pending: Configuration in progress.

* Available



**ProjectName ** <span data-label="purple">String </span>`Example: Project_1`

The project to which the customer gateway belongs.



**Asn ** <span data-label="purple">Integer </span>`Example: 65001`

The ASN of the customer gateway.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Information about all tags associated with the customer gateway.


**Key ** <span data-label="purple">String </span>`Example: key1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: value1`

The tag value.




**IpVersion ** <span data-label="purple">String </span>`Example: ipv4`

The IP protocol type of the VPN gateway.


* ipv4

* ipv6



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeCustomerGatewayAttributes&Version=2020-04-01&CustomerGatewayId=cgw-7qthudw0ll6jmc**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeCustomerGatewayAttributes",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccountId": "20005****",
        "Asn": 65001,
        "ConnectionCount": 8,
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "CustomerGatewayId": "cgw-3tehy13n2l4c6c0v****",
        "CustomerGatewayName": "CGW-q04n",
        "Description": "This is a sample description",
        "IpAddress": "8.XX.XX.8",
        "IpVersion": "ipv4",
        "ProjectName": "Project_1",
        "RequestId": "202203211611080102121461940900****",
        "Status": "Available",
        "Tags": [
            {
                "Key": "key1",
                "Value": "value1"
            }
        ],
        "UpdateTime": "2021-04-09T10:30:04+08:00"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidCustomerGateway.NotFound |The specified customer gateway does not exist. |The specified customer gateway does not exist. |
