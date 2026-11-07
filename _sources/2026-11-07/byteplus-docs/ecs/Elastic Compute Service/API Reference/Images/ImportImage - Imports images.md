---
title: "ImportImage - Imports images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ImportImage"
---

Call the ImportImage operation to import a local image file to BytePlus. This image will be displayed as a custom image in the corresponding region.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* For prerequisites and precautions for calling this operation, refer to [Image import requirements](https://docs.byteplus.com/en/docs/ecs/Requirements).

* Each region supports a maximum of 50 custom images.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

You can use the imported image to create ECS instances ([RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances)) or change the system volume of instances ([ReplaceSystemDisk](https://docs.byteplus.com/en/docs/ecs/ReplaceSystemVolume)).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ImportImage&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|8llXOT">必选</span> `Sample value: ImportImage`

The action that you want to perform. Valid value: ImportImage.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|V5vfRk">必选</span> `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**Architecture ** <span data-label="purple">string </span>`Optional` `Sample value: amd64`

The architecture type of the image. Value:


* amd64: x86

* arm64: ARM



**BootMode ** <span data-label="purple">string </span>`Optional` `Sample value: UEFI`

The boot mode of the image. Value:


* BIOS (default): BIOS boot mode

* UEFI: UEFI boot mode


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">EBM\-type ECS instances support the <code>UEFI</code> boot mode only.</div>


* <div data-tips="true" data-tips-type="tip">If you set the <code>Architecture</code> parameter to arm64, the default value is <code>UEFI</code> and you cannot specify other values for the BootMode parameter.<code></code></div>




**Description ** <span data-label="purple">string </span>`Optional` `Sample value: This is my first image`

The image description.


* It must start with a letter or a Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), equal signs (=), English commas (,), English periods (.), Chinese commas (，), Chinese periods (。), and spaces.

* It must be 0 to 255 characters in length.

* If left blank, the parameter defaults to an empty value.



**ImageName ** <span data-label="purple">string </span><span data-api-tag="require|9MzUID">必选</span> `Sample value: image-1`

The name of the image.


* It must start with a letter or a Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), and English periods (.).

* The name must be 1 to 128 characters in length.



**ImportDataVolumes.N.DataVolumeUrl ** <span data-label="purple">string[] </span>`Optional` `Sample value: ImportDataVolumes.1.DataVolumeUrl=https://example.tos-cn-beijing.com/data1.qcow2&ImportDataVolumes.2.DataVolumeUrl=https://example.tos-cn-beijing.com/data2.qcow2`

The URL of the data volume files contained in the custom image in the TOS bucket.


* Parameter \- N: specifies the serial number of the data volume URL. Valid range: 1–15.

* Separate multiple data volume URLs with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Obtain the URLs after you upload the custom image files to the TOS bucket. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1">Importing custom images</a>.</div>




**LicenseType ** <span data-label="purple">string </span>`Optional` `Sample value: Volcengine`

The type of image license. Value:


* BytePlus: By default, the official license of BytePlus is used based on the `platform` you specified.

* BYOL: Bring Your Own License (BYOL).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you set this parameter to BYOL, make sure that your license key is supported by BytePlus.</div>


* <div data-tips="true" data-tips-type="tip">This parameter takes effect only when you import commercial images (such as Windows Server). Otherwise, this parameter does not take effect.</div>




**NeedDetection ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Specifies whether to perform image detection. Value:


* true: performs image detection. This is the default value.

* false: does not perform image detection.



**OsType ** <span data-label="purple">string </span>`Optional` `Sample value: Linux`

The operating system type. Value:


* Linux

* Windows


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you leave this parameter empty, BytePlus determines the value of the <code>OsType</code> parameter based on the value that you passed in for the <code>Platform</code> parameter.</div>




**Platform ** <span data-label="purple">string </span><span data-api-tag="require|INxUyw">必选</span> `Sample value: CentOS`

The version of the image operating system. Value:


* CentOS

* Debian

* veLinux

* Windows Server

* Fedora

* OpenSUSE

* Ubuntu

* Rocky Linux

* AlmaLinux



**PlatformVersion ** <span data-label="purple">string </span>`Optional` `Sample value: 7.6`

The platform version of the image. The version can contain up to 100 characters.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The project to which the resource belongs.



**Tags.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Key=image-tag-key-1&Tags.2.Key=image-tag-key-2`

The tag key of the image tag.


* Parameter \- N: Indicates the serial number of the tag key. Value range: 1–20.

* Separate multiple tag keys with `&`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Naming rules:</div>


   * <div data-tips="true" data-tips-type="tip">It cannot start with <code>volc:</code> or <code>sys:</code> in any case form.</div>


   * <div data-tips="true" data-tips-type="tip">Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.</div>


   * <div data-tips="true" data-tips-type="tip">It must be 1 to 128 characters in length.</div>


* <div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Value=image-tag-value-1&Tags.2.Value=image-tag-value-2`

The tag value of the image tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple key values with ampersands (`&`).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Naming rules:</div>


   * <div data-tips="true" data-tips-type="tip">Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.</div>


   * <div data-tips="true" data-tips-type="tip">It can be empty. Length limit: 0–256 characters.</div>


* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




**Url ** <span data-label="purple">string </span><span data-api-tag="require|ZAJyiY">必选</span> `Sample value: https://example.tos-cn-beijing.com/centos.qcow2`

The URL of the system volume files contained in the custom image in the TOS bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Obtain the URLs after you upload the custom image files to the TOS bucket. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1">Importing custom images</a>.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ImageId ** <span data-label="purple">string </span>`Sample value: image-ebgy1og99tfct0gw****`

The image ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ImportImage&Version=2020-04-01&ImageName=image-1&OsType=Linux&Platform=CentOS&PlatformVersion=7.6&Architecture=amd64&Url=xxx HTTP/1.1
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
        "Action": "ImportImage",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "ImageId": "image-ebgy1og99tfct0gw****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArchitecture.Malformed |The specified Architecture is malformed. |The specified image architecture type is invalid. |
|400 |InvalidBootMode.Malformed |The specified BootMode is malformed. |The specified boot mode is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified description is invalid. |
|400 |InvalidImageFormat.Malformed |The specified image format is malformed. |The specified image format is invalid. |
|400 |InvalidImageName.Malformed |The specified ImageName is malformed. |The specified image name is invalid. |
|400 |InvalidLicenseType.Malformed |The specified LicenseType is malformed. |The specified license type is invalid. |
|400 |InvalidOsType.Malformed |The specified OsType is malformed. |The specified operating system is invalid. |
|400 |InvalidPlatformForDetect.UnSupported |The specified image platform cannot be used for detect. |The specified image platform does not support detection |
|400 |InvalidPlatformForImportImage.Unsupported |The specified Platform cannot be used for ImportImage. |The specified image operating system distribution cannot be imported |
|400 |InvalidPlatformVersion.Malformed |The specified PlatformVersion is malformed. |The value specified for the PlatformVersion parameter is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidTosGetObject.AccessDenied |The Action tos:GetObject is not authorized for ecs, please check your IAM policy of ecs. |The tos:GetObject permission is not granted to ECS. Check the IAM policies attached to your ECS instance. |
|400 |InvalidUrl.Malformed |The specified URL is malformed. |The specified URL is invalid. |
|400 |LimitExceeded.MaximumImageCount |You've reached the limit on the number of image that you can create. |The number of custom images that you create exceeds the upper limit. |
|400 |LimitExceeded.MaximumImageSize |The specified image size exceeds the limit. |The specified image size exceeds the upper limit. |
|400 |LimitExceeded.MaximumImportDataVolumes |The number of specified ImportDataVolumes exceeds the maximum limit. |The specified value of the ImportDataVolumes parameter exceeds the upper limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |MissingParameter.ImageName |The required parameter ImageName is not supplied. |The image name cannot be empty. |
|400 |MissingParameter.Platform |The required parameter Platform is not supplied. |The specified operating system distribution cannot be empty. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidTOSObject.NotFound |The specified TOSObject does not exist. |The specified TOS object does not exist. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |OperationDenied.SnapshotServiceUnavailable |The specified operation is denied as Snapshot service is unavailable. |The specified operation was denied because the snapshot service is not enabled. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
