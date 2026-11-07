---
title: "DetectImage - Detects images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DetectImage"
---

Call the DetectImage operation to initiate an image detection process.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

For prerequisites and precautions for calling this operation, see [Image detection overview](https://docs.byteplus.com/en/docs/ecs/Image_Detection_Overview#.5rOo5oSP5LqL6aG5).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation and pass in the ID of the target image to obtain the detection result.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DetectImage&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|myPImn">必选</span> `Sample value: DetectImage`

The action that you want to perform. Valid value: DetectImage.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|awJwgq">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ImageId** <span data-label="purple">string</span> <span data-api-tag="require|BWPDw3">必选</span> `Sample value: image-yczf9rotssgh*****`

The image ID. You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation to query and obtain the image ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DetectImage&Version=2020-04-01&ImageId=image-yczf9rotssgh***** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022061517394001022514606307*****",
        "Action": "DetectImage",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidImageStatus |The specified image is not in the correct status for the request. |The current status of the image does not support this operation. |
|400 |InvalidPlatformForDetect.UnSupported |The specified image platform cannot be used for detect. |The specified image platform does not support detection |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|412 |OperationDenied.ImageIsDetecting |The specified operation is denied as your image is detecting. |The specified operation is rejected because the image is being detected. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
