---
title: "DescribeTransitRouterRouteTables - Listing TR route tables"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables"
---

Call the DescribeTransitRouterRouteTables API to query basic information (such as name, creation time, and route table type) for Transit Router (TR) route tables that meet the specified filter conditions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

To query route details, such as destination CIDR block and Next Hop, call the [DescribeTransitRouterRouteEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries) API.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterRouteTables&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|dCrtQy">必选</span> `Example: DescribeTransitRouterRouteTables`

The interface name. The current API name is `DescribeTransitRouterRouteTables`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|nTYNp7">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterId ** <span data-label="purple">String </span><span data-api-tag="require|zip7Pv">必选</span> `Example: tr-7qthudw0ll6jmc****`

The ID of the TR instance. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Valid range: 1–100. Default: 20.



**TransitRouterRouteTableIds.N ** <span data-label="purple">String </span>`optional` `Example: tr-rtb-hy13n2l4c6c0v****`

The ID of the TR route table.


* N represents the sequence number of a TR route table, ranging from 1 to 100.

* Separate multiple TR route table IDs with ampersands (&).



**TransitRouterRouteTableType ** <span data-label="purple">String </span>`optional` `Example: System`

The type of the TR route table.


* System: System route table.

* Custom: Custom route table.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key of the TR route table.


* N represents the sequence number of a tag key, ranging from 1 to 10.

* Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the TR route tables that contain all specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value of the TR route table.


* The first N represents the sequence number of a tag key, ranging from 1 to 10.

* The second N represents the sequence number of a tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).

* To provide this parameter, you must first provide TagFilters.N.Key.

* When this parameter is set to an empty string, it means querying resources where the tag value is empty for the specified tag key.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

Total number of TR route tables that meet the conditions.



**TransitRouterRouteTables ** <span data-label="purple">Object[] </span>`Example: --`

The details of TR route tables that meet the conditions.


**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the TR route table is created.



**Description ** <span data-label="purple">String </span>`Example: This route table is used for test.`

The description of the TR route table.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the TR route table.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**TransitRouterRouteTableId ** <span data-label="purple">String </span>`Example: tr-rtb-im8p5z1v7rb48g****`

The ID of the TR route table.



**TransitRouterRouteTableName ** <span data-label="purple">String </span>`Example: route-1`

The name of the TR route table.



**TransitRouterRouteTableType ** <span data-label="purple">String </span>`Example: System`

The type of the TR route table.



**InRoutePolicyTableId ** <span data-label="purple">String </span>`Example: tr-rtp-im8p5z1v7rb48g****`

The ID of the inbound route policy associated with the TR route table.



**OutRoutePolicyTableId ** <span data-label="purple">String </span>`Example: tr-rtp-hy13n2v7r3g4****`

The ID of the outbound route policy associated with the TR route table.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the TR route table is last modified.



**Tags ** <span data-label="purple">Object[] </span>`Example: --`

The tag information of the TR route table.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeTransitRouterRouteTables&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T035321Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202508041153251881211922103DB215",
        "Action": "DescribeTransitRouterRouteTables",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageSize": 20,
        "PageNumber": 1,
        "TotalCount": 2,
        "TransitRouterRouteTables": [
            {
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "Description": "This route table is used for test.",
                "Status": "Available",
                "TransitRouterRouteTableId": "tr-rtb-im8p5z1v7rb48g****",
                "TransitRouterRouteTableName": "route-1",
                "TransitRouterRouteTableType": "System",
                "InRoutePolicyTableId": "tr-rtp-im8p5z1v7rb48g****",
                "OutRoutePolicyTableId": "tr-rtp-hy13n2v7r3g4****",
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |This request contains an invalid or unsupported parameter. The maximum number of resource query results is 100. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag filter keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag filter values that can be specified in a single request. |
