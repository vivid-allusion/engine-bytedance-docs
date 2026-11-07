---
title: "DescribeImages - Queries images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeImages"
---

Call the DescribeImages operation to query image information.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

When you call this operation, the number of images queried using `TagFilters.N.Key` and `TagFilters.N.Values.N` cannot exceed 1,000. If the number exceeds 1,000, please call the [DescribeTags](https://docs.byteplus.com/en/docs/ecs/DescribeTags) operation to query image information.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeImages&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|WRCNCg">必选</span> `Sample value: DescribeImages`

The action that you want to perform. Valid value: DescribeImages.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|t1GM88">必选</span> `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ImageIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: ImageIds.1=image-3tksv4n6ay3vj0******& ImageIds.2=image-2asdv4n6ay3vj0******`

The ID of the image. A maximum of 100 IDs are supported. You can call the [CreateImage](https://docs.byteplus.com/en/docs/ecs/CreateImage) and [ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage) operations to obtain the custom image ID, or call this operation to query and obtain the custom image ID.


* Argument \- N: specifies the serial number of the image ID.

* Separate multiple image IDs with `&`.



**ImageName ** <span data-label="purple">string </span>`Optional` `Sample value: testImage`

The name of the image.



**InstanceTypeId ** <span data-label="purple">string </span>`Optional` `Sample value: ecs.c1.xlarge`

The type ID of the instance. When you pass in this parameter, the list of available image IDs for the instance type is returned.



**IsLTS ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Specifies whether the public image is long\-term maintained. Valid values:


* true: The public image is long\-term maintained.

* false (default): This parameter does not take effect.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only when you pass in <code>true</code> to query long\-term maintained public images. When you pass in <code>false</code> or do not pass in a value, this parameter does not take effect.</div>




**IsSupportCloudInit ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Specifies whether the image supports Cloud\-init. Valid values:


* true: The image supports Cloud\-init.

* false: Not supported



**MaxResults ** <span data-label="purple">integer </span>`Optional` `Sample value: 15`

The number of entries returned on each page in a pagination query.


* Value range: 1 to 100.

* Default value: 15.



**NextToken ** <span data-label="purple">string </span>`Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**OsType ** <span data-label="purple">string </span>`Optional` `Sample value: Linux`

The operating system type. Valid values:


* Linux

* Windows



**Platform ** <span data-label="purple">string </span>`Optional` `Sample value: CentOS`

The distribution of the image operating system. Valid values:


* CentOS

* Debian

* veLinux

* Windows Server

* Fedora

* OpenSUSE

* Ubuntu



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The project to which the resource belongs.



**Status.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: Status.1=available&Status.2=creating`

The status of the image. Up to 10 statuses are supported. If this parameter is not configured, only images in the `available` status are returned by default. Valid values:


* available (default): The image is available.

* creating: The image is being created.

* error: An error is encountered.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: Specifies the serial number of the image status.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple image statuses with ampersands (&).</div>




**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Key=k1`

The tag key of the image tag.

Parameter \- N specifies the serial number of the tag key.


* Valid range: 1–10, with multiple tag keys separated by ampersands (&).

* Duplicates are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The tag value of the image tag.


* The first N specifies the serial number of the tag key. Value range: 1–10.

* The second N specifies the serial number of the tag value. Value range: 1–3. You can query up to three tag values for the same tag key .

* Separate multiple tag values with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




**Visibility ** <span data-label="purple">string </span>`Optional` `Sample value: public`

The visibility of the image. Valid values:


* public: public image

* private: custom image

* shared: shared image



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Images ** <span data-label="purple">object[] </span>`Sample value: --`

The image information.


**MarketplaceImageBillType ** <span data-label="purple">integer </span>`Sample value: 1`

Billing method supported by the marketplace image. Values:


* `0`: Only "Pay\-as\-you\-go" is supported

* `1`: Only "Subscription" is supported

* `2`: Both "Subscription" and "Pay\-as\-you\-go" are supported


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when you query a marketplace image.</div>




**LifecycleStatus ** <span data-label="purple">string </span>`Sample value: Mainstream`

Image lifecycle status. Valid values:


* Mainstream: The image is in the full support phase.

* Maintenance: The image is in the maintenance and support phase.

* EndOfLife: The image is in the extended support phase.

* Deprecated: The image is no longer available.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when you query a public image.</div>




**Architecture ** <span data-label="purple">string </span>`Sample value: amd64`

The architecture type of the image. Valid values:


* amd64: x86

* arm64: ARM



**BootMode ** <span data-label="purple">string </span>`Sample value: UEFI`

The boot mode of the image.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2021-07-26T21:55:12+08:00`

The time when the image was created. The time must comply with the RFC3339 format.



**Description ** <span data-label="purple">string </span>`Sample value: testdescription`

The image description.



**DetectionResults ** <span data-label="purple">object </span>`Sample value: --`

The detection result of the image.


**DetectionStatus ** <span data-label="purple">string </span>`Sample value: Finished`

The image detection status. Valid values:


* Finished: Indicates detection is complete

* Processing: Indicates detection is in progress



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

The details of the image detection item.


**Name ** <span data-label="purple">string </span>`Sample value: Virtio1.1`

The name of the detection item. You can view the details of supported detection items in [Detection item description](https://docs.byteplus.com/en/docs/ecs/Detect_item_description).



**Result ** <span data-label="purple">string </span>`Sample value: Unsupported`

The corresponding result for this detection item.



**RiskCode ** <span data-label="purple">string </span>`Sample value: Virtio110.NotInstalled`

The risk description code. You can view the details in [Detection item description](https://docs.byteplus.com/en/docs/ecs/Detect_item_description).



**RiskLevel ** <span data-label="purple">string </span>`Sample value: High`

The risk level. You can view the details in [Detection item description](https://docs.byteplus.com/en/docs/ecs/Detect_item_description).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the return value of this parameter is empty, no risk exists.</div>






**ImageId ** <span data-label="purple">string </span>`Sample value: image-3tksv4n6ay3vj******`

The image ID.



**ImageName ** <span data-label="purple">string </span>`Sample value: testImage`

The name of the image.



**ImageOwnerId ** <span data-label="purple">string </span>`Sample value: 210005****`

The ID of the account to which the image belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only when you query shared images.</div>




**IsInstallRunCommandAgent ** <span data-label="purple">boolean </span>`Sample value: false`

Specifies whether the cloud assistant Agent is installed in the image. Valid values:


* true: installed

* false: not installed


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only for public images.</div>




**IsLTS ** <span data-label="purple">boolean </span>`Sample value: true`

Specifies whether the public image is long\-term maintained.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only for public images and is meaningless for custom images.</div>




**IsSupportCloudInit ** <span data-label="purple">boolean </span>`Sample value: true`

Specifies whether the image supports Cloud\-init.



**Kernel ** <span data-label="purple">string </span>`Sample value: 3.10.0-1160.80.1.el7.x86_64`

The kernel version of the image.



**LicenseType ** <span data-label="purple">string </span>`Sample value: BytePlus`

The type of image license. Valid values:


* BytePlus: By default, the official license of BytePlus is used based on the `platform` you specified.

* BYOL: Bring Your Own License (BYOL).



**OsName ** <span data-label="purple">string </span>`Sample value: CentOS 7.9 64 bit`

The operating system of the image.



**OsType ** <span data-label="purple">string </span>`Sample value: Linux`

The operating system type.



**Platform ** <span data-label="purple">string </span>`Sample value: CentOS`

The distribution of the image operating system. Valid values:


* CentOS

* Debian

* veLinux

* Windows Server

* Fedora

* OpenSUSE

* Ubuntu



**PlatformVersion ** <span data-label="purple">string </span>`Sample value: 7.9`

The platform version of the image.



**ProductCode ** <span data-label="purple">string </span>`Sample value: cm015022`

The product code of the marketplace image.



**ProjectName ** <span data-label="purple">string </span>`Sample value: 210005****`

The project to which the resource belongs.



**ShareStatus ** <span data-label="purple">string </span>`Sample value: HasShared`

The share status of the image. Valid values:


* HasShared: The custom image has been shared with other users.

* When the custom image is not shared or when you use a public image, the return value of the `ShareStatus` parameter is empty.



**Size ** <span data-label="purple">integer </span>`Sample value: 40`

The size of the image in GiB.



**Snapshots ** <span data-label="purple">object[] </span>`Sample value: --`

The information of the snapshot associated with the image.


**Size ** <span data-label="purple">integer </span>`Sample value: 8`

The snapshot size in GiB.



**SnapshotId ** <span data-label="purple">string </span>`Sample value: vol-bp1s5fnvk4gn2tws0****`

The snapshot ID.



**VolumeKind ** <span data-label="purple">string </span>`Sample value: system`

The volume category. Valid values:


* system: system volume

* data: data volume




**Status ** <span data-label="purple">string </span>`Sample value: available`

The status of the image.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tag information of the image.


**Key ** <span data-label="purple">string </span>`Sample value: image-tag-key-1`

The tag key of the image.



**Value ** <span data-label="purple">string </span>`Sample value: image-tag-value-1`

The tag value of the image.




**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2021-07-26T21:55:12+08:00`

The image update time, which must comply with the RFC3339 format.



**VirtualSize ** <span data-label="purple">double </span>`Sample value: 42949672960`

The image size in Byte.



**Visibility ** <span data-label="purple">string </span>`Sample value: public`

The visibility of the image.




**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The pagination token returned by this call. If this value is empty, the current page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeImages&Version=2020-04-01&ImageId=image-ebgy1og99tfct0gw**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240306165859006BB5E*****",
    "Action": "DescribeImages",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "Images": [
      {
        "ImageId": "image-ebgy1og99tfct0gw****",
        "ImageName": "CentOS7.9-pal",
        "Description": "",
        "VirtualSize": 8589934592,
        "Size": 8,
        "OsType": "Linux",
        "Platform": "CentOS",
        "ReleaseVersion": "0",
        "Status": "available",
        "Visibility": "private",
        "Architecture": "amd64",
        "UpdatedAt": "2024-03-04T15:44:39+08:00",
        "CreatedAt": "2024-02-21T14:43:42+08:00",
        "OsName": "CentOS 7.9 64 bit",
        "PlatformVersion": "7.9",
        "ProductCode": "cm015022",
        "IsSupportCloudInit": true,
        "LicenseType": "BytePlus",
        "ShareStatus": "",
        "ImageOwnerId": "",
        "ProjectName": "default",
        "Snapshots": [
          {
            "SnapshotId": "snap-3vgp9debs*****",
            "Size": 8,
            "VolumeKind": "system"
          }
        ],
        "BootMode": "UEFI",
        "Tags": [],
        "IsLTS": true,
        "DetectionResults": {
          "DetectionStatus": "Processing",
          "Items": []
        }
      }
    ],
    "NextToken": ""
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidOsType.Malformed |The specified OsType is malformed. |The specified operating system is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The format of the specified tag key for query is invalid.​ ​​ |
|400 |InvalidTagFilterValue.Malformed |The specified TagFilterValue is malformed. |The format of the specified tag value for query is invalid. |
|400 |InvalidVisibility.Malformed |The specified Visibility is malformed. |The specified visibility is invalid. |
|400 |LimitExceeded.MaximumImageIds |You've reached the limit on the number of ImageIds that you can set. |The specified number of image IDs exceeds the limit. |
|400 |LimitExceeded.MaximumStatus |You've reached the limit on the number of Status that you can set. |The specified number of statuses exceeds the limit. |
|400 |LimitExceeded.MaximumTagFilterKeys |You've reached the limit on the number of TagFilterKeys that you can set. |The specified query tag key is out of range. |
|400 |LimitExceeded.MaximumTagFilterResults |You've reached the limit on the number of resources that you can describe by TagFilters. |The number of resources filtered by tag exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterValues |You've reached the limit on the number of TagFilterValues that you can set. |The specified query tag value exceeds the valid range. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
