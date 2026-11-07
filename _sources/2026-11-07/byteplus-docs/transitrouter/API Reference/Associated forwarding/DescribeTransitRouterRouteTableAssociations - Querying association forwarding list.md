---
title: "DescribeTransitRouterRouteTableAssociations - Querying association forwarding list"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTableAssociations"
---

Call the DescribeTransitRouterRouteTableAssociations API to query association forwarding that meets the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterRouteTableAssociations&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String ` example: `DescribeTransitRouterRouteTableAssociations`

Interface name. The current API name is `DescribeTransitRouterRouteTableAssociations`.



**Version ** `String  ` Example value: `2020-04-01`

Interface version. The current API version is `2020-04-01`.



**TransitRouterRouteTableId ** `String  ` Example value: `tr-rtb-hy13n2l4c6c0v****`

The ID of the route table associated with the TR instance. You can call [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) to obtain the TR route table ID.



**PageNumber ** `Integer optional` example value: `1`

Page number of the list. Default: 1.



**PageSize ** `Integer optional` Example value: `20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**TransitRouterAttachmentId** `String optional` example value: `tr-attach-a*******`

The attachment ID.


* You can call [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) to obtain the ID of the VPC attachment.

* You can call [DescribeTransitRouterVpnAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments) to obtain the ID of the Virtual Private Network (VPN) attachment.

* You can call [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) to obtain the ID of the Direct Connect (DC) Gateway attachment.

* You can call [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) to obtain the ID of the Direct Connect (DC) Gateway attachment.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** `Integer optional` example value: `20`

Number of entries per page in the current pagination.



**PageNumber ** `Integer optional` example: `1`

The current page number.



**TotalCount ** `Integer optional` Example value: `1`

Total number of matching association forwarding.



**TransitRouterRouteTableAssociations ** `Object[] optional` example: `--`

Detailed information of eligible association forwarding.


**TransitRouterAttachmentId ** `String optional` example: `tr-attach-13n2l4c****`

The attachment ID.



**TransitRouterRouteTableId ** `String optional` example: `tr-rtb-1i5i8khf9m58gae5kcx6****`

The ID of the route table associated with the TR instance.



**Status ** `String optional` example: `Available`

Status of association forwarding.


* Available

* Creating

* Pending: ​​Configuration in progress.

* Deleting




<span id="eyRRfIjB"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterRouteTableAssociations&Version=2020-04-01&TransitRouterRouteTableId=tr-rtb-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T030547Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id="vROIIaTF"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250815110552079110162179816D68",
    "Action": "DescribeTransitRouterRouteTableAssociations",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 1,
    "TransitRouterRouteTableAssociations": [
      {
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


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified Transit Router (TR) does not exist. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified attachment does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
