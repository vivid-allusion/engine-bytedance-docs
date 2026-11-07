---
title: "DescribeTransitRouterTrafficQosQueueEntries - Querying the list of traffic queues"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueueEntries"
---

Call the DescribeTransitRouterTrafficQosQueueEntries API to query traffic queues that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterTrafficQosQueueEntries&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|0cmsUB">必选</span>`Example: DescribeTransitRouterTrafficQosQueueEntries`

The interface name. The current API name is `DescribeTransitRouterTrafficQosQueueEntries`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|QuNlnr">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**TransitRouterTrafficQosQueuePolicyId ** <span data-label="purple">String </span><span data-api-tag="require|VU066I">必选</span>`Example: tr-tqp-hy13n2l4c6c0v****`

ID of the traffic queue policy.



**TransitRouterTrafficQosQueueEntryIds.N ** <span data-label="purple">String </span>`optional` `Example: tr-tqe-1i5i8khf9m58gae5kcx6****`

ID of the queue.


* N represents the serial number of the queue ID, ranging from 1 to 100.

* Separate multiple queue IDs with ampersands (&).



**TransitRouterTrafficQosQueueEntryName ** <span data-label="purple">String </span>`optional` `Example: tqe-02`

The name of the traffic queue.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterTrafficQosQueueEntries ** <span data-label="purple">Object[] </span>`Example: -`

The details of qualified traffic queues.


**Description ** <span data-label="purple">String </span>`Example: This traffic qos marking entry is used for test.`

The description of the traffic queue.



**TransitRouterTrafficQosQueueEntryName ** <span data-label="purple">String </span>`Example: tqe-02`

The name of the traffic queue.



**TransitRouterTrafficQosQueueEntryId ** <span data-label="purple">String </span>`Example: tr-tqe-1i5i8khf9m58gae5kcx6****`

Traffic queue ID.



**TransitRouterTrafficQosQueuePolicyId ** <span data-label="purple">String </span>`Example: tr-tqp-hy13n2l4c6c0v****`

ID of the traffic queue policy.



**BandwidthPercent ** <span data-label="purple">Integer </span>`Example: 10`

The percentage of cross\-region bandwidth available for the queue.



**Dscps ** <span data-label="purple">Integer[] </span>`Example: 1`

​​The DSCP value that the queue should match.​



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the traffic marking entry.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the queue is updated.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the queue is created.



**IsDefault ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether the queue is the default one.


* true: Default queue.

* false: Non\-default queue.



**Priority ** <span data-label="purple">String </span>`Example: High`

The priority of the traffic queue.


* `Normal`: Normal priority.

* `High`: High priority.




**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of qualified traffic queues.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTransitRouterTrafficQosQueueEntries&Version=2020-04-01&TransitRouterTrafficQosQueuePolicyId=tr-tqp-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T040625Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterTrafficQosQueueEntries",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 2,
        "TransitRouterTrafficQosQueueEntries": [
            {
                "Dscps": [
                    1
                ],
                "Status": "Available",
                "Priority": "High",
                "IsDefault": false,
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "Description": "This traffic qos marking entry is used for test.",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "BandwidthPercent": 10,
                "TransitRouterTrafficQosQueueEntryId": "tr-tqe-1i5i8khf9m58gae5kcx6****",
                "TransitRouterTrafficQosQueuePolicyId": "tr-tqp-hy13n2l4c6c0v****",
                "TransitRouterTrafficQosQueueEntryName": "tqe-02"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
