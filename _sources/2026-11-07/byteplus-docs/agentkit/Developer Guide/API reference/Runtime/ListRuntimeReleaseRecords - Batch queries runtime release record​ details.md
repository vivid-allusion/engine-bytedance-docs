---
title: "ListRuntimeReleaseRecords - Batch queries runtime release record​ details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListRuntimeReleaseRecords"
---

You can call this operation to batch query runtime release record​ details using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|jGw20S">必选</span> `Sample value: ListRuntimeReleaseRecords`

The action that you want to perform. Value: ListRuntimeReleaseRecords.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ZZ4pCR">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Filters.N.Name ** <span data-label="purple">string[] </span>`Optional` `Sample value: Id`

Field name used for exact filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Value:

   * Id: Release order ID.

   * Status: Release order status.

   * SourceVersionNumber: Source version number.

   * TargetVersionNumber: Target version number.



**Filters.N.NameContains ** <span data-label="purple">string[] </span>`Optional` `Sample value: q`

Default parameter description



**Filters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: n6tfbaejc25r****`

Value of the filter field.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&).



**OrderBy.Key ** <span data-label="purple">string </span><span data-api-tag="require|3sbs8I">必选</span> `Sample value: CreationTime`

The key name for sorting:


* CreateTime: Creation time.

* FinishTime: Completion time.



**OrderBy.Ascend ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether the sorting result is in ascending order.


* true: Ascending.

* false (default): Descending.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|wEQvmO">必选</span> `Sample value: r-yefj305tds75z4k3****`

ID of the runtime.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

Release record​ list.


**CreationTime ** <span data-label="purple">string </span>`Sample value: 2026-02-11 14:05:48.796 +0000 UTC`

The creation time.



**Description ** <span data-label="purple">string </span>`Sample value: Release Description`

Description of the release information.



**Id ** <span data-label="purple">string </span>`Sample value: n6tfbaejc25r****`

Release record​ ID.



**LastUpdateTime ** <span data-label="purple">string </span>`Sample value: 2026-02-11 14:06:07.339 +0000 UTC`

Update time.



**NewVersionNumber ** <span data-label="purple">integer </span>`Sample value: 4`

The target version number for the release.



**OldVersionNumber ** <span data-label="purple">integer </span>`Sample value: 3`

The previously released version number.



**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-yefj305tds75z4k3****`

ID of the runtime.



**Status ** <span data-label="purple">string </span>`Sample value: finished`

Release status:


* rolling: Releasing.

* finished: Completed.

* rollbacking: Rolling back.

* rollbacked: Rolled back.

* failed: Failed.




**Total ** <span data-label="purple">integer </span>`Sample value: 1`

Total number of items that match the filter conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListRuntimeReleaseRecords&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  "RuntimeId": "r-yefj305tds75z4k3****",
  "PageNumber": 1,
  "PageSize": 10,
  "Filters": [
    {
      "Name": "Id",
      "Values": [
        "n6tfbaejc25r****"
      ]
    }
  ],
  "OrderBy": {
    "Key": "CreationTime",
    "Ascend": false
  }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2026021216481852AA621C43DFC278****",
        "Action": "ListRuntimeReleaseRecords",
        "Version": "2025-10-30",
        "Service": "agentkit",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Total": 1,
        "Items": [
            {
                "RuntimeId": "r-yefj305tds75z4k3****",
                "Status": "finished",
                "NewVersionNumber": 4,
                "OldVersionNumber": 3,
                "CreationTime": "2026-02-11 14:05:48.796 +0000 UTC",
                "LastUpdateTime": "2026-02-11 14:06:07.339 +0000 UTC",
                "Id": "n6tfbaejc25r****",
                "Description": ""
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.Key |The required parameter Key is not supplied. |The parameter Key cannot be empty.  |
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
