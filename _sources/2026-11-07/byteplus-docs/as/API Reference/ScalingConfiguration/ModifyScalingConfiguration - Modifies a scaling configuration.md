---
title: "ModifyScalingConfiguration - Modifies a scaling configuration"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration"
---

Modify a scaling configuration. If you do not specify optional parameters, optional parameters remain unchanged. For operation instructions and precautions, see [Managing scaling configurations](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyScalingConfiguration&groupName=%E4%BC%B8%E7%BC%A9%E9%85%8D%E7%BD%AE&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|zGEuT4">必选</span> `Sample value: ModifyScalingConfiguration`

The operation that you want to perform. Valid value: ModifyScalingConfiguration.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|qlqXvc">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingConfigurationId ** <span data-label="purple">string </span><span data-api-tag="require|X0C4Mz">必选</span> `Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID. You can call [DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) to query the scaling configuration ID.



**KeyPairName ** <span data-label="purple">string </span>`Optional` `Sample value: kp-test-123`

When you use "SSH Key" to log in to the instance, enter the name of the key pair.

If the `KeyPairName` and `Password` parameters are specified at the same time, only the `KeyPairName` parameter takes effect.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The project to which the instance created based on the scaling configuration belongs. A resource can belong to only one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**InstanceTypeOverrides.N.PriceLimit ** <span data-label="purple">float[] </span>`Optional` `Sample value: 0.01`

The maximum hourly price for the spot instance type.


* Parameter \- N: Specifies the serial number of the instance type. Valid value: 1–10.

* Value \- PriceLimit: The maximum hourly price for the spot instance type. Value: greater than 0, with a maximum of 3 decimal places.

* Separate multiple prices with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>SpotStrategy</code> is set to SpotWithPriceLimit.</div>




**InstanceTypeOverrides.N.InstanceType ** <span data-label="purple">string[] </span>`Optional` `Sample value: ecs.g2i.large`

The type of spot instances.


* Parameter \- N: Specifies the serial number of the instance type. Valid value: 1–10.

* Parameter \- InstanceType: The type of spot instances.

* Use & to separate multiple types.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>SpotStrategy</code> is set to SpotWithPriceLimit.</div>




**SpotStrategy ** <span data-label="purple">string </span>`Optional` `Sample value: NoSpot`

The spot policy of the instances. Value:


* NoSpot: Creates regular Pay\-as\-you\-go instances.

* SpotAsPriceGo: Creates spot instances with auto\-bidding that follows the current market price.

* SpotWithPriceLimit: Creates spot instances with a user\-defined maximum bid price.



**Ipv6AddressCount ** <span data-label="purple">integer </span>`Optional` `Sample value: 0`

Whether to assign IPv6 addresses to the instance's network interfaces. Value:


* 0: Do not assign IPv6 addresses.

* 1: Assign IPv6 addresses. The system automatically allocates an IPv6 CIDR block.



**Eip.SecurityProtectionTypes.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: AntiDDoS_Enhanced`

The security protection type of EIP.


* N specifies the serial number of the protection type. Currently, only 1 is supported.

* Valid values:

   * AntiDDoS_Enhanced: EIP of the Security Enhanced type, which can be added to an Anti\-DDoS Origin instance.

   * If no argument is passed in, this indicates applying for an EIP of the basic protection type.



**SecurityGroupIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: sg-3ti78x9h8t4bw*****`

The ID of the security group associated with the instance's primary network interface. You can call [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) to query the security group ID. Value:


* Parameter \- N: The serial number of the security group associated with the primary network interface. Up to 5 security groups can be associated. Valid values: 1 \- 5.

* Parameter \- SecurityGroupId: The ID of the Nth security group associated with the primary network interface.

* Separate multiple security group IDs with ampersands (&).



**HpcClusterId ** <span data-label="purple">string </span>`Optional` `Sample value: hpcCluster-ycdj7d9ios38dfny****`

The ID of the HPC cluster to which the instance belongs.

This parameter is valid only when `InstanceTypes.N` is set to HPC\-optimized instance type.



**Eip.BandwidthPackageId ** <span data-label="purple">string </span>`Optional` `Sample value: bwp-2zeo05qre24nhrqpy****`

ID of the shared bandwidth package. This means you add the EIP to the specified shared bandwidth package. You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) operation to query IDs of shared bandwidth packages. To associate an EIP with a shared bandwidth package, the following conditions are required:


* The EIP and bandwidth package must be of the same security mode.

* The EIP and shared bandwidth package must be of the same ISP type.

* Shared bandwidth package is of the IPv4 type.



**Eip.SecurityProtectionInstanceId ** <span data-label="purple">integer </span>`Optional` `Sample value: 193`

The security package ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Eip.SecurityProtectionTypes.N</code> is not empty, this parameter is required.</div>




**Tags ** <span data-label="purple">string </span>`Optional` `Sample value: "k1":"v1"`

The tags for instances created based on the scaling configuration. Tags are passed in as key\-value pairs. You can pass in up to 20 key\-value pairs. Key naming rules are as follows:


* Key naming rules:

   * It cannot start with `volc:` or `sys:` in any case form.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Tags with keys prefixed with <code>volc:</code> or <code>sys:</code> are reserved for system use. You cannot create tags that use these prefixes.      </div>
      

   * It can contain only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@".

   * It must be 1 to 128 characters in length.

> Duplicate tag keys are not allowed within the same scaling configuration.


* Value naming rules:

   * Only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

   * It can be empty. Length limit: 0\-256 characters.



**Volumes.N.ExtraPerformanceTypeId ** <span data-label="purple">string[] </span>`Optional` `Sample value: Volumes.2.ExtraPerformanceTypeId=IOPS`

This parameter allows you to purchase additional performance for the volume. This parameter is supported only for ESSD FlexPL volumes.


* Parameter \- N: Specifies the serial number of the volume. No. 1 represents the system volume. No. 2 or greater represents a data volume. Only data volumes support additional performance packages. Valid range: 2–16

* Value \- ExtraPerformanceTypeId indicates the additional performance package type of the Nth volume:

   * IOPS: IOPS type. Use the ExtraPerformanceIOPS parameter.

   * Balance: balanced type. Use the ExtraPerformanceIOPS parameter.

   * Throughput: throughput type. Use the ExtraPerformanceThroughputMB parameter.



**Volumes.N.ExtraPerformanceThroughputMB ** <span data-label="purple">integer[] </span>`Optional` `Sample value: Volumes.2.ExtraPerformanceThroughputMB=100`

This parameter allows you to configure the throughput performance value for the additional performance package of the volume. Unit: MB/s. This parameter is supported only for ESSD FlexPL volumes.


* Parameter \- N: Specifies the serial number of the volume. No. 1 represents the system volume. No. 2 or greater represents a data volume. Only data volumes support additional performance packages. Valid range: 2–16

* Value \- ExtraPerformanceThroughputMB indicates the throughput performance value for the additional performance package of the Nth volume:

   * Throughput：1\-650



**Volumes.N.ExtraPerformanceIOPS ** <span data-label="purple">integer[] </span>`Optional` `Sample value: Volumes.2.ExtraPerformanceIOPS=100`

This parameter allows you to configure the IOPS performance value for the additional performance package of the volume. This parameter is supported only for ESSD FlexPL volumes.


* Parameter \- N: Specifies the serial number of the volume. No. 1 represents the system volume. No. 2 or greater represents a data volume. Only data volumes support additional performance packages. Valid range: 2–16

* Value \- ExtraPerformanceIOPS indicates the IOPS performance value for the additional performance package of the Nth volume:

   * IOPS: 1\-50000

   * Balance: 1\-50000



**Eip.ReleaseWithInstance ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether the EIP is deleted along with the instance.

This parameter takes effect only when an instance with a Pay\-as\-you\-go EIP is deleted in the ECS console. For the retention rules of EIPs when instances are removed from the scaling group, see the detailed description in [Instance management](https://docs.byteplus.com/en/docs/as/Managing-instances). Value:


* true: The EIP is deleted along with the instance.

* false: The EIP is not deleted when the instance is deleted.



**Eip.Bandwidth ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The peak bandwidth of the EIP. Unit: Mbps. Value:


* When Eip.BillingType is set to PostPaidByBandwidth, the value ranges from 1 to 500.

* When Eip.BillingType is set to PostPaidByTraffic, the value ranges from 1 to 200.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the specified scaling configuration already has an EIP configured, setting this parameter to 0 deletes the EIP configuration. If no EIP is configured, specifying values for Eip.Bandwidth, Eip.ISP, or Eip.BillingType adds an EIP configuration to the scaling configuration. Unspecified parameters use their default values.</div>




**Eip.BillingType ** <span data-label="purple">string </span>`Optional` `Sample value: PostPaidByBandwidth`

The billing method of the EIP. Valid values:


* PostPaidByBandwidth: Pay\-as\-you\-go\-Pay\-by\-bandwidth.

* PostPaidByTraffic: Pay\-as\-you\-go\-Pay\-by\-data\-transfer.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To enable automatic allocation of an EIP when an instance joins the scaling group, you must configure at least one of Eip.Bandwidth, Eip.ISP, or Eip.BillingType. If none are configured, no EIP will be allocated.</div>




**Eip.ISP ** <span data-label="purple">string </span>`Optional` `Sample value: BGP`

The ISP type. Valid values:


* BGP: BGP line.

* If your account has applied for static single\-line access, the ISP parameter can also be set to ChinaMobile (China Mobile), ChinaTelecom (China Telecom), or ChinaUnicom (China Unicom).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To enable automatic allocation of an EIP when an instance joins the scaling group, you must configure at least one of Eip.Bandwidth, Eip.ISP, or Eip.BillingType. If none are configured, no EIP will be allocated.</div>




**HostName ** <span data-label="purple">string </span>`Optional` `Sample value: instance-host-name`

Instance hostname Value:


* Linux instance

   * Periods can be used to separate the hostname into multiple segments. Each segment can contain letters, digits, or hyphens "\-".

   * The hostname cannot start or end with a period "." or hyphen "\-", and periods "." or hyphens "\-" cannot be used consecutively.

   * The length of the hostname for Linux systems is limited to 2 to 63 characters.

* Windows instances

   * Letters, numbers, or hyphens "\-" are allowed. The name can not be comprised of numbers only.

   * The hostname cannot start or end with a hyphen "\-", and hyphens "\-" cannot be used consecutively.

   * The length of the hostname for Windows systems is limited to 2 to 15 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can configure sequential and unique instance names or hostnames for instances created during scale\-out. For configuration rules, see <a href="https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances">Configuring sequential and unique instance names or hostnames</a>.</div>




**ImageId ** <span data-label="purple">string </span>`Optional` `Sample value: image-ybmhzqo8u4l8j1ii****`

The ID of the image. This parameter specifies the image resource used by the scaling group to create instances automatically. You can call [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) to query image IDs.



**InstanceDescription ** <span data-label="purple">string </span>`Optional` `Sample value: ECS instance.`

The description of the instance. Valid range:


* Cannot start with a number or a hyphen (\-).

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The length is limited to 0 ~ 255 characters.



**InstanceName ** <span data-label="purple">string </span>`Optional` `Sample value: instance-test`

The instance name. Valid range:


* Start with a letter or Chinese.

* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can configure sequential and unique instance names or hostnames for instances created during scale\-out. For configuration rules, see <a href="https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances">Configuring sequential and unique instance names or hostnames</a>.</div>




**InstanceTypes.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: ecs.g1.large`

The list of instance types. You can call [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) to query the stock information of instance types.



**Password ** <span data-label="purple">string </span>`Optional` `Sample value: password@123`

The password required for logging in to the instance as the root user.


* The length is limited to 8 ～ 30 characters

* A password can only consist of uppercase letters, lowercase letters, numbers, and special characters, and must include at least three of these elements

* Special characters allowed: `~!@#$%^&\*()_\-+= |

* A password can not start with "/" or "$6$"



**ScalingConfigurationName ** <span data-label="purple">string </span>`Optional` `Sample value: scaling-config-test`

The name of the scaling configuration. Within the same region and scaling group, the scaling configuration name must be unique. Valid value:


* It must start with a letter or Chinese character.

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The name must be 1 to 128 characters in length.

* Special characters are currently not supported.



**SecurityEnhancementStrategy ** <span data-label="purple">string </span>`Optional` `Sample value: Active`

Whether to enable security enhancement. Value:


* Active: Enables security enhancement. This feature is effective for public images only.

* InActive: Disables security enhancement. This feature is effective for all images.



**UserData ** <span data-label="purple">string </span>`Optional` `Sample value: ZWNobyBoZWxsbyBlY3Mh`

Instance custom data. The custom data for an instance must be encoded in Base64 format, and the data can not exceed 16 KB before Base64 encoding.

If left blank, the parameter defaults to an empty value.



**Volumes.N.DeleteWithInstance ** <span data-label="purple">boolean[] </span>`Optional` `Sample value: true`

Whether the volume is released with the instance:


* Parameter \- N: Specifies the serial number of the volume. No. 1 represents the system volume. No. 2 or greater represents a data volume. Valid value: 1 \- 15.

* Parameter \- DeleteWithInstance: Whether the volume is released along with the instance.

   * true: The volume is released with the instance.

   * false: The volume is not released with the instance.

* When "false" is passed in, this configuration is invalid on the system volume. By default, the system volume is released with the instance and can not be retained.



**Volumes.N.Size ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 100`

The volume capacity. Unit: GiB.


* Parameter \- N: Specifies the serial number of the volume. No. 1 represents the system volume. No. 2 or greater represents a data volume. Valid value: 1\-15.

* Value \- Size: The capacity of the Nth volume. Unit: GiB.

   * Valid value for the system volume: 10 \- 500.

   * Valid value for data volumes: 10 \- 8192.

* Separate multiple volumes with ampersands (&).



**Volumes.N.VolumeType ** <span data-label="purple">string[] </span>`Optional` `Sample value: PTSSD`

The volume type:


* Parameter \- N: Specifies the serial number of the volume. No. 1 represents the system volume. No. 2 or greater represents a data volume. Valid value: 1\-15.

* Parameter \- VolumeType: The type of the Nth volume. Valid value:

   * PTSSD: PTSSD.

   * ESSD_PL0: ESSD PL0.

* Separate multiple volumes with ampersands (&).



**ZoneId**<span data-label="purple"> string </span>`Optional Sample value: cn-beijing-a`

The availability zone ID of the scaling configuration.



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
GET /?Action=ModifyScalingConfiguration&ScalingConfigurationId=scc-ybmt16auaugh9zfy****&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T095055Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240507175103018142130120A2A064",
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
|400 |InvalidScalingConfigurationName.Malformed |The specified ScalingConfigurationName is malformed. |The specified scaling configuration name is invalid. |
|400 |MissingParameter.ScalingConfigurationId |The required parameter ScalingConfigurationId is not supplied. |The scaling configuration ID cannot be empty. |
|400 |LimitExceeded.ScalingConfigurationName |You've reached the limit on the length of ScalingConfigurationName. |The scaling configuration name has reached the upper limit in length. |
|400 |MissingParameter.InstanceName |The required parameter InstanceName is not supplied. |Instance name can not be empty. |
|400 |InvalidInstanceName.Malformed |The specified InstanceName is malformed. |The specified instance name is invalid. |
|400 |InvalidInstanceDescription.Malformed |The specified InstanceDescription is malformed. |The specified instance description is not valid. |
|400 |LimitExceeded.InstanceDescription |You've reached the limit on the length of InstanceDescription. |The instance description has reached the upper limit in length. |
|400 |InvalidUserData.Malformed |The specified UserData is malformed. |The specified UserData is invalid. |
|400 |LimitExceeded.UserData |You've reached the limit on the size of UserData. |UserData has reached the upper limit in length. |
|400 |InvalidSecurityEnhancementStrategy |The specified SecurityEnhancementStrategy is unsupported. |The specified security enhancement policy is not supported. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of Tags that you can create. |The upper limit of tags that you can create is reached. |
|400 |TagKey.ForbidDelete |The previous system TagKey is not allowed to be deleted. |System tags cannot be deleted. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidEipISP |The specified Eip ISP is unsupported. |The specified EIP line type is not supported. |
|400 |InvalidKeyPairForWindows.Unsupported |The OSType of this specified instance is Windows, which does not support key pairs. |The Windows operating system does not support key pairs. |
|400 |InvalidPassword.Malformed |The specified Password is malformed. |The specified password is invalid. |
|400 |MissingParameter.PasswordAndKeyPair |The parameter Password and KeyPair are both empty. |The password and key pair cannot both be empty. |
|400 |LimitExceeded.SecurityGroupIds |You've reached the limit on the number of SecurityGroupIds. |The number of security groups that can be configured has reached the upper limit. |
|400 |InvalidEipBandwidthPackage.Mismatch |The specified Eip does not match the BandwidthPackage [%s]. |The specified EIP and shared bandwidth package do not match. |
|400 |InvalidEipBandwidth.Malformed |The specified Eip Bandwidth is malformed. |The specified EIP bandwidth is invalid. |
|400 |InvalidEipSecurityProtectionType |The specified Eip SecurityProtectionType is unsupported. |The specified EIP security protection type is not supported. |
|400 |InvalidEipBillingType |The specified Eip BillingType is unsupported. |The specified EIP billing method is not supported. |
|400 |InvalidIpv6AddressCount.Malformed |The specified Ipv6AddressCount is malformed. |The specified IPv6 address is invalid. |
|400 |InvalidSubnetIdIpv6.Malformed |The specified Subnet %s Ipv6 is unsupported. |The specified subnet IPv6 address is invalid. |
|400 |InvalidHostName.Malformed |The specified HostName is malformed. |The specified hostname is invalid. |
|400 |MissingParameter.HpcClusterId |The specified InstanceType [%s] required parameter HpcClusterId. |You must specify the ID of the HPC cluster for the specified instance type. |
|400 |LimitExceeded.Volumes |You've reached the limit on the number of Volumes that InstanceType [%s] can attach, max [%d]. |The maximum number of disks that can be mounted for the instance type has been reached. |
|400 |InvalidVolumeType.InstanceTypeMismatch |The specified VolumeType [%s] does not match InstanceType [%s]. |The specified disk type does not match the instance type. |
|400 |InvalidVolumeSize.Malformed |The specified VolumeSize is malformed. |The specified disk size is invalid. |
|400 |InvalidVolumeSize.ImageSizeMismatch |The specified system disk size is smaller than the image file size. |The specified system volume size is smaller than the image size. |
|400 |InvalidInstanceType.ImageIdMismatch |The specified InstanceType [%s] does not match ImageId [%s]. |The specified instance type and image ID do not match. |
|400 |InvalidVolumeTypes.Mismatch |Mismatch between attached Volume types. |The disk type does not match. |
|400 |InvalidSpotStrategy |The specified SpotStrategy is unsupported. |The specified instance spot policy is not supported. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|400 |LimitExceeded.InstanceTypes |You've reached the limit on the number of InstanceType, max [%d]. |The maximum number of instance types has been reached. |
|400 |MissingParameter.VolumeType |The specified parameter VolumeType is not supplied. |The disk type cannot be empty. |
|400 |MissingParameter.EipSecurityProtectionInstanceId |The required parameter EIP SecurityProtectionInstanceId is not supplied. |The security package ID of the EIP cannot be empty. |
|400 |MissingParameter.Volumes |The required parameter Volumes is not supplied. |The disk information cannot be empty. |
|400 |MissingParameter.InstanceType |The required parameter InstanceType is not supplied. |The instance type cannot be empty. |
|400 |InvalidTags.Malformed |The specified Tags are malformed. |The specified tag is invalid. |
|400 |InvalidSystemVolumeForExtraPerformance.Unsupported |The specified SystemVolume does not support extra performance. |The specified system volume does not support purchase of additional performance. |
|400 |InvalidVolumeTypeForExtraPerformance.Unsupported |The specified VolumeType does not support extra performance. |The specified volume type does not support purchase of additional performance. |
|400 |InvalidSnapshotStatus |The status of the specified snapshot does not support this request. |The specified snapshot status does not support this operation. |
|400 |InvalidVolumeTypeForSnapshot.UnSupported |The specified VolumeType cannot be used for create snapshot. |The specified volume type does not support snapshot. |
|400 |InvalidInstancePriceLimit.Malformed |The specified PriceLimit is malformed. |The specified spot instance price is invalid. |
|400 |InvalidInstanceType.Conflict |The specified InstanceType is already existed. |The specified instance type already exists. |
|400 |InvalidVolumeSizeForExtraPerformance.Unsupported |The specified VolumeSize does not support extra performance. |The specified volume capacity does not support purchase of additional performance. |
|400 |LimitExceeded.MinimumExtraPerformanceIOPS |The number of specified ExtraPerformanceIOPS exceeds the minimum limit. |The specified additional performance IOPS exceeds the minimum limit. |
|400 |LimitExceeded.MaximumExtraPerformanceIOPS |The number of specified ExtraPerformanceIOPS exceeds the maximum limit. |The specified additional performance IOPS exceeds the maximum limit. |
|400 |LimitExceeded.MinimumExtraPerformanceThroughputMB |The number of specified ExtraPerformanceThroughputMB exceeds the minimum limit. |The specified additional performance throughput exceeds the minimum limit. |
|400 |LimitExceeded.MaximumExtraPerformanceThroughputMB |The number of specified ExtraPerformanceThroughputMB exceeds the maximum limit. |The specified additional performance throughput exceeds the maximum limit. |
|400 |LimitExceeded.ExtraPerformanceThroughput |You've reached the limit on the number of ExtraPerformanceThroughput that you can set. |The throughput has reached the maximum limit. No additional performance required. |
|400 |InvalidExtraPerformanceTypeId.Malformed |The specified ExtraPerformanceTypeId is malformed. |The specified type of additional performance package is invalid. |
|400 |InvalidDeploymentSetId.Malformed |The specified DeploymentSetId is malformed. |The specified deployment set ID is invalid |
|400 |InvalidDeploymentSetGroupNumber |The specified DeploymentSetGroupNumber is invalid. |The specified deployment set group is invalid. |
|404 |InvalidScalingConfiguration.NotFound |The specified ScalingConfiguration [%s] does not exist. |The specified scaling configuration does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidKeyPair.NotFound |The specified KeyPair does not exist. |The specified key pair does not exist. |
|404 |InvalidImageId.NotFound |The specified ImageId does not exist. |The specified image ID does not exist. |
|404 |InvalidZoneId.NotFound |The specified ZoneId does not exist. |The specified availability zone ID does not exist. |
|404 |InvalidEipBandwidthPackageId.NotFound |The specified Eip BandwidthPackageId [%s] does not exist. |The specified EIP bandwidth package ID does not exist. |
|404 |InvalidHpcCluster.NotFound |The specified HpcCluster does not exist. |The specified HPC cluster does not exist. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType [%s] does not exist. |The specified instance type does not exist. |
|404 |InvalidSubnetId.NotFound |The specified SubnetId [%s] does not exist. |The specified subnet ID does not exist. |
|404 |InvalidSecurityGroupId.NotFound |The specified SecurityGroupId [%s] does not exist. |The specified security group ID does not exist. |
|404 |InvalidSnapshot.NotFound |The specified Snapshot does not exist. |The specified snapshot does not exist. |
|404 |InvalidDeploymentSetId.NotFound |The specified DeploymentSetId does not exist. |The specified deployment set does not exist |
|404 |InvalidSupportVolume.NotFound |The specified Support volume type does not exist. |The specified volume type is not supported |
|409 |InvalidScalingConfigurationName.Conflict |The specified ScalingConfigurationName already exists. |The specified scaling configuration name already exists. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|409 |InvalidInstanceTypesAndInstanceTypeOverrides.Conflict |The specified parameter InstanceTypes and InstanceTypeOverrides is duplicate. |The instance type and instance type extension parameters conflict. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|412 |InvalidHpcCluster.InstanceTypeIdMismatch |The specified HpcClusterId does not match the InstanceTypeId [%s]. |The specified HPC cluster does not match the instance type. |
|412 |InvalidHpcCluster.SubnetMismatch |The specified HpcClusterId does not match the subnet of the group. |The subnet of the specified HPC cluster does not match the scaling group. |
|412 |InvalidInstanceTypeId.DeploymentSetIdMismatch |The specified instance type [%s] and deployment set id do not match. |The specified instance type cannot be added to the deployment set. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
