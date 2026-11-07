---
title: "ReplaceSystemVolume - Changes operating systems"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ReplaceSystemVolume"
---

You can call the ReplaceSystemVolume operation to replace the system for an instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

For prerequisites and precautions for calling this operation, see [Operation instructions](https://docs.byteplus.com/en/docs/ecs/Changing-OS#.5pON5L2c6K-05piO).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ReplaceSystemVolume&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|kdODHh">必选</span> `Sample value: ReplaceSystemVolume`

The action that you want to perform. Value: ReplaceSystemVolume.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|mppRUs">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API operation times out or an internal server error occurs. Values:

Not more than 64 ASCII characters.



**DryRun ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to only precheck this request. Value:


* true: Sends a check request only without replacing the system. Check items include whether the required parameters are provided, the request format, and business limits. If the check fails, the corresponding error is returned. If the check passes, the error code `DryRunOperation` is returned.

* false (default): Sends a normal request and directly replaces the system after the check is passed.



**ImageId ** <span data-label="purple">string </span><span data-api-tag="require|MjJSM8">必选</span> `Sample value: image-38dfk6rfisf6kir6****`

The ID of the image used when the operating system is replaced. You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation to query and obtain the image ID.



**ImageReleaseVersion ** <span data-label="purple">string </span>`Optional` `Sample value: 20241115`

The specific version number of the image used.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter only takes effect when the used image is a public image.</div>


* <div data-tips="true" data-tips-type="tip">If this parameter is empty, the latest version of the image is used.</div>




**InstanceId ** <span data-label="purple">string </span>`required` `Sample value: i-a8j6n1i4hojfqpa0****`

The instance ID. To query and obtain the instance ID, call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation.



**KeepImageCredential ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to use the password/key pair preset in the image for login. Value:


* true: Uses the password/key pair preset in the image for login.

* false (default): Does not use the password/key pair preset in the image for login.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only custom images and shared images support this feature.</div>


* <div data-tips="true" data-tips-type="tip">When this parameter is set to <code>true</code>, do not pass in <code>PassWord</code> and <code>KeyPairName</code>.</div>




**KeyPairName ** <span data-label="purple">string </span>`Optional` `Sample value: kp-test-123`

Reset the key pair. You can call the [DescribeKeyPairs](https://docs.byteplus.com/en/docs/ecs/DescribeKeyPairs) interface to query key pair information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This feature only supports Linux\-based instances.</div>


* <div data-tips="true" data-tips-type="tip">When <code>KeepImageCredential</code> is set to <code>false</code>, this parameter and <code>Password</code> cannot both be empty.</div>


* <div data-tips="true" data-tips-type="tip">If the <code>KeyPairName</code> and <code>Password</code> parameters are configured at the same time, only the <code>KeyPairName</code> parameter takes effect.</div>




**Password ** <span data-label="purple">string </span>`Optional` `Sample value: Password@123`

Reset the password. Rules for setting a password are as follows:


* The length is limited to 8~30 characters

* A password can only consist of uppercase letters, lowercase letters, numbers, and special characters, and must include at least three of these elements

   Valid special characters: `~!@#$%^&\*()_\-+=|{}[]:;'<\>,.?/

* A password cannot start with "/" or "$6$"


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For login credentials, "Password", "Key Pair", and "Keep image settings" are available. If you choose to use a password, specify a complex password to improve security.</div>


* <div data-tips="true" data-tips-type="tip">When <code>KeepImageCredential</code> is set to <code>false</code>, this parameter and <code>KeyPairName</code> cannot both be empty.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ReplaceSystemVolume&Version=2020-04-01&InstanceId=i-a8j6n1i4hojfqpa0****&ImageId=image-38dfk6rfisf6kir6****&Password=Password@123 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
            "RequestId": "2021062415303301022514515207C4****",
            "Action": "ReplaceSystemVolume",
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
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDedicatedHostStatus.Unsupported |The status of the specified dedicated host does not support this request. |The dedicated host in current status does not support this action. |
|400 |InvalidImageForReplaceSystemVolume.UnSupported |The specified image cannot be used for ReplaceSystemVolume. |The specified image does not support changing the operating system. |
|400 |InvalidImageSize.Malformed |The specified ImageSize is malformed. |The specified image size is invalid. |
|400 |InvalidInstanceForReplaceSystemVolume.Unsupported |The specified instance cannot be used for ReplaceSystemVolume. |The specified instance does not support replacing the operating system. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidKeyPairForWindows.Unsupported |The OSType of this specified instance is Windows, which does not support key pairs. |The specified instance is based on the Windows operating system and does not support key pairs. |
|400 |InvalidPassword.Malformed |The specified password is malformed. |The specified password format is invalid. |
|400 |InvalidSnapshotStatus |The status of the specified snapshot does not support this request. |The specified snapshot status does not support this operation. |
|400 |InvalidVolumeAffinity.Malformed |The specified VolumeAffinity is malformed. |The affinity of the specified volume is invalid. |
|400 |InvalidVolumeDescriptionFormat.Malformed |The specified VolumeDescriptionFormat is malformed. |The format of the specified volume description is invalid. |
|400 |InvalidVolumeDescriptionLen.Malformed |The specified VolumeDescriptionLen is malformed. |The length of the specified volume description is invalid. |
|400 |InvalidVolumeKind.Malformed |The specified VolumeKind is malformed. |The specified volume attribute is invalid. |
|400 |InvalidVolumeNameFormat.Malformed |The specified VolumeNameFormat is malformed. |The format of the specified volume name is invalid. |
|400 |InvalidVolumeNameLen.Malformed |The specified VolumeNameLen is malformed. |The length of the specified volume name is invalid. |
|400 |InvalidVolumeStatus |The status of the specified volume does not support this request. |The volume in current status does not support this action. |
|400 |InvalidVolumeTypeForSnapshot.UnSupported |The specified VolumeType cannot be used for create snapshot. |The specified volume type does not support snapshots. |
|400 |LimitExceeded.MaximumVolumes |You've reached the limit on the number of volumes that can be attached to the instance. |The specified number of volumes mounted to the instance exceeds the maximum limit. |
|400 |LimitExceeded.SystemVolumeSize |The specified system volume size exceeds the limit. |The specified system volume size (GiB) exceeds the limit. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The parameter InstanceId cannot be left empty. |
|400 |MissingParameter.PasswordAndKeyPair |The required parameter PasswordAndKeyPair is not supplied. |The password and key pair cannot both be empty. |
|400 |MissingParameter.VolumeName |The required parameter VolumeName is not supplied. |The volume name cannot be empty. |
|400 |MissingParameter.VolumeType |The required parameter VolumeType is not supplied. |The volume type cannot be empty. |
|403 |InvalidInstance.RequestForbidden |Request is forbidden by the server. |The specified resource can no longer be used because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidKeyPair.NotFound |The specified KeyPair does not exist. |The specified key pair does not exist. |
|404 |InvalidVolume.NotFound |The specified volume does not exist. |The specified volume does not exist. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |InvalidDedicatedHost.Expired |The specified dedicated host has expired. |The dedicated host has expired. |
|412 |InvalidImage.HostnameMismatch |The hostname of the current instance can not be applied to the image you choose. |The instance hostname does not match the selected image. |
|412 |InvalidImage.InstanceTypeMismatch |The specified image and instance type do not match. |The specified image does not support the specified instance type. |
|412 |InvalidImageId.KeepImageCredentialMismatch |The specified ImageId and KeepImageCredential do not match. |The specified ImageId and KeepImageCredential do not match. |
|412 |InvalidInstance.Expired |The specified instance has expired. |The instance has expired. |
|412 |InvalidKeyPairName.KeepImageCredentialMismatch |The specified KeyPairName and KeepImageCredential do not match. |The specified KeyPairName and KeepImageCredential do not match. |
|412 |InvalidPassword.KeepImageCredentialMismatch |The specified Password and KeepImageCredential do not match. |The specified Password and KeepImageCredential do not match. |
|412 |InvalidSnapshotZoneId.Mismatch |The specified ZoneId does not match the snapshot ZoneId. |The specified ZoneId does not match the snapshot ZoneId. |
|412 |InvalidVolumeSize.ImageSizeMismatch |The specified system disk size is smaller than the image file size. |The specified system volume capacity is smaller than the image file size. |
|412 |InvalidVolumeType.ImageMismatch |The specified VolumeType and Image do not match. |The specified volume type and image do not match. |
|412 |OperationDenied.InstanceIsCreatingImage |The specified operation is denied as your instance is creating image. |The specified operation is rejected because the instance is being used to create a custom image. |
|412 |OperationDenied.ResourceCreatedByOtherService |The specified operation is denied as your resource is created by other service. You can check system tags to find the service. |The specified operation is rejected because your resource was created by another service. You can query the corresponding service based on the system tag of the resource. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
