---
title: "ListTagsForResources"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListTagsForResources"
---

Obtain a list of resource labels.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListTagsForResources&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListTagsForResources |API name. The API name is `ListTagsForResources`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/vmp/ListTagsForResources#tagfilter) |No |\- |Conditions used to filter labels. |
|ResourceType |String |Yes |Workspace |Resource type. `Workspace` is the only type supported currently. |
|ResourceIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Resource ID. |
|NextToken |String |No |1 |Current page number. The minimum and default values are both 1. |
|MaxResults |Long |No |10 |Results per page:<br><br><br>* A number from 0 to 100.<br><br>* 10 by default. |


<span id="TagFilter"></span>
### TagFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |doc |Key of label. |
|Values |Array of String |No |demo |Value of label. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListTagsForResources&Version=2021-03-03
Content-Type: application/json
{
    "ResourceType": "Workspace",
    "ResourceIds": [
        "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
    ],
    "TagFilters": [
        {
            "Key": "doc",
            "Values": [
                "demo"
            ]
        }
    ],
    "NextToken": "1",
    "MaxResults": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Types |Sample value |Description |
|---|---|---|---|
|NextToken |String |1 |Current page number. The minimum and default values are both 1. |
|ResourceTags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/vmp/ListTagsForResources#resourcetag) |\- |Resources and labels that meet the filter criteria. |


<span id="ResourceTag"></span>
### ResourceTag


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|TagKey |String |doc |Key of label. |
|TagValue |String |demo |Value of label. |
|ResourceID |String |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Resource ID. |
|ResourceType |String |Workspace |Resource type. `Workspace` is the only type supported currently. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListTagsForResources",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "1",
        "ResourceTags": [
            {
                "TagKey": "doc",
                "TagValue": "demo",
                "ResourceID": "["e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"]",
                "ResourceType": "workspace"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
