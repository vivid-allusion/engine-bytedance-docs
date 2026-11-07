---
title: "UnTagResources - Deletes tags"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/UnTagResources"
---

Call the UnTagResources operation to disassociate and delete tags for the specified SMC migration source and migration task.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=UnTagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|N6lqpQ">必选</span> `Sample value: UnTagResources`

The operation that you want to perform. Valid value: UnTagResources.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|VPCZso">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**ResourceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|ReEqzr">必选</span> `Sample value: ResourceIds.1=job-3tiegs1y963vj0****&ResourceIds.2=job-4segs15yts2ls****`

Resource ID.


* Argument \- N: indicates the serial number of the resource. Valid range: 1\-50.

* Separate multiple resources with ampersands (`&`).



**ResourceType ** <span data-label="purple">string </span><span data-api-tag="require|TWQInG">必选</span> `Sample value: migrationjob`

The resource type. Valid values:


* migrationsource: the migration source.

* migrationjob: the migration job.



**TagKeys.N ** <span data-label="purple">string[] </span><span data-api-tag="require|0GeUBp">必选</span> `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the tag associated with the resource.


* Parameter \- N: Indicates the serial number of the tag key. Value range: 1–20.

* Separate multiple tag keys with ampersands (`&`).

* Naming rules:

   * It cannot start with any case of `volc:` or `sys:`.

   * It can contain only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@".

   * It must be 1 to 128 characters in length.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OperationDetails ** <span data-label="purple">object[] </span>`Sample value: --`

The operation details.


**Error ** <span data-label="purple">object </span>`Sample value: --`

The error message for the resource being operated on.


**Code ** <span data-label="purple">string </span>`Sample value: InvalidResourceId.NotFound`

The error code for the failure of a specific request during batch operations. Value:


* InvalidResourceIds.NotFound: The specified resources do not exist.

* InvalidActionOrVersion: The requested operation does not exist.

* InvalidTagKey.Malformed: The specified tag key is invalid.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message ** <span data-label="purple">string </span>`Sample value: The specified ResourceId does not exist.`

The error information for the failure of a specific request during batch operations. Value:


* `The specified resourceids do not exist.`: The specified resources do not exist.

* `Could not find operation %s for version %s.`: The requested operation does not exist.

* `The specified TagKey is malformed.`: The specified tag key is invalid.




**ResourceId ** <span data-label="purple">string </span>`Sample value: job-3tiegs1y963vj0****`

The ID of the target resource.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=UnTagResources&Version=2020-04-01&ResourceType=migrationjob&ResourceIds.1=job-3tiegs1y963vj0****&ResourceIds.2=job-4segs15yts2ls****&TagKeys.1=k1&TagKeys.2=k2 HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"202306021637410F150D*****",
        "Action":"UnTagResources",
        "Version":"2020-04-01",
        "Service":"smc",
        "Region":"cn-beijing"
    },
    "Result":{
        "OperationDetails":[
            {
                "Error":null,
                "ResourceId":"job-3tiegs1y963vj0****"
            },
            {
                "Error":{
                    "Code":"InvalidResourceId.NotFound",
                    "Message":"The specified ResourceId does not exist."
                },
                "ResourceId":"job-4segs15yts2ls****"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumResourceIds |You've reached the limit on the number of ResourceIds that you can set. |The number of specified resource IDs exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagKeys |You've reached the limit on the number of TagKeys that you can set. |The number of specified tag keys exceeds the upper limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
