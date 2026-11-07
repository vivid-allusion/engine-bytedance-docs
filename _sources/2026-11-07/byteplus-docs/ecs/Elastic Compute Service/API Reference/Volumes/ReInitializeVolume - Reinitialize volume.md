---
title: "ReInitializeVolume - Reinitialize volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ReInitializevolume"
---

Call the ReInitializeVolume interface to reinitialize the volume.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

After reinitializing the volume, the volume ID remains unchanged. Different creation methods of volumes result in different initial states after reinitialization, as detailed below:


* Volume created by snapshot: After reinitialization, it will be restored to the snapshot state when the volume was created, and the data generated after the volume creation was successful will be cleared.

* Volume not created by snapshot: After reinitialization, all volume data is cleared.

* It is recommended that you create a snapshot to back up the volume data before reinitializing the volume.

* Reinitialization is supported only for data disks, see [Reinitializing volume](https://docs.byteplus.com/en/docs/ecs/Reinitialize-volume) for more information.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ReInitializeVolume&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the request parameters specific to this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|gqTDtV">必选</span> `Example: ReInitializeVolume`

Operation to perform: ReInitializeVolume.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|C8VBv7">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**VolumeId ** <span data-label="purple">string </span><span data-api-tag="require|FOCTpc">必选</span> `Example: vol-3vi4xtz7r142xlz6****`

Initialized volume ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This API does not have specific response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ReInitializeVolume&VolumeID=vol-3vi4xtz7r142xlz6**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```text
{
    "ResponseMetadata": {
        "RequestId": "c95b6da5-041e-4f3c-8a4f-3f4b3411****",
        "Action": "ReInitializeVolume",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to the business logic of this API. For public error codes, please refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |VolumeInCreatingSnapshot |The operation is not permitted due to the volume is creating a snapshot. |The specified volume has snapshots being created. |
|400 |MissingVolumeID |The specified parameter VolumeId is missing. |Volume ID is missing. |
|400 |IncorrectSnapshotStatus |The specified snapshot status is invalid. |The specified snapshot status is invalid. |
|400 |SnapshotStatusNotAvailable |Current snapshot state does not support volume reinitialization. |The snapshot status of the volume pending initialization does not support volume initialization. |
|403 |IncorrectInstanceStatus |The rollback condition is not permitted due to the instance which volume attached must be in stopped status. |The current instance is not in a stopped state and cannot perform a reinitialization operation. |
|403 |OperationDenied.InstanceIsCreatingImage |The operation is not permitted due to the instance is creating an image. |The current instance is creating an image and cannot perform a reinitialization operation. |
|403 |OperationDenied.InstanceIsSnapshotRollback |The operation is not permitted due to the instance is locked by snapshot rollback or volume reInitialization. |The volume mounted by the current instance is performing a snapshot rollback or volume initialization and cannot perform a reinitialization operation. |
|404 |VolumeNotFound |The specified volume does not exist. |Volume does not exist. |
|404 |SnapshotNotFound |The specified snapshot does not exist. |The specified snapshot does not exist. |
|412 |VolumeStatusForbidReInitialize |volume status forbid reInitialize. |The current volume state does not support performing reinitialization operations. |
|412 |SystemVolumeForbidReInitialize |system volume currently does not support reInitialize. |The system disk does not support performing reinitialization operations. |
|412 |SnapshotTaskExceedLimit |Exceeded the limit on the number of ongoing snapshot tasks. |Exceeded the limit number of snapshot tasks in progress. |
