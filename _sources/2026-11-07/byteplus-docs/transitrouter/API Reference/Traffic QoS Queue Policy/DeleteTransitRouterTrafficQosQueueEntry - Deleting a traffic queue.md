---
title: "DeleteTransitRouterTrafficQosQueueEntry - Deleting a traffic queue"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosQueueEntry"
---

Call the DeleteTransitRouterTrafficQosQueueEntry API to delete the specified traffic queue.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterTrafficQosQueueEntry&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Yhe8tb">必选</span> `Example value: DeleteTransitRouterTrafficQosQueueEntry`

The interface name. The current API name is `DeleteTransitRouterTrafficQosQueueEntry`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|QFof5U">必选</span>`Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterTrafficQosQueueEntryId ** <span data-label="purple">String </span><span data-api-tag="require|N77lM8">必选</span> `Example value: tr-tqe-1i5i8khf9m58gae5kcx6****`

Traffic queue ID. You can call the [DescribeTransitRouterTrafficQosQueueEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueueEntries) API to get the traffic queue ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterTrafficQosQueueEntry&Version=2020-04-01&TransitRouterTrafficQosQueueEntryId=tr-tqe-1i5i8khf9m58gae5kcx6**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250722T132947Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250722/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2024073017145814907708609292B752",
        "Action": "DeleteTransitRouterTrafficQosQueueEntry",
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
|400 |InvalidTransitRouterTrafficQosQueueEntry.DefaultCannotDelete |The specified Transit Router traffic qos queue entry is default, and cannot be deleted. |The specified traffic queue is the default queue and cannot be deleted. |
|400 |InvalidTransitRouterTrafficQosQueueEntry.InvalidStatus |The specified Transit Router traffic qos queue entry is not in the correct status for the request. |The specified traffic queue cannot respond to this request due to its status. |
|404 |InvalidTransitRouterTrafficQosQueueEntry.NotFound |The specified Transit Router traffic qos queue entry does not exist. |The specified traffic queue does not exist. |
