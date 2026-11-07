---
title: "ListContactGroups"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListContactGroups"
---

Obtain the list of alerting contact groups.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListContactGroups&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListContactGroups |API name. The API name is `ListContactGroups`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |The previous page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* A number from 0 to 100.<br><br>* The default number is 10. |
|Filter |Object of [ContactGroupFilter](https://docs.byteplus.com/en/docs/vmp/ListContactGroups#contactgroupfilter) |No |\- |Filter conditions for contact groups. |
|SortBy |String |No |CreatedAt |Whether to perform query result sorting. The value `CreatedAt` indicates that the results will be sorted. Absence of this parameter indicates no sorting. |
|SortOrder |String |No |Asc |Sorting order of query results:<br><br><br>* **Asc**: indicates sorting in ascending order.<br><br>* **Desc**: indicates sorting in descending order. |


<span id="ContactGroupFilter"></span>
### ContactGroupFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |Exact query by contact group IDs. |
|Name |String |No |test |Fuzzy query by the name of a contact group. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListContactGroups&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Ids": [
            "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
        ],
        "Name": "test"
    },
    "SortBy": "CreatedAt",
    "SortOrder": "Asc"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of contact groups. |
|Items |Array of [ContactGroup](https://docs.byteplus.com/en/docs/vmp/ListContactGroups#contactgroup) |\- |A list of contact groups. |


<span id="ContactGroup"></span>
### ContactGroup


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c |Contact group ID. |
|Name |String |test |The name of a contact group. |
|ContactIds |Array of String |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |A list of IDs for contact persons in the group. |
|CreateTime |String |2020\-01\-01T00:00:00Z |The creation time of the contact group. It is presented in RFC3339 format. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListContactGroups",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c",
                "Name": "test",
                "ContactIds": [
                    "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
                ],
                "CreateTime": "2020-01-01T00:00:00Z"
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
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The specified parameter is invalid. |
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
