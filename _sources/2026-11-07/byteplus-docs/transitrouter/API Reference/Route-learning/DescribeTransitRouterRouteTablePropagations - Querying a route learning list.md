---
title: "DescribeTransitRouterRouteTablePropagations - Querying a route learning list"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTablePropagations"
---

Call DescribeTransitRouterRouteTablePropagations to query route learning that meets the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterRouteTablePropagations&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|DjKhWv">必选</span> `Example value: DescribeTransitRouterRouteTablePropagations`

The interface name. The current API name is `DescribeTransitRouterRouteTablePropagations`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|tJyLX0">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**PageNumber ** <span data-label="purple">Integer </span><span data-api-tag="require|JkgX4f">必选</span> `Example value: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span><span data-api-tag="require|yBI1zb">必选</span> `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**TransitRouterAttachmentId ** <span data-label="purple">String </span><span data-api-tag="require|lM4PFT">必选</span> `Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.


* You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.

* You can call the [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) API to obtain the ID of the Direct Connect (DC) Gateway attachment.

* You can call the [DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) API to obtain the ID of the inter\-region attachment.



**TransitRouterRouteTableId ** <span data-label="purple">String </span><span data-api-tag="require|Jaf2L1">必选</span> `Example value: r-rtb-1i5i8khf9m58gae5kcx6****`

The ID of the route table associated with the Transit Router (TR) instance. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageNumber ** <span data-label="purple">Integer </span>`Example value: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of route learning that matches the conditions.



**TransitRouterRouteTablePropagations ** <span data-label="purple">Object[] </span>`Example value: --`

The details of route learning that matches the conditions.


**CreationTime ** <span data-label="purple">String </span>`Example value: 2021-04-09T08:36:47+08:00`

The time when route learning is created.



**TransitRouterAttachmentId ** <span data-label="purple">String </span>`Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.



**TransitRouterRouteTableId ** <span data-label="purple">String </span>`Example: tr-rtb-1i5i8khf9m58gae5kcx6****`

The ID of the route table associated with the Transit Router (TR) instance.



**Status ** <span data-label="purple">String </span>`Example: Available`

The route learning status.


* Available

* Creating

* Pending: ​​Configuration in progress.

* Deleting



**PropagationGranularity ** <span data-label="purple">String </span>`Example value: Subnet`

The route learning granularity.


* Subnet: Learn routes per subnet

* VPC: Learn routes per Virtual Private Cloud (VPC).




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTransitRouterRouteTablePropagations&Version=2020-04-01&TransitRouterRouteTableId=r-rtb-1i5i8khf9m58gae5kcx6**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T031012Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250815111015034200066214456DC8",
        "Action": "DescribeTransitRouterRouteTablePropagations",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageSize": 1,
        "PageNumber": 1,
        "TotalCount": 2,
        "TransitRouterRouteTablePropagations": [
            {
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "TransitRouterAttachmentId": "tr-attach-13n2l4c****",
                "TransitRouterRouteTableId": "tr-rtb-1i5i8khf9m58gae5kcx6****",
                "Status": "Available"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
