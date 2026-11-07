---
title: "EnableScalingGroup - Enables a scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/EnableScalingGroup"
---

Enable a scaling group. For operation instructions and precautions, see [Enabling scaling groups](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-group).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=EnableScalingGroup&groupName=%E4%BC%B8%E7%BC%A9%E7%BB%84&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|UEoQXv">必选</span> `Sample value: EnableScalingGroup`

The action that you want to perform. Value: EnableScalingGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|TDLjDK">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|A3x04e">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingGroupId ** <span data-label="purple">string </span>`String example: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=EnableScalingGroup&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T093415Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2024050717344620200612623946F5B5",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingGroupId": "scg-ybmssdnnhn5pkgyd****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidScalingGroup.InvalidStatus |The specified ScalingGroup is not in the correct status. |The current status of the specified scaling group does not support this operation. |
|400 |MissingParameter.ScalingGroupId |The required parameter ScalingGroupId is not supplied. |The scaling group ID cannot be empty. |
|400 |InvalidLaunchTemplateId.VersionMismatch |The specified LaunchTemplateId [%s] and LaunchTemplateVersion [%s] are mismatched. |The ID and version of the specified launch template do not match. |
|400 |MissingParameter.ScalingConfigurationOrLaunchTemplate |The parameters ScalingConfiguration and LaunchTemplate can't be both empty. |The scaling configuration and launch template cannot both be empty. |
|400 |MissingParameter.LaunchTemplateImageId |The required parameter LaunchTemplate ImageId is not supplied. |The ID of the image associated with the specified launch template cannot be empty. |
|400 |MissingParameter.LaunchTemplateInstanceType |The required parameter LaunchTemplate InstanceType is not supplied. |The instance type of the specified launch template cannot be empty. |
|400 |InvalidLaunchTemplateVolumeTypes.Mismatch |The specified LaunchTemplate VolumeTypes are mismatched. |The volume type of the specified launch template is invalid. |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|404 |InvalidLaunchTemplateImageId.NotFound |The specified LaunchTemplate ImageId does not exist. |The ID of the image associated with the specified launch template does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
