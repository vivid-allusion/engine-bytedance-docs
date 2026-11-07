---
title: "ModifyInstanceAttribute - Modifies instance information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute"
---

Call the ModifyInstanceAttribute operation to modify the information of an ECS instance, including the name, description, password, hostname, and custom data.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

Before you modify the login password, hostname, or custom data of an instance, check the relevant documentation first to fully understand the constraints, limitations, and precautions involved. This helps ensure the accuracy and compliance of the operation.


* [Resetting login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) (`Password`)

* [Changing instance hostname](https://docs.byteplus.com/en/docs/ecs/Changing-the-hostname-of-an-instance) (`Hostname`)

* [Changing instance custom data](https://docs.byteplus.com/en/docs/ecs/Configuring-custom-data) (`UserData`)

> After you restart the instance, new custom data will be displayed on the instance, but data scripts will not be executed.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

When you call this operation, if you do not pass in optional parameters, the original configuration is retained.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstanceAttribute&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string </span><span data-api-tag="require|f6kh78">必选</span> `Sample value: ModifyInstanceAttribute`

The operation that you want to perform. Valid value: ModifyInstanceAttribute.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|LcStOU">必选</span>   `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure request idempotency. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**CpuOptions.TopologyType ** <span data-label="purple">string </span>`Optional` `Sample value: DiscreteCoreToHTMapping`

The CPU topology mode. Valid values:


* ContinuousCoreToHTMapping: HT continuous mode.

* DiscreteCoreToHTMapping: HT discrete mode.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, please contact your account manager to apply.</div>




**DeletionProtection ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

The attribute of instance deletion protection. Specify whether to delete the instance through the console or API. Valid values:


* true: Enable instance deletion protection.

* false: Disable instance deletion protection.



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: ECS instance for testing.`

The description of the instance.


* Must start with a letter or a Chinese character.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When an empty string is passed in, the existing description is cleared.</div>




**EnableJumboFrame ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether jumbo frames are enabled for the instance. Valid values:


* false: Jumbo frames are not enabled. The MTU value of all network interfaces of the instance is 1500.

* true: Jumbo frames are enabled. The MTU value of all network interfaces of the instance is 8500.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is only supported for certain instances. For instances that support jumbo frames, see <a href="https://docs.byteplus.com/en/docs/ecs/Enabling_or_Disabling_jumbo_frames">Enabling/disabling jumbo frames</a>.</div>




**Hostname ** <span data-label="purple">string </span>`Optional Sample value: instance-host-name`

The hostname is the internal computer name within the operating system of an instance.


* Linux instances:

   * Letters, numbers, periods ".", and hyphens "\-" are allowed.

   * Cannot start or end with a hyphen or period. Hyphens and periods cannot be used consecutively.

   * The length limit is 2 to 63 characters.

* Windows instances:

   * Letters, numbers, and hyphens ("\-") are allowed, but the name cannot consist only of digits.

   * Cannot start or end with a hyphen. Hyphens cannot be used consecutively.

   * The length limit is 2 to 15 characters.



**InstanceId ** <span data-label="purple">string</span><span data-api-tag="require|xyxj7h">必选</span>  `Sample value: i-l8u10sauiu9qj0h*****`

The instance ID.



**InstanceName ** <span data-label="purple">string </span>`Optional` `Sample value: instance-test`

The instance name.


* Start with a letter or a Chinese character.

* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* It must be 1 to 128 characters in length.



**Password**<span data-label="purple"> string </span>`Optional Sample value: password@123`

The password for logging in to the instance. This parameter is required if you want to use password\-based login.


* The length limit is 8 to 30 characters.

* Passwords can only consist of uppercase letters, lowercase letters, numbers, and special characters, and must include at least three of these elements.

* Valid special characters: `~!@#$%^&\*()_\-+=|{}[]:;'<\>,.?/

* The password cannot start with "/" or "$6$".



**UserData ** <span data-label="purple">string </span>`Optional` `Sample value: IyEvYmluL2Jhc2gKdG91Y2ggL3RtcC91c2VyZG******`

Instance custom data provides a feature for customizing instance startup behavior and passing in data.


* When you pass in data, the specified custom data must be Base64 encoded, and the size of the custom data before Base64 encoding must not exceed 16 KB.

* When an empty string is passed in, custom data will be cleared.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyInstanceAttribute&Version=2020-04-01&InstanceId=i-l8u10sauiu9qj0h*****&Password=password@123 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
        "ResponseMetadata": {
                "RequestId": "20211104180426010194099035220C****",
                "Action": "ModifyInstanceAttribute",
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


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidCpuAccelerator.Malformed |The specified CpuAccelerator is malformed. |The specified CpuAccelerator is invalid. |
|400 |InvalidDedicatedHostStatus.Unsupported |The status of the specified dedicated host does not support this request. |The dedicated host in the current status does not support this action. |
|400 |InvalidEnableJumboFrameForModifyInstanceAttribute.Unsupported |The specified EnableJumboFrame cannot be used for ModifyInstanceAttribute. |Currently, modifying the EnableJumboFrame configuration is not supported. |
|400 |InvalidHostname.Malformed |The specified Hostname is malformed. |The specified hostname is invalid. |
|400 |InvalidInstanceDescription.Malformed |The specified InstanceDescription is malformed. |The specified instance description is not valid. |
|400 |InvalidInstanceName.Malformed |The specified InstanceName is malformed. |The specified instance name is invalid. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidPassword.Malformed |The specified password is malformed. |The specified password format is invalid. |
|400 |InvalidTopologyType.Malformed |The specified TopologyType is malformed. |The specified TopologyType is invalid. |
|400 |InvalidUserData.Malformed |The specified UserData is malformed. |The specified UserData is invalid. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|400 |MissingParameter.InstanceName |The required parameter InstanceName is not supplied. |The instance name cannot be empty. |
|403 |InvalidChargeTypeForDeletionProtection.Unsupported |Deletion protection is only valid for postPaid instance. |The deletion protection feature can only be used on general pay\-as\-you\-go resources. |
|403 |InvalidInstance.RequestForbidden |Request is forbidden by the server. |The specified resource can no longer be used because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidResetAuthenticationAgent.NotFound |The specified reset\-authentication agent does not install on the instance. |The specified password\-reset plugin does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |InvalidDisableJumboFrame.VrdmaMismatch |The specified request includes an unsupported operation. It is not supported to disable jumbo frame with vRDMA ENI on the ECS. |You must disable vRDMA ENI before disabling JumboFrame. |
|412 |OperationDenied.ResourceCreatedByOtherService |The specified operation is denied as your resource is created by other service. You can check system tags to find the service. |The specified operation is rejected because your resource was created by another service. You can query the corresponding service based on the system tag of the resource. |
|412 |OperationDenied.EnableJumboFrameForceDisabled |The specified operation is denied because Jumbo Frame is force\-disabled for the account. |The specified operation is rejected because JumboFrame is forcibly disabled for the current account. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again. If multiple attempts fail, submit a ticket. |
