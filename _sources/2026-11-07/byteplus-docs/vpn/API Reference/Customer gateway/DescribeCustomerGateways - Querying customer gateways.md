---
title: "DescribeCustomerGateways - Querying customer gateways"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways"
---

Call DescribeCustomerGateways to query customer gateways based on the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeCustomerGateways&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|18EhzM">必选</span> `Example: DescribeCustomerGateways`

The action that you want to perform. Value: DescribeCustomerGateways.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|7FhIIb">必选</span> `Example: 2020-04-01`

The API version.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number for pagination query.


* If you specify this parameter, it must be a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



**CustomerGatewayIds.N ** <span data-label="purple">String </span>`optional` `Example: cgw-3tehy13n2l4c6c0v****`

ID of the customer gateway.


* N represents the sequence number of a VPN gateway ID.

* Separate multiple IDs with ampersands (&).



**CustomerGatewayName ** <span data-label="purple">String </span>`optional` `Example: CGW-te001`

The name of the customer gateway.



**IpAddress ** <span data-label="purple">String </span>`optional` `Example: 8.XX.XX.8`

The egress IP address of the customer gateway.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

The project to which the customer gateway belongs.


* If you provide this field, the system will query customer gateways under the specified project.

* If you omit this field, the system will query customer gateways across all projects.



**Status ** <span data-label="purple">String </span>`optional` `Example: Available`

The status of the customer gateway.


* Creating

* Deleting

* Pending: Configuration in progress.

* Available



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The specified tag key when querying resources by tag.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with `&`.

* Duplicate values are not allowed.



**TagFilters.N.Values.M ** <span data-label="purple">String </span>`optional` `Example: value1`

The specified tag value when querying resources by tag.


* The first N represents the sequence number of a tag key. Valid values: 1–10.

* The second N represents the sequence number of a tag value. Value range: 1–3. That is, you can query up to three tag values for the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, you must provide TagFilters.N.Key.

* If you only provide TagFilters.N.Key without this parameter, the system will query all tag values of the same tag key.

* If you provide an empty string, the system will query tags with an empty tag value.

* If you set multiple TagFilters.N.Values.M values for the same TagFilters.N.Key, these TagFilters.N.Values.M values are combined with a logical OR.



**IpVersion ** <span data-label="purple">String </span>`optional` `Example: ipv4`

The IP protocol type of the VPN gateway. Values:


* ipv4 (default)

* ipv6



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 202203211611080102121461940900****`

Request ID.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 33`

Total number of customer gateways that meet the conditions.



**CustomerGateways ** <span data-label="purple">Object[] </span>`Example: -`

Details of the customer gateway.


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



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-09T10:30:00+08:00`

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

The IP address protocol type of the VPN gateway.


* ipv4

* ipv6




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeCustomerGateways&Version=2020-04-01&CustomerGatewayIds.1=cgw-7qthudw0ll6jmc****&PageNumber=1&PageSize=20 HTTP/1.1
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
        "Action": "DescribeCustomerGateways",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "CustomerGateways": [
            {
                "Asn": 65001,
                "Tags": [
                    {
                        "Key": "key1",
                        "Value": "value1"
                    }
                ],
                "Status": "Available",
                "AccountId": "20005****",
                "IpAddress": "8.XX.XX.8",
                "IpVersion": "ipv4",
                "UpdateTime": "2021-04-09T10:30:00+08:00",
                "Description": "This is a sample description",
                "ProjectName": "Project_1",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "ConnectionCount": 8,
                "CustomerGatewayId": "cgw-3tehy13n2l4c6c0v****",
                "CustomerGatewayName": "CGW-q04n"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "RequestId": "202203211611080102121461940900****",
        "TotalCount": 33
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.CustomerGatewayId |You've reached the limit on the number of customer gateway IDs that you can describe. |You have reached the maximum of customer gateway IDs that you can query. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
