---
title: "EnableScalingConfiguration - Enables a scaling configuration"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/EnableScalingConfiguration"
---

Associate a scaling configuration with a scaling group.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* The availability zone selected for the scaling configuration must be the availability zone of the scaling group's subnet. Otherwise, subsequent instance scale\-out will fail.

* A scaling group can be associated with only one scaling configuration. After a new scaling configuration is associated with the scaling group, it takes effect only the next time an instance is created and does not affect existing instances in the scaling group.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=EnableScalingConfiguration&groupName=%E4%BC%B8%E7%BC%A9%E9%85%8D%E7%BD%AE&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|dxtKBI">必选</span> `Sample value: EnableScalingConfiguration`

The operation that you want to perform. Valid value: EnableScalingConfiguration.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|BbrnL0">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span><span data-api-tag="require|xsT9s9">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**ScalingConfigurationId ** <span data-label="purple">string </span><span data-api-tag="require|4j31qU">必选</span> `Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID. You can call [DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) to query the scaling configuration ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScalingConfigurationId ** <span data-label="purple">string </span>`Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=EnableScalingConfiguration&ScalingConfigurationId=scc-ybmt16auaugh9zfy****&ScalingGroupId=scg-ybmssdnnhn5pkgyd****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T095605Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507175620023114149131892215",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScalingConfigurationId": "scc-ybmt16auaugh9zfy****"
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
|400 |MissingParameter.ScalingConfigurationId |The required parameter ScalingConfigurationId is not supplied. |The scaling configuration ID cannot be empty. |
|400 |InvalidScalingConfiguration.ScalingGroupMismatch |The specified ScalingConfiguration [%s] does not match ScalingGroup [%s]. |The specified scaling configuration does not match the scaling group. |
|400 |InvalidSubnetIdIpv6.Malformed |The specified Subnet %s Ipv6 is unsupported. |The specified subnet IPv6 address is invalid. |
|400 |InvalidConfigInstanceType |The ScalingGroup InstanceType [%s] is not in Configuration InstanceTypes. |The instance type of the scaling group is not included in the scaling configuration. |
|400 |InvalidDeploymentSetId.Malformed |The specified DeploymentSetId is malformed. |The specified deployment set ID is invalid |
|404 |InvalidScalingGroupId.NotFound |The specified ScalingGroup [%s] does not exist. |The specified scaling group does not exist. |
|404 |InvalidScalingConfiguration.NotFound |The specified ScalingConfiguration [%s] does not exist. |The specified scaling configuration does not exist. |
|404 |InvalidSubnetId.NotFound |The specified SubnetId [%s] does not exist. |The specified subnet ID does not exist. |
|404 |InvalidHpcCluster.NotFound |The specified HpcCluster does not exist. |The specified HPC cluster does not exist. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType [%s] does not exist. |The specified instance type does not exist. |
|404 |InvalidImageId.NotFound |The specified ImageId does not exist. |The specified image ID does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSecurityGroupId.NotFound |The specified SecurityGroupId [%s] does not exist. |The specified security group ID does not exist. |
|404 |InvalidKeyPair.NotFound |The specified KeyPair does not exist. |The specified key pair does not exist. |
|404 |InvalidDeploymentSetId.NotFound |The specified DeploymentSetId does not exist. |The specified deployment set does not exist |
|404 |InvalidSupportVolume.NotFound |The specified Support volume type does not exist. |The specified volume type is not supported |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|412 |InvalidInstanceTypeId.DeploymentSetIdMismatch |The specified instance type [%s] and deployment set id do not match. |The specified instance type cannot be added to the deployment set. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
