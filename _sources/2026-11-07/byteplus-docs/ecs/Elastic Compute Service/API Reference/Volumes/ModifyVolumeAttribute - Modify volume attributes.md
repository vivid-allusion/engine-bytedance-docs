---
title: "ModifyVolumeAttribute - Modify volume attributes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modifyvolumeattribute"
---

Call the ModifyVolumeAttribute interface to modify volume attributes.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyVolumeAttribute&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only unique request parameters for this interface and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|0N8Q5z">必选</span>` Example value: ModifyVolumeAttribute`

Operation to perform, value: ModifyVolumeAttribute.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|puo5Ns">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**VolumeName ** <span data-label="purple">string </span><span data-api-tag="require|6kEPWg">必选</span> `Example: dtest3-volume-1`

Cloud disk name.



**Description ** <span data-label="purple">string </span>`optional` `example value: test`

Volume description information.



**DeleteWithInstance ** <span data-label="purple">boolean </span>`Optional` `Example: true`

When releasing the instance, choose whether to release the volume with the instance. Details are as follows:


* true: Released with the instance.

* false: Not released with the instance.



**DeleteProtection ** <span data-label="purple">boolean </span>`Optional` `Example: true`

Enable volume delete protection.



**DeleteProtectionRetentionDays ** <span data-label="purple">integer </span>`optional` `example value: 3`

Snapshot data associated with delete protection is retained permanently by default. You can also select a specific retention period between 1 and 65,536 days (default is 30 days). Once the set period ends, the snapshot will be deleted automatically.



**VolumeId ** <span data-label="purple">string </span><span data-api-tag="require|6kYmgq">必选</span> `Example: vol-3thhlu8byl4bwbha****`

Volume ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ModifyVolumeAttribute&Version=2020-04-01&VolumeId=vol-3tir92lne23vj0x1****&VolumeName=dtest3-volume-1&DeleteWithInstance=true HTTP/1.1
Host: open.volcengineapi.com
Region: cn-beijing
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```text
{
    "ResponseMetadata": {
        "RequestId": "202106232008120102251331430A0D****",
        "Action": "ModifyVolumeAttribute",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this interface and business logic. For public error codes, see the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |MissingVolumeID |The specified parameter VolumeId is missing. |Missing volume ID. |
|404 |VolumeNotFound |The specified volume does not exist. |The specified volume does not exist. |
