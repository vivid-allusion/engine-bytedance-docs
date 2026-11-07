---
title: "ModifyTransitRouterTrafficQosQueueEntryAttributes - Modifying a traffic queue"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosQueueEntryAttributes"
---

Call the ModifyTransitRouterTrafficQosQueueEntryAttributes API to modify the bandwidth allocation, name and description for a traffic queue.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterTrafficQosQueueEntryAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|16mFOA">必选</span> `Example: ModifyTransitRouterTrafficQosQueueEntryAttributes`

The interface name. The current API name is `ModifyTransitRouterTrafficQosQueueEntryAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|jtT9rG">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterTrafficQosQueueEntryId ** <span data-label="purple"> String  </span><span data-api-tag="require|zQvD9f">必选</span> `Example: qos-queue-entry-123456789`

The ID of the TR traffic queue entry.



**TransitRouterTrafficQosQueueEntryName ** <span data-label="purple"> String </span>`optional` `Example: tqe-02`

The name of the queue.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If you do not provide this parameter or leave it unset, it defaults to empty.



**Description ** <span data-label="purple"> String </span>`Optional` `Example: This traffic qos queue entry is used for test.`

The description of the queue.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**BandwidthPercent ** <span data-label="purple"> Integer </span>`optional` `Example: 50`

The bandwidth percentage of the traffic queue, with a valid range of 0 to 100.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyTransitRouterTrafficQosQueueEntryAttributes&Version=2020-04-01&TransitRouterTrafficQosQueueEntryId=qos-queue-entry-123456789 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyTransitRouterTrafficQosQueueEntryAttributes",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.TooLong |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidName.TooLong |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterTrafficQosQueueEntry.BandwidthPercentExceed |The specified bandwidth percentage of the traffic qos queue entry exceeds the available remaining bandwidth percentage. |The specified queue bandwidth percentage exceeds the remaining allocable bandwidth percentage. |
|400 |InvalidTransitRouterTrafficQosQueueEntry.BandwidthPercentNotSupport |The specified bandwidth percent of the Transit Router traffic qos queue entry is invalid. Only normal priority traffic qos queues support configuring bandwidth percent. |The specified queue bandwidth percentage is invalid. You can only configure bandwidth percentage for normal\-priority queues. |
|400 |InvalidTransitRouterTrafficQosQueueEntry.DefaultCannotModify |The specified Transit Router traffic qos queue entry is default, and cannot be modified. |The specified traffic queue is the default queue and cannot be modified. |
|400 |InvalidTransitRouterTrafficQosQueueEntry.InvalidBandwidthPercent |The specified bandwidth percent of the Transit Router traffic qos queue entry is invalid. Bandwidth percent only support 0~100. |The specified queue bandwidth percentage is invalid. It must be an integer between 0 and 100. |
|400 |InvalidTransitRouterTrafficQosQueueEntry.InvalidStatus |The specified Transit Router traffic qos queue entry is not in the correct status for the request. |The specified traffic queue cannot respond to this request due to its status. |
|404 |InvalidTransitRouterTrafficQosQueueEntry.NotFound |The specified Transit Router traffic qos queue entry does not exist. |The specified traffic queue does not exist. |
