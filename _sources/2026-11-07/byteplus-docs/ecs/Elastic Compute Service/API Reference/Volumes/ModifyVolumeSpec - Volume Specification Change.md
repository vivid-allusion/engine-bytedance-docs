---
title: "ModifyVolumeSpec - Volume Specification Change"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modifyvolumespec"
---

Change the volume specifications via the ModifyVolumeSpec interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## precautions

For detailed precautions about volume specification changes, see [Volume Specification Change](https://docs.byteplus.com/en/docs/ecs/Modify-volume-type).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyVolumeSpec&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the interface\-specific request parameters and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|9gWRai">必选</span> `Example: ModifyVolumeSpec`

Operation to perform, value: ModifyVolumeSpec



**Version ** <span data-label="purple">string </span><span data-api-tag="require|NWjje6">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**VolumeId ** <span data-label="purple">string </span><span data-api-tag="require|n0ypyq">必选</span> `Example value: vol-hwnpjm4gl8jww4u0****`

Volume ID.



**TargetVolumeType ** <span data-label="purple">string </span><span data-api-tag="require|98biJX">必选</span> `Example value: ESSD_FlexPL`

The modified volume specifications currently only support changing ESSD_PL0 volumes to ESSD_FlexPL volumes, which are set as ESSD_FlexPL.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return Parameters

Only the interface\-specific return parameters are listed below. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**VolumeId ** <span data-label="purple">string </span>`Example: vol-hwnpjm4gl8jww4u0****`

Volume ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After invoking the ModifyVolumeSpec interface, if you see the volume upgraded to the target specification on the console, it means the volume specification change was successful.</div>




**OrderNo ** <span data-label="purple">string </span>`Example value: Order218800001834604****`

Order number.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The order number is only returned when modifying the specifications of a subscription volume.</div>




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ModifyVolumeSpec&Version=2020-04-01&VolumeId=vol-hwnpjm4gl8jww4u0****&TargetVolumeType=ESSD_FlexPL HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "2025112516580923709012719033****",
    "Action": "ModifyVolumeSpec",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "VolumeId": "vol-hwnpjm4gl8jww4u0****",
    "OrderNo": "Order218800001834604****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to business logic for this API. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|400 |InvalidParameters |The request has invalid parameters. |The request contains invalid parameters. |
|400 |MissingVolumeID |The specified parameter VolumeId is missing. |Missing volume ID. |
|400 |InvalidVolumeSize |Invalid volume size. |The volume size is invalid. |
|400 |IncorrectVolumeStatus |The specified volume status is invalid. |The specified volume status is invalid. |
|400 |ErrInvalidCurrentVolumeType |The current volume type is invalid. |The current volume type is invalid. |
|400 |ErrInvalidTargetVolumeType |The target volume type is invalid. |The target volume type is invalid. |
|404 |VolumeNotFound |The specified volume does not exist. |The volume does not exist. |
|412 |ErrInstanceExpired |Instance is already expired. |The ECS instance has expired. |
|412 |ErrVolumeDownGradeTooOften |Only one modification is allowed within one days. |You can only downgrade the specification once per day. |
|412 |QuotaCheckNotPass |The user has exceeded the quota for creating volumes of this type and cannot create more: {{param}}. |The user has exceeded their quota for this type of volume and cannot create more: {{param}}. |
|500 |InternalError |An internal error has occurred. |Internal error. Try again. If multiple attempts fail, submit a ticket. |
