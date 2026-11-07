---
title: "CreateImage - Creates images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateImage"
---

Call the CreateImage operation to create a custom image based on an instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* For prerequisites and precautions for calling this operation, see [Operation instructions](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance#.5pON5L2c6K-05piO).

* The number of custom images in the region where the instance is located cannot exceed 50.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateImage&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|cFRPlC">必选</span> `Sample value: CreateImage`

The action that you want to perform. Value: CreateImage.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|uVWKTk">必选</span> `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CreateWholeImage ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Indicates whether to create a whole image. Value:


* false: Default value. This indicates not creating a whole image.

* true: This indicates creating a whole image.



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: This is my first image`

The image description.


* It must start with a letter or a Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), equal signs (=), English commas (,), English periods (.), Chinese commas (，), Chinese periods (。), and spaces.

* It must be 0 to 255 characters in length.

* If left blank, the parameter defaults to an empty value.



**ImageName ** <span data-label="purple">string </span><span data-api-tag="require|u8rlbM">必选</span> `Sample value: image-1`

The name of the image.


* It must start with a letter or a Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), and English periods (.).

* The name must be 1 to 128 characters in length.



**InstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: i-3teco18f1w5a71******`

The instance ID. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query the instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">One of the values of this parameter, <code>SnapshotId</code>, or <code>SnapshotGroupId</code> is required.</div>




**NeedDetection ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Specifies whether to perform image detection. Value:


* true: performs image detection. This is the default value.

* false: does not perform image detection.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The image detection feature is currently in Beta. If you need a trial, contact your account manager.</div>




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The project to which the resource belongs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the account that calls the operation has permissions only on specific projects, this parameter is required. </div>




**SnapshotGroupId ** <span data-label="purple">string </span>`Optional` `Sample value: sg-120931dkslfkl****`

The snapshot consistency group ID. This indicates creating the custom image by using a snapshot consistency group. You can call the [DescribeSnapshotGroups](https://docs.byteplus.com/en/docs/ecs/DescribeSnapshotGroups) operation to obtain the snapshot consistency group ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">One of the values of this parameter, <code>SnapshotId</code>, or <code>InstanceId</code> is required.</div>




**SnapshotId ** <span data-label="purple">string </span>`Optional` `Sample value: snap-120931dkslfkl****`

The system volume snapshot ID, which indicates using the system volume snapshot to create the custom image. You can call the [DescribeSnapshots](https://docs.byteplus.com/en/docs/ecs/Describesnapshots) operation to view and obtain the snapshot ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">One of the values of this parameter, <code>InstanceId</code>, or <code>SnapshotGroupId</code> is required.</div>




**Tags.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Key=image-tag-key-1&Tags.2.Key=image-tag-key-2`

The tag key of the image tag.


* Parameter \- N: Indicates the serial number of the tag key. Value range: 1–20.

* Separate multiple keys with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Naming rules:</div>


   * <div data-tips="true" data-tips-type="tip">It cannot start with <code>volc:</code> or <code>sys:</code> in any case form.</div>


   * <div data-tips="true" data-tips-type="tip">Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.</div>


   * <div data-tips="true" data-tips-type="tip">It must be 1 to 128 characters in length.</div>


* <div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Value=image-tag-value-1&Tags.2.Value=image-tag-value-2`

The tag value of the image tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Naming rules:</div>


   * <div data-tips="true" data-tips-type="tip">Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.</div>


   * <div data-tips="true" data-tips-type="tip">It can be empty. Length limit: 0–256 characters.</div>


* <div data-tips="true" data-tips-type="tip">If you need to pass in this parameter, first specify the Tags.N.Key parameter.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ImageId ** <span data-label="purple">string </span>`Sample value: image-3teco18f1w5a71******`

The image ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateImage&Version=2020-04-01&InstanceId=i-3teco18f1w5a71******&ImageName=image-1 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"2021110417394001022514606307*****",
        "Action":"CreateImage",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
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
|400 |InvalidImageName.Malformed |The specified ImageName is malformed. |The specified image name is invalid. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidInstanceVolumeStatusForCreateImage.Unsupported |The specified instance volume status cannot be used for CreateImage. |The volume status of the specified instance does not support creating a custom image. |
|400 |InvalidParameterCombination |Indicates an incorrect combination of parameters, or a missing parameter. |Argument combination error or missing argument. |
|400 |InvalidPlatformForDetect.UnSupported |The specified image platform cannot be used for detect. |The specified image platform does not support detection |
|400 |InvalidSnapshotIdOrSnapshotGroupIdForCreateImage.UnSupported |The specified SnapshotId or SnapshotGroupId cannot be used for CreateImage. |The specified snapshot or consistency group does not support creating a custom image. |
|400 |InvalidSnapshotStatus |The status of the specified snapshot does not support this request. |The specified snapshot status does not support this operation. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidVolumeTypeForCreateImage.Unsupported |The specified instance volume type cannot be used for CreateImage. |The volume type of the specified instance does not support creating a custom image. |
|400 |LimitExceeded.MaximumImageCount |You've reached the limit on the number of image that you can create. |The number of custom images that you create exceeds the upper limit. |
|400 |LimitExceeded.MaximumSnapshotCount |You've reached the limit on the number of snapshot that you can create. |The number of specified volume snapshots exceeds the limit. |
|400 |LimitExceeded.MaximumSnapshotGroupTotalSize |You've reached the limit on the total size of snapshot group that you can create. |The capacity of the specified snapshot consistency group exceeds the limit. |
|400 |LimitExceeded.MaximumSystemVolumeSize |The specified system volume size exceeds the limit. |The specified system volume size (GiB) exceeds the limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |MissingParameter.ImageName |The required parameter ImageName is not supplied. |The image name cannot be empty. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSnapshotGroupId.NotFound |The specified SnapshotGroupId does not exist. |The specified snapshot consistency group ID does not exist. |
|404 |InvalidSnapshotId.NotFound |The specified SnapshotId does not exist. |The specified snapshot ID does not exist. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|412 |OperationDenied.SnapshotServiceUnavailable |The specified operation is denied as Snapshot service is unavailable. |The specified operation was denied because the snapshot service is not enabled. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again. If multiple attempts fail, submit a ticket. |
