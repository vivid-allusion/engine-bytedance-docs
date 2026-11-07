---
title: "DescribeTransitRouterFlowLogs - Querying the list of flow logs"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterFlowLogs"
---

Call the DescribeTransitRouterFlowLogs API to query Transit Router (TR) flow logs that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterFlowLogs&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|t0T8uh">必选</span> `Example: DescribeTransitRouterFlowLogs`

The interface name. The current API name is `DescribeTransitRouterFlowLogs`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|udeMwu">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterFlowLogName ** <span data-label="purple"> String </span>`optional` `Example: tr-fl-name`

The name of the flow log.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.



**TransitRouterFlowLogIds.N ** <span data-label="purple"> String  </span>`optional` `Example: tr-fl-12321shagg91`

The ID of the flow log.


* N represents the sequence number of a flow log ID. Valid range: 1\-100.

* Separate multiple flow log IDs with ampersands (&).



**ResourceType ** <span data-label="purple"> String  </span>`optional` `Example: PeerAttachment`

The type of the resource associated with the flow log


* PeerAttachment: Inter\-region attachment.



**ResourceId ** <span data-label="purple"> String </span>`optional` `Example: tr-peer-aa1etq18ertf****`

The ID of the resource associated with the flow log



**TlsProjectId ** <span data-label="purple"> String </span>`optional` `Example: tls-project-1252ajgbx****`

The ID of the log project.



**TlsTopicId ** <span data-label="purple"> String  </span>`optional` `Example: tls-topic-12skahxa09****`

The ID of the log topic.



**Status ** <span data-label="purple"> String  </span>`optional` `Example: Pending`

The status of the flow log.


* Active: Enabled.

* Inactive: Disabled.

* Creating

* Pending: ​​Configuration in progress.

* Deleting



**PageNumber** <span data-label="purple">Integer</span> `optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**TransitRouterId ** <span data-label="purple"> String  </span><span data-api-tag="require|3Swl3Y">必选</span> `Example: tr-7qthudw0ll6jmc****`

The TR instance ID. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**TagFilters.N.Key ** <span data-label="purple"> String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key, with a valid range of 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the flow logs that contain all specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple">String</span> `optional` `Example: v1`

The tag value.


* The first N represents the sequence number of a tag key, with a valid range of 1 to 10.

* The second N represents the sequence number of a tag value, with a valid range of 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">To provide this parameter, you must first provide TagFilters.N.Key.</div>


* <div data-tips="true" data-tips-type="default">When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterFlowLogs ** <span data-label="purple"> Object[]  </span>`Example:--`

The details of the flow log.


**Status ** <span data-label="purple"> String </span>`Example: Active`

The status of the flow log instance.



**AggregationInterval ** <span data-label="purple"> Integer </span>`Example: 1`

The collection period of flow logs. It is also the cycle at which TR aggregates log data and reports data to TLS, measured in minutes.



**CreatedAt ** <span data-label="purple"> String  </span>`Example: 2021-08-05T21:46:55+08:00`

The time when the flow log is created.



**Description ** <span data-label="purple"> String  </span>`Example: tr-fl-desc`

The description of the flow log.



**LogFormatString ** <span data-label="purple"> String </span>`Example: ${srcaddr}${dstaddr}${srcport}${dstport}${protocol}${bytes}`

The log format of the flow log.



**TransitRouterFlowLogId ** <span data-label="purple"> String </span>`Example: tr-fl-12aseg282acgqa`

The ID of the flow log.



**ResourceType ** <span data-label="purple"> String </span>`Example: PeerAttachment`

The type of the resource associated with the flow log


* PeerAttachment: Inter\-region attachment.



**UpdatedAt ** <span data-label="purple"> String  </span>`Example: 2021-08-05T21:46:55+08:00`

The time when the flow log is recently updated.



**TransitRouterFlowLogName ** <span data-label="purple"> String  </span>`Example: tr-fl-name`

The name of the flow log.



**ResourceId ** <span data-label="purple"> String  </span>`Example: tr-peer-123456****`

The ID of the resource associated with the flow log



**TlsProjectId ** <span data-label="purple"> String </span>`Example: fc69****`

ID of the log project.



**TlsProjectName ** <span data-label="purple"> String  </span>`Example: tls-project-name`

The name of the log project.



**TlsTopicId ** <span data-label="purple"> String </span>`Example: b***********`

The ID of the log topic.



**TlsTopicName ** <span data-label="purple"> String  </span>`Example: tls-topic-name`

The name of the log topic.



**TransitRouterId ** <span data-label="purple"> String  </span>`Example: tr-1hr3ty5rst****`

The ID of the TR instance to which the flow log belongs.



**Tags ** <span data-label="purple"> Object[] </span>`Example: --`

The tag information of the flow log.


**Key ** <span data-label="purple"> String  </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple"> String  </span>`Example: v1`

The tag value.




**AccountId ** <span data-label="purple"> String </span>`Example: 20****0957`

The ID of the account to which the flow log belongs.




**PageNumber** <span data-label="purple">Integer</span> `Example: 1`

The current page number.



**PageSize ** <span data-label="purple"> Integer </span>`Example: 10`

The number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple"> Integer  </span>`Example: 2`

The total number of qualified flow logs.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterFlowLogs&Version=2020-04-01&ResourceType=PeerAttachment&ResourceId=tr-peer-aa1etq18ertf****&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T104808Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterFlowLogs",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 2,
        "TransitRouterFlowLogs": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Status": "Active",
                "AccountId": "20****0957",
                "CreatedAt": "2021-08-05T21:46:55+08:00",
                "UpdatedAt": "2021-08-05T21:46:55+08:00",
                "ResourceId": "tr-peer-123456****",
                "TlsTopicId": "b***********",
                "Description": "tr-fl-desc",
                "ResourceType": "PeerAttachment",
                "TlsProjectId": "fc69****",
                "TlsTopicName": "tls-topic-name",
                "TlsProjectName": "tls-project-name",
                "LogFormatString": "${srcaddr}${dstaddr}${srcport}${dstport}${protocol}${bytes}",
                "TransitRouterId": "tr-1hr3ty5rst****",
                "AggregationInterval": 1,
                "TransitRouterFlowLogId": "tr-fl-12aseg282acgqa",
                "TransitRouterFlowLogName": "tr-fl-name"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |This request contains an invalid or unsupported parameter. The maximum number of resource query results is 100. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
