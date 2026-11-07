---
title: "CopyImage - Copies images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CopyImage"
---

Call the CopyImage operation to copy images across regions or copy shared images within the same region.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* This feature is in Beta. If you need a trial, contact your account manager.

* For prerequisites and precautions for calling this operation, refer to [Precautions](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images#.5rOo5oSP5LqL6aG5).

* Each region supports a maximum of 50 custom images.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

You can call the [DescribeTasks](https://docs.byteplus.com/en/docs/ecs/DescribeTasks) operation in the target region and specify the ID of the target image by using the `ResourceIds.N` parameter to query the progress of the image replication task.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CopyImage&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|5q7gzK">必选</span> `Sample value: CopyImage`

The action that you want to perform. Value: CopyImage.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|KIrsQm">必选</span> `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CopyImageTags ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Specifies whether to copy the tags of the source image. Value:


* false (default): No

* true: Yes


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not effective when you copy shared images.</div>




**Description ** <span data-label="purple">string </span>`Optional` `Sample value: winserver`

The description of the target image. If you do not specify this parameter, the description of the target image is the same as that of the source custom image. Rules for specifying the description of the target image:


* It must start with a letter or Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), equal signs (=), English commas (,), English periods (.), Chinese commas (，), Chinese periods (。), and spaces.

* It must be 0 to 255 characters in length.



**DestinationRegion ** <span data-label="purple">string </span><span data-api-tag="require|XJrJxI">必选</span> `Sample value: cn-beijing`

The target region, also where the target image resides.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When you copy an image across regions, the target region must be different from the region where the source custom image is located.</div>


* <div data-tips="true" data-tips-type="warning">When you copy a shared image within the same region, the target region must match that of the source shared image.</div>




**ImageId ** <span data-label="purple">string </span><span data-api-tag="require|Anu6qM">必选</span> `Sample value: image-4431h3l7hl31a0******`

The ID of the source custom image. You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation and configure the `Visibility=private` parameter to query and obtain the ID of the custom image.



**ImageName ** <span data-label="purple">string </span><span data-api-tag="require|fgvjU0">必选</span> `Sample value: image-1`

The name of the target custom image. Naming rules:


* It must start with a letter or a Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), and English periods (.).

* It must be 1 to 128 characters in length.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The project to which the image belongs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the account that calls the operation has permissions only on specific projects, this parameter is required. </div>




**Tags.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the target image.


* Parameter \- N: Indicates the serial number of the tag key. Value range: 1–20.

* Separate multiple keys with ampersands (&).


Naming rules:


* It cannot start with volc: or sys: in any case form.

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you set the <code>CopyImageTags</code> parameter to <code>true</code>, this parameter does not take effect.</div>


* <div data-tips="true" data-tips-type="tip">Tag keys of the same resource must be unique.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the target image.


* Parameter \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple key values with ampersands (&).

   Naming rules:

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It can be empty. Length limit: 0\-256 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you set the <code>CopyImageTags</code> parameter to <code>true</code>, this parameter does not take effect.</div>


* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ImageId ** <span data-label="purple">string </span>`Sample value: image-4431h3l7hl31a0******`

The ID of the target image.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CopyImage&Version=2020-04-01&ImageId=image-4431h3l7hl31a0******&DestinationRegion=cn-shanghai&ImageName=image-1 HTTP/1.1
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
        "Action": "CopyImage",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "ImageId": "image-3teco18f1w5a71******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified description is invalid. |
|400 |InvalidDestinationRegion.Malformed |The specified DestinationRegion is malformed. |The target region is invalid. |
|400 |InvalidImageForCopyImage.UnSupported |The specified image cannot be used for CopyImage. |The specified image does not support image replication. |
|400 |InvalidImageName.Malformed |The specified ImageName is malformed. |The specified image name is invalid. |
|400 |InvalidImageStatus |The specified image is not in the correct status for the request. |The current status of the image does not support this operation. |
|400 |InvalidRegionForCopyImage.UnSupported |The specified region cannot be used for CopyImage. |The specified source region or target region does not allow you to copy images across regions. |
|400 |LimitExceeded.MaximumImageCount |You've reached the limit on the number of image that you can create. |The number of custom images that you create exceeds the upper limit. |
|400 |LimitExceeded.MaximumImageSize |The specified image size exceeds the limit. |The specified image size exceeds the upper limit. |
|400 |MissingParameter.DestinationRegion |The required parameter DestinationRegion is not supplied. |The target region cannot be empty. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|400 |MissingParameter.ImageName |The required parameter ImageName is not supplied. |The image name cannot be empty. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The requested API does not exist. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|412 |InvalidDestinationRegion.Mismatch |The destination region cannot be equal to the target region. |The source region and the target region must be different. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|412 |OperationDenied.SnapshotServiceUnavailable |The specified operation is denied as Snapshot service is unavailable. |The specified operation was denied because the snapshot service is not enabled. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
