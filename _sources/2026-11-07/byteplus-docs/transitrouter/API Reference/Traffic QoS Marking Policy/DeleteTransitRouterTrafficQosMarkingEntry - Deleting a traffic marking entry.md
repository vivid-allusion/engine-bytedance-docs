---
title: "DeleteTransitRouterTrafficQosMarkingEntry - Deleting a traffic marking entry"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosMarkingEntry"
---

Call the DeleteTransitRouterTrafficQosMarkingEntry API to delete entries from a traffic marking policy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Traffic marking may be impacted by deleting traffic marking entries. If the bandwidth allocated to the scheduling queue matched by the traffic marking is insufficient for actual business requirements, normal service forwarding may be impacted.​

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterTrafficQosMarkingEntry&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|bdi9Ft">必选</span> `Example value: DeleteTransitRouterTrafficQosMarkingEntry`

The interface name. The current API name is `DeleteTransitRouterTrafficQosMarkingEntry`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|fcNITr">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterTrafficQosMarkingEntryId ** <span data-label="purple">String </span><span data-api-tag="require|Yl1Njr">必选</span> `Example value: tr-tme-1i5i8khf9m58gae5kcx6****`

ID of the marking entry. You can call the [DescribeTransitRouterTrafficQosMarkingEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingEntries) API to get the ID of the traffic marking entry.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterTrafficQosMarkingEntry&Version=2020-04-01&TransitRouterTrafficQosMarkingEntryId=tr-tme-1i5i8khf9m58gae5kcx6**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T084030Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202507311640342251801900121DE282",
        "Action": "DeleteTransitRouterTrafficQosMarkingEntry",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.InvalidStatus |The specified Transit Router traffic qos marking entry is not in the correct status for the request. |The specified traffic marking entry cannot respond to this request due to its status. |
|404 |InvalidTransitRouterTrafficQosMarkingEntry.NotFound |The specified Transit Router traffic qos marking entry does not exist. |The specified traffic marking entry does not exist. |
