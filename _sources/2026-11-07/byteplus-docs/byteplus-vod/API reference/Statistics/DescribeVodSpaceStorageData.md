---
title: "DescribeVodSpaceStorageData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodspacestoragedata"
---

This interface is used to query the storage space usage within a certain time range under the specified space dimension.

<span id="requirements"></span>
## Requirements


* Billing: For storage space usage billing prices, please refer to [Pay-As-You-Go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* Data Latency: **1 day**.

* Time Range: The time span for queries should not exceed **93 days**.

* Permission Description: When using a sub\-account to request an interface, the interface will perform permission verification based on the sub\-account and only return the data that the sub\-account has permission to access. For more details, see [Creating a sub-account](https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-iam-users).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodSpaceStorageData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodSpaceStorageData` |The API action. For the current API, the value is `DescribeVodSpaceStorageData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceList |String |No |`test` |List of VOD space names. Multiple space names are separated by a comma `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br> |
|StartTime |String |Yes |`2023-01-01T16:00:00Z` |The start time of the query. It follows the RFC3339 format in UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |Yes |`2023-01-02T16:00:00Z` |The query end time. Follows the RFC3339 format for UTC time with second\-level precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The time span for a single query can not exceed 93 days.</div><br> |
|Aggregation |Integer |No |`86400` |The aggregation time granularity. The unit is seconds, and currently only supports a value of `86400`, which is 24 hours. |
|Type |String |No |`hot` |The storage type. It queries the usage of all storage types by default. The values are as follows:<br><br><br>* `hot`: Standard storage.<br><br>* `lowfreq`: Low\-frequency storage.<br><br>* `archive`: Archive storage.<br><br>* `punish`: Early deletion amount for low\-frequency storage.<br><br>* `archive_punish`: Early deletion amount for archive storage. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceList |Array of String |`["SpaceList"]` |The list of VOD space names. |
|StartTime |String |`2023-01-01T16:00:00Z` |The query start time. It follows the RFC3339 format for UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |`2023-01-02T16:00:00Z` |Query the end time. The UTC time follows the RFC3339 format with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Aggregation |Integer |`86400` |The aggregation time granularity. |
|Type |String |`hot` |The storage type. The values are as follows:<br><br><br>* `hot`: Standard storage.<br><br>* `lowfreq`: Low frequency storage.<br><br>* `archive`: Archive storage.<br><br>* `punish`: Early deletion amount for low frequency storage.<br><br>* `archive_punish`: Early deletion amount for archive storage. |
|LatestStorageData |Long |`123` |The latest storage amount for the selected time period. The unit is bytes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <code>Type</code> parameter is set to <code>punish</code> or <code>archive_punish</code>, the content corresponding to the <code>LatestStorageData</code> parameter represents <strong>the total storage amount for the selected time period</strong>.</div><br> |
|StorageDataList |Array of [StorageData](https://docs.byteplus.com/en/docs/25/8055#storagedata) |`-` |The storage usage details. |


#{.custom\-md\-table\-4}#

<span id="storagedata"></span>
### StorageData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2023-01-01T16:00:00Z` |The start time of the data's time interval. It follows the RFC3339 format for UTC time with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Storage |Long |`123` |The storage capacity. Measured in bytes. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodSpaceStorageData&Version=2023-01-01&SpaceList=test&StartTime=2023-01-01T16:00:00Z&EndTime=2023-01-02T16:00:00Z&Aggregation=86400&Type=hot
```


<span id="sample-response"></span>
### Sample response

```json
HTTP/1.1 200 OK
Content-Length: 190
Content-Type: application/json

{
  "ResponseMetadata": {
    "RequestId": "20201124165******22034080031B5",
    "Action": "DescribeVodSpaceStorageData",
    "Version": "2023-01-01",
    "Service": "vod"
  },
  "Result": {
    "SpaceList":["test"],
    "StartTime":"2023-01-01T16:00:00Z",
    "EndTime":"2023-01-02T16:00:00Z",
    "Aggregation":86400,
    "Type":"hot"
    "LatestStorageData":"LatestStorageData",
    "StorageDataList":[
      {
        "Time":"2023-01-01T16:00:00Z",
        "Storage":1234
      }
    ]
  }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
