---
title: "DescribeTasks - Queries request progress"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeTasks"
---

Call the DescribeTasks operation to query the progress of one or more asynchronous requests.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* You can view the task progress for custom image creation, copying, import, and export, such as task IDs, status, and start and end times.

* You can log on to the [ECS console](https://console.byteplus.com/ecs/instance) and then click "Maintenance & Monitoring \> Executions" to view the task ID `TaskIds` or resource ID `ResourceId`. For details, see [Managing custom image tasks](https://docs.byteplus.com/en/docs/ecs/Managing-custom-image-tasks).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeTasks&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|TmUAtW">必选</span> `Sample value: DescribeTasks`

The action that you want to perform. Value: DescribeTasks.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|LZePuP">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 20`

The number of entries per page.


* Maximum value: 100

* Default value: 20



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: 3tiegs1y963vj0******`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ResourceId** <span data-label="purple">string</span> `Optional` `Sample value: image-ebgy1og99tfct0gw`

The resource ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To improve compatibility, use the <code>ResourceIds.N</code> parameter.</div>




**ResourceIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: ResourceIds.1=image-ebgy1og99tfc****&ResourceIds.2=image-opisd1og89tfc****`

The resource ID. A maximum of 100 resource IDs is supported.


* Argument \- N: specifies the serial number of the task.

* Separate multiple resource IDs with `&`.



**TaskIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TaskIds.1=t-ybnz9qci2sahiqdl****&TaskIds.2=t-ybnz9qci89sw*****`

The task ID. Up to 100 task IDs are supported per operation. You can obtain task IDs when you perform operations on custom images by calling [ExportImage](https://docs.byteplus.com/en/docs/ecs/ExportImage), [CopyImage](https://docs.byteplus.com/en/docs/ecs/CopyImage), or other operations.


* Argument \- N: specifies the serial number of the task.

* Separate multiple task IDs with `&`.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



**Tasks** <span data-label="purple">object[]</span> `Sample value: --`

The task list.


**CreatedAt** <span data-label="purple">string</span> `Sample value: 2022-05-06T00:01:00+08:00`

The creation time of the task.



**EndAt** <span data-label="purple">string</span> `Sample value: 2022-05-06T00:01:00+08:00`

The task end time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The returned value of this parameter is empty if the task is not completed.</div>




**Id** <span data-label="purple">string</span> `Sample value: t-ybnz9qci2sahiqdl****`

The task ID.



**Process** <span data-label="purple">long</span> `Sample value: 100`

The progress of the task (expressed as a percentage). Unit: `%`.



**ResourceId** <span data-label="purple">string</span> `Sample value: image-ebgy1og99tfct0gw****`

The resource ID.



**Status** <span data-label="purple">string</span> `Sample value: Succeeded`

The status of the task. Value:


* Pending: To be executed

* Running: Running

* Succeeded: Successful execution

* Failed: Failed execution



**Type** <span data-label="purple">string</span> `Sample value: ExportImage`

The type of the task to be queried. Value:


* ImportImage: Custom image import

* ExportImage: Custom image export

* CreateImage: Custom image creation

* CopyImage: Custom image duplication

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The feature of copying custom images is in Beta. If you need a trial, contact your account manager.   </div>
   



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2022-05-06T00:01:00+08:00`

The update time of the task.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeTasks&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "DescribeTasks",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "",
        "Tasks": [
            {
                "Id": "t-ybnz9qci2sahiqdl****",
                "CreatedAt": "2022-05-06T00:01:00+08:00",
                "UpdatedAt": "2022-05-06T00:07:12+08:00",
                "EndAt": "2022-05-06T00:07:12+08:00",
                "ResourceId": "image-ybnz9qci2sahiqdl****",
                "Type": "ExportImage",
                "Process": 100,
                "Status": "Succeeded"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumMaxResults |The number of specified MaxResults exceeds the maximum limit. |The value specified for MaxResults exceeds the upper limit. |
|400 |LimitExceeded.MaximumResourceIds |You've reached the limit on the number of ResourceIds that you can set. |The specified number of resource IDs exceeds the limit. |
|400 |LimitExceeded.MinimumMaxResults |The number of specified MaxResults exceeds the minimum limit. |The value specified for MaxResults exceeds the lower limit. |
|400 |LimitExceeded.MaximumTaskIds |You've reached the limit on the number of TaskIds that you can set. |The specified number of task IDs exceeds the limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
