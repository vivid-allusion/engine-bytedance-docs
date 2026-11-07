---
title: "ModifyVolumeExtraPerformance - Adjust extra performance package for volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyVolumeExtraPerformance"
---

Call the ModifyVolumeExtraPerformance API to adjust the extra performance package of the volume.

<span id=".5rOo5oSP5LqL6aG5"></span>
## precautions


* ESSD FlexPL data volumes must have at least 500 GiB capacity to use the ModifyVolumeExtraPerformance API to configure extra performance.

* TSSD TL0 volumes must have at least 100 GiB capacity to use the ModifyVolumeExtraPerformance API to configure extra performance.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyVolumeExtraPerformance&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the API\-specific request parameters and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple">string</span><span data-api-tag="require|XbrfHW">必选</span>` Example: ModifyVolumeExtraPerformance`

Operation to perform, value: ModifyVolumeExtraPerformance.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|aNrl7q">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**VolumeId ** <span data-label="purple">string </span><span data-api-tag="require|MBE4K0">必选</span> `Example: vol-cmq1cd6ezvhcitve****`

ID of the volume for which you want to create or modify an extra performance package



**ExtraPerformanceTypeId ** <span data-label="purple">string </span><span data-api-tag="require|TyB5BE">必选</span> `Example value: IOPS`

The type of extra performance varies based on the volume. Details are as follows:


* The extra performance options for ESSD FlexPL data volumes are as follows:

   * Balance: Balanced extra performance.

   * IOPS: IOPS\-type extra performance.

   * Throughput: Throughput\-type extra performance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details about extra performance for ESSD FlexPL data volumes, see <a href="https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume">Extra Performance for Volumes</a>.   </div>
   

* TSSD_TL0 volumes only support the `Throughput` option, which sets additional throughput for TSSD_TL0 volumes. For more details, see [Volume Specifications – Throughput SSD Volume](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume)



**ExtraPerformanceIOPS ** <span data-label="purple">integer </span>`Optional` `Example value: 100`

Extra IOPS performance size, measured in operations per second. The range of extra performance values for different types is as follows:


* IOPS type extra performance: 0~50000

* Balance type extra performance: 0~50000



**ExtraPerformanceThroughputMB ** <span data-label="purple">integer </span>`Optional` `Example: 100`

Additional throughput performance (MB/s).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The additional throughput for ESSD FlexPL data disks ranges from 0 to 650 MB/s.</div>


* <div data-tips="true" data-tips-type="tip">Different volume capacities allow for different purchasable additional throughput amounts.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only interface\-specific return parameters are listed below. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderNumber ** <span data-label="purple">string </span>`Example: Order722545967890640****`

Order number.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ModifyVolumeExtraPerformance&Version=2020-04-01&VolumeId=vol-cmq1cd6ezvhcitve****&ExtraPerformanceTypeId=IOPS&ExtraPerformanceIOPS=10 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```text
{
    "ResponseMetadata": {
        "RequestId": "20210702183508010225243153072A****",
        "Action": "ModifyVolumeExtraPerformance",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "OrderNumber": "Order722545967890640****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists error codes related to this interface and business logic. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidExtraPerformanceType |Incorrect additional performance package type. |Incorrect extra performance package type. |
|400 |InvalidExtraPerformanceValue |Incorrect additional performance package value. |Invalid extra performance package value. |
|400 |InvalidVolumeTypeForExtraPerformance |This volume type does not support creating additional performance packages. |This volume type does not support creating extra performance packages. |
|400 |InvalidVolumeKindForExtraPerformance |System volume do not support creating additional performance packages. |System volumes do not support creating extra performance packages. |
|400 |InvalidVolumeSizeForExtraPerformance |The capacity of this volume does not support creating additional performance packages. |The volume size does not support creating an extra performance package. |
|400 |InvalidVolumeStatusForExtraPerformance |The status of this volume does not support creating additional performance packages. |The volume status does not support creating an extra performance package. |
|400 |FeatureExtraPerformanceNotAvailable |Additional performance package functionality is not available, please contact the administrator. |Extra performance package features are unavailable. Contact your administrator. |
|400 |ExtraPerformanceNotAvailableForVolume |Additional performance package functionality is not available for the current volume, please contact the administrator. |Additional performance package functionality is not available for the current volume. Contact the administrator. |
|500 |ResourceLockError |Failed to lock resource: [resourceId] |Resource lock failed: [resourceId]. |
