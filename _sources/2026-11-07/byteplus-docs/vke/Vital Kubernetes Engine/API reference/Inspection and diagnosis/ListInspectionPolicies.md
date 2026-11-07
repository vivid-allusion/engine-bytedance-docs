---
title: "ListInspectionPolicies"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListInspectionPolicies"
---

Queries the inspection policy list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListInspectionPolicies&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListInspectionPolicies&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListInspectionPolicies |The API name. The API name is `ListInspectionPolicies`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|Filter |Object of [InspectionConfigFilter](https://docs.byteplus.com/en/docs/90/120597#inspectionconfigfilter) |No |\- |The inspection object filter. It intersects the value ranges of query parameters and returns matching results. |
|PageNumber |Long |No |1 |The starting page number for paginated queries. The value starts at 1 and defaults to 1. |
|PageSize |Long |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="inspectionconfigfilter"></span>
### InspectionConfigFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |R202604\*\*\*\* |The inspection policy ID. |
|Name |String |No |policy\-test |The inspection policy name. |
|Types |Array of String |No |ClusterInspection |The inspection type. You can only set the value to **ClusterInspection**, which indicates that a regular inspection is initiated for the inspection object. |
|ClusterIds |Array of String |No |ccbm7\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
|ResourceIds |Array of String |No |["ccbm7\*\*\*\*", "ccdhm\*\*\*\*"] |The inspection object IDs. |
|ResourceType |String |No |VkeCluster |The inspection object type. You can only set the value to **VkeCluster**, which indicates a cluster inspection. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListInspectionPolicies&Version=2022-05-12
Content-Type: application/json
{
    "Filter": {
        "Ids": [
            ""
        ],
        "Name": "policy-test",
        "Types": [
            ""
        ],
        "ClusterIds": [
            "ccbm7****"
        ],
        "ResourceIds": [
            "ccbm7****",
            "ccdhm****"
        ],
        "ResourceType": "VkeCluster"
    },
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [InspectionConfigResult](https://docs.byteplus.com/en/docs/90/120597#inspectionconfigresult) |\- |The inspection and self\-healing configurations. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |Number of tasks displayed per page. |
|TotalCount |Long |178 |The total number of data entries that match the query conditions. |


<span id="inspectionconfigresult"></span>
### InspectionConfigResult


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |R2026\*\*\*\*\*\* |The inspection policy ID. |
|Name |String |policy\-test |The inspection policy name. |
|Type |String |ClusterInspection |The inspection type. You can only set the value to **ClusterInspection**, which indicates that a regular inspection is initiated for the inspection object. |
|Enabled |Boolean |true |Whether the inspection policy is enabled. Valid values:<br><br><br>* **true**: The policy is enabled.<br><br>* **false**: The policy is disabled. |
|Schedule |String |0 0 13 \* 5 |The inspection schedule in standard crontab format. For example, 0 0 13 \* 5 means the task runs at 00:00 on the 13th of each month and at 00:00 every Friday. |
|ClusterId |String |ccbm\*\*\*\*\* |Cluster ID. |
|CreateTime |String |2021\-01\-01T00:00:00Z |The time when the inspection policy was created.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|UpdateTime |String |2021\-01\-01T00:00:00Z |The time when the inspection policy was updated.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|ClientToken |String |BC028527\-33B9\-4990\-A633\-84E9F9xxxx |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|ResourceIds |Array of String |["ccbm7\*\*\*\*", "ccdhm\*\*\*\*"] |The inspection object IDs. |
|ResourceType |String |VkeCluster |The inspection object type. You can only set the value to **VkeCluster**, which indicates a cluster inspection. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104********",
        "Action": "ListInspectionPolicies",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "R2026******",
                "Name": "policy-test",
                "Type": "ClusterInspection",
                "Enabled": true,
                "Schedule": "0 0 13 * 5",
                "ClusterId": "ccbm*****",
                "CreateTime": "2021-01-01T00:00:00Z",
                "UpdateTime": "2021-01-01T00:00:00Z",
                "ClientToken": "BC028527-33B9-4990-A633-84E9F9xxxx",
                "ResourceIds": [
                    "ccbm7****",
                    "ccdhm****"
                ],
                "ResourceType": "VkeCluster"
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 178
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no API\-specific error codes. For details about common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).
