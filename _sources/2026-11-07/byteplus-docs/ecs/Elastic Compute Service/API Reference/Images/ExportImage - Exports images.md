---
title: "ExportImage - Exports images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ExportImage"
---

Call the ExportImage operation to export a custom image.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

For prerequisites and precautions for calling this operation, see [Operation instructions](https://docs.byteplus.com/en/docs/ecs/Exporting-custom-images#.5pON5L2c5q2l6aqk).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

You can go to the ECS console to [view export details](https://docs.byteplus.com/en/docs/ecs/Exporting-custom-images#.5ZCO57ut5pON5L2c) or query task progress by calling the [DescribeTasks](https://docs.byteplus.com/en/docs/ecs/DescribeTasks) operation.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ExportImage&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|vwDILD">必选</span> `Sample value: ExportImage`

The action that you want to perform. Value: ExportImage.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|SyEdjy">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ImageId** <span data-label="purple">string</span> <span data-api-tag="require|MGT27n">必选</span> `Sample value: image-4431h3l7hl31a0******`

The image ID. You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation and configure the `Visibility=private` parameter to query and obtain the ID of the custom image.



**TOSBucket** <span data-label="purple">string</span> <span data-api-tag="require|BtfxlK">必选</span> `Sample value: bucket-1`

The name of the TOS bucket where the file of the exported image is stored. To query and obtain the TOS bucket name, call the [ListBuckets](https://docs.byteplus.com/en/docs/tos/reference-listbuckets) operation.



**TOSPrefix** <span data-label="purple">string</span> <span data-api-tag="require|ULWkEY">必选</span> `Sample value: test123`

Indicates the custom prefix of the file name of the exported image.


* Composed of digits or letters.

* Length: 1\-30 characters

   The name of the image file to be stored in the TOS bucket is:

   `<custom prefix>_ImageId_system.qcow2`



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TaskId** <span data-label="purple">string</span> `Sample value: t-3teco18f1w5a71******`

The ID of the task for exporting the image.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ExportImage&Version=2020-04-01&ImageId=image-4431h3l7hl31a0******&TOSBucket=bucket-1&TOSPrefix=test123 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"2021110417394001022514606307*****",
        "Action":"ExportImage",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result": {
        "TaskId": "t-3teco18f1w5a71******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidImageForExportImage.UnSupported |The specified image cannot be used for ExportImage. |The specified image cannot be exported. |
|400 |InvalidImageStatus |The specified image is not in the correct status for the request. |The current status of the image does not support this operation. |
|400 |InvalidTOSPrefix.Malformed |The specified TOSPrefix is malformed. |The custom prefix of the file name is invalid. |
|400 |InvalidTosPutObject.AccessDenied |The Action tos:PutObject is not authorized for ecs, please check your IAM policy of ecs. |The permission of "tos:PutObject" is not granted to ECS instances. Please check your IAM policy for ECS instances. |
|400 |LimitExceeded.ExportImageOneday |You've reached the limit on the number of ExportImage oneday. |The number of image export operations in one day exceeds the limit. |
|400 |LimitExceeded.TaskConcurrent |You've reached the limit on the number of task concurrent. |The number of concurrently executed tasks reaches the upper limit. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|400 |MissingParameter.TOSBucket |The required parameter TOSBucket is not supplied. |The parameter TOSBucket cannot be left empty. |
|400 |MissingParameter.TOSPrefix |The required parameter TOSPrefix is not supplied. |The prefix of the file name of the exported image cannot be empty. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|404 |InvalidTOSBucket.NotFound |The specified TOSBucket does not exist. |The specified TOS bucket does not exist. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified action was rejected because your resource has been locked by other actions. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again. If multiple attempts fail, submit a ticket. |
