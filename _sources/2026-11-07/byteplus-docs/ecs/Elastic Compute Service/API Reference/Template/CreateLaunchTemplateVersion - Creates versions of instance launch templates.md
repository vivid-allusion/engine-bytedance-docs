---
title: "CreateLaunchTemplateVersion - Creates versions of instance launch templates"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplateVersion"
---

Call the CreateLaunchTemplateVersion operation to create a version based on the specified instance launch template. Each instance launch template can have up to 30 versions at the same time. For operation instructions and precautions, refer to [Creating versions of instance launch templates](https://docs.byteplus.com/en/docs/ecs/Creating-launch-template-versions).

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

When you create an instance launch template, instance\-related parameters are not restricted or validated. Related parameters are validated only when you create an instance using this template. If validation fails, the instance creation fails.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateLaunchTemplateVersion&groupName=%E5%90%AF%E5%8A%A8%E6%A8%A1%E7%89%88&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|whlq5N">必选</span> `Sample value: CreateLaunchTemplateVersion`

The action that you want to perform. Value: CreateLaunchTemplateVersion.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|YqcRn8">必选</span>   `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**Volumes.N.ExtraPerformanceIOPS ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 1`

The capacity of additional IOPS (unit: ops/sec, operations per second) of the volume. Only ESSD FlexPL data volumes support additional IOPS performance. When `ExtraPerformanceTypeId` is set to `Balance` or `IOPS`, configure this parameter. The value ranges for each type of extra performance are as follows:


* IOPS: 1–50000

* Balance: 1–50000


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid value: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Volumes.N.ExtraPerformanceTypeId ** <span data-label="purple">string[] </span>`Optional` `Sample value: Balance`

The type of additional performance for the volume. This feature is only supported by ESSD FlexPL data volumes. For more information about additional performance, please refer to [Volume additional performance](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume).

Valid range:


* Balance: Balanced additional performance.

* IOPS: IOPS additional performance.

* Throughput: Additional performance related to throughput.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**DeploymentSetGroupNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

When an ECS instance is to join or adjust to a deployment set with the AvailabilityGroup policy, this parameter can be used to specify the group number of the instance within the deployment set.



**DeploymentSetId ** <span data-label="purple">string </span>`Optional` `Sample value: dps-yc1o9aahks5m57nk****`

The ID of the deployment set that the instance is added to.



**Volumes.N.SnapshotId ** <span data-label="purple">string[] </span>`Optional` `Sample value: snap-31ak39j5bh8rubsn****`

Only data volumes can be created with a snapshot. You can call the [DescribeSnapshots](https://docs.byteplus.com/en/docs/ecs/Describesnapshots) operation to query the snapshot ID.


* Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume. Therefore, you can pass in the snapshot ID for the target data volume.

* Multiple volumes are separated with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only ESSD supports volume creation using snapshots. PTSSD does not support snapshot\-related features.</div>


* <div data-tips="true" data-tips-type="tip">Only snapshots in "Available" status support new volume creation. Snapshots in statuses "Creating", "Rolling Back", "Deleting", and "Error" do not.</div>




**Volumes.N.ExtraPerformanceThroughputMB ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 1`

The capacity of additional throughput performance (unit: MB/s) for the volume. Only ESSD FlexPL data volumes support additional throughput performance. When `ExtraPerformanceTypeId` is `Throughput`, configure this parameter. Value range: 1–650.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Eip.ReleaseWithInstance**<span data-label="purple"> boolean </span>`Optional Sample value: false`

Whether the EIP is deleted along with the instance. This feature is only available for pay\-as\-you\-go EIPs. Value:


* true: The EIP is deleted along with the instance. When an instance is automatically reclaimed by the system (for example, 24 hours after unsubscription or upon expiration) or deleted via the [DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) or [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API, the EIP is released along with the instance.

* false (default): The EIP is not deleted when the instance is deleted.



**KeepImageCredential ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to keep image settings. Value:


* true: Keeps image settings. This allows you to use the password or key pair specified for the image to log in to the ECS instance.

* false (default): Does not keep image settings.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only custom images and shared images support this feature.</div>


* <div data-tips="true" data-tips-type="tip">When the value of this parameter is <code>true</code>, do not pass in <code>KeyPairName</code>.</div>




**LaunchTemplateId ** <span data-label="purple">string </span>`Optional` `Sample value: lt-ysxc16auaugh9zfy****`

The launch template ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to confirm the template.</div>


* <div data-tips="true" data-tips-type="tip">If both the values of LaunchTemplateId and LaunchTemplateName are valid, the value of LaunchTemplateId takes precedence.</div>




**Description ** <span data-label="purple">string </span>`Optional` `Sample value: ECS instance`

The description of the instance. Valid range:


* Cannot start with a number or a hyphen (\-).

* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).

* The length limit is 0 to 255 characters.

* If left blank, the parameter defaults to an empty string.



**HostName**<span data-label="purple"> string </span>`Optional Sample value: instance-host-name`

The instance hostname. Valid range:


* Periods "." are allowed to separate the string into multiple segments.

* Letters, numbers, and hyphens "\-" are allowed in each segment.

* Cannot start or end with a hyphen "\-" or period ".". Hyphens and periods cannot be used consecutively.

* The length of a hostname in the Linux system is 2 to 59 characters.

* The length of a hostname in the Windows system is 2 to 10 characters. The hostname cannot contain a period ".", and cannot consist entirely of digits.


If no argument is filled in, the hostname is automatically generated based on the following rules:


* Format: iv\- + initial hostname. For example, iv\-3tigy72q3u3vj0\*\*\*\*\*\*.

* Generation logic of the initial hostname:

* Linux instances: Extract all characters after instance ID i\-.

* Windows instances: Extract the last 12 characters after instance ID i\-.



**ImageId**<span data-label="purple"> string </span>`Optional Sample value: image-ybmhzqo8u4l8j1ii****`

The ID of the image used when the instance is started. You can query available image resources by calling the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation.



**InstanceChargeType ** <span data-label="purple">string </span>`Optional` `Sample value: PostPaid`

The billing methods for instance and volume. Value:


* PostPaid: Pay\-as\-you\-go.

* PrePaid: Subscription.

* Esi: ESI type.

* Segmented: ESI\-Segmented.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The ESI\-Segmented feature is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**InstanceName ** <span data-label="purple">string </span>`Optional` `Sample value: instance-test`

The instance name. Valid range:


* Cannot start with a number, a hyphen (\-), or an underscore (_).

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The name must be 1 to 128 characters in length.

* Special characters cannot be used. If left blank, the parameter defaults to an empty string.



**InstanceTypeId ** <span data-label="purple">string </span>`Optional` `Sample value: ecs.g1.large`

The instance type. Currently, you can only specify one instance type.

For more details about instance types, refer to [Instance type introductions](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). You can also call the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) operation to obtain the latest list of instance types.



**KeyPairName ** <span data-label="purple">string </span>`Optional` `Sample value: kp-test-123`

When you use "SSH Key" to log in to the instance, enter the name of the key pair.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the KeyPairName and Password parameters are specified at the same time, only the KeyPairName parameter takes effect.</div>




**NetworkInterfaces.N.SecurityGroupIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: NetworkInterfaces.1.SecurityGroupIds.1=sg-3ti78x9h8t4bw*****& NetworkInterfaces.2.SecurityGroupIds.1=sg-3cj59ih2v9hj46c6rr******`

The ID of the security group associated with the network interface.


* The first N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* The second N: indicates the serial number of the security group associated with the network interface. Value: 1–5.

* Value \- SecurityGroupIds: indicates the security group ID.

* Separate multiple security group IDs with ampersands (&).



**NetworkInterfaces.N.SubnetId ** <span data-label="purple">string[] </span>`Optional` `Sample value: NetworkInterfaces.1.SubnetId=subnet-3tispp1nai4e8i****& NetworkInterfaces.2.SubnetId=subnet-2ff1nczrx2lts5oxru****`

The ID of the subnet of the instance VPC. When creating an instance, you can associate secondary network interfaces with it.


* Argument \- N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* Value \- SubnetId: indicates the subnet ID of the network interface.

* Separate multiple VPC subnet IDs with ampersands (&).



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The project to which the instance belongs.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**SecurityEnhancementStrategy ** <span data-label="purple">string </span>`Optional` `Sample value: Active`

Whether to enable security enhancement. Value:


* Active: Enables security enhancement. This feature is effective for public images only.

* InActive: Disables security enhancement. This feature is effective for all images.

   When you create an instance launch template, the security enhancement type is not restricted or validated. However, if an inappropriate security enhancement type is configured in the template, you may fail to create an instance using the template.



**SpotStrategy ** <span data-label="purple">string </span>`Optional` `Sample value: NoSpot`

Spot strategy for instance billed in pay\-as\-you\-go mode. Value:


* NoSpot (default): Creates a regular Pay\-as\-you\-go instance.

* SpotAsPriceGo:The system automatically bids based on the current market price for the spot instance.

* SpotWithPriceLimit: spot instance with a price limit.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When InstanceChargeType is set to PostPaid, this parameter takes effect.</div>


* <div data-tips="true" data-tips-type="tip">For details on bidding patterns of spot instances, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance">Purchasing spot instances</a>.</div>




**Tags.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

Tag key of the instance.


* Parameter \- N: Indicates the serial number of the tag key. Value range: 1–20.

* Separate multiple tag keys with ampersands ( & ).


Naming rules:


* Cannot start with volc: in any case form.

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the instance.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).


Naming rules:


* Only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It can be empty. Length limit: 0–256 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you want to pass in this parameter, pass in the Tags.N.Key parameter first.</div>




**VersionDescription ** <span data-label="purple">string </span>`Optional` `Sample value: template version description`

The description of the instance launch template version.

Length: 1 to 256 English or Chinese characters. Cannot start with http:// or https://.



**Volumes.N.VolumeType ** <span data-label="purple">string[] </span>`Optional` `Sample value: Volumes.1.VolumeType=ESSD_PL0&Volumes.2.VolumeType=ESSD_FlexPL`

The volume type.


* Argument \- N: indicates the serial number of the volume. Valid range: 1–15. N = 1 indicates the system volume, and N ≥ 2 indicates the data volume.

* Parameter \- VolumeType: indicates the volume type. Valid values:

   * ESSD_PL0: ESSD PL0

   * PTSSD: PTSSD

* Separate multiple volumes with ampersands (&).



**VpcId ** <span data-label="purple">string </span>`Optional` `Sample value: vpc-3thbinq64t4bwbha****`

The VPC ID. You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) operation to query VPCs that meet the condition.



**ZoneId**<span data-label="purple"> string </span>`Optional Sample value: cn-beijing-a`

The available zone ID of the instance. You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



**LaunchTemplateName ** <span data-label="purple">string </span>`Optional` `Sample value: template-test`

The launch template name.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to confirm the template.</div>


<div data-tips="true" data-tips-type="tip">If both the values of LaunchTemplateId and LaunchTemplateName are valid, the value of LaunchTemplateId takes precedence.</div>




**ImageName ** <span data-label="purple">string </span>`Optional` `Sample value: NameDemo`

The name of the image.



**UserData**<span data-label="purple"> string</span>` Optional Sample value: ZWNobyBoZWxsbyBlY3Mh`

Instance custom data. The custom data for an instance must be encoded in Base64 format, and the data cannot exceed 16 KB before Base64 encoding.

If left blank, the parameter defaults to an empty value.



**HpcClusterId**<span data-label="purple"> string </span>`Optional Sample value: hpcCluster-l8u24ovdmoab6opf****`

ID of the HPC cluster to which the instance belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect and is required only for the creation of HPC\-optimized instances.</div>




**Volumes.N.Size ** <span data-label="purple">integer[] </span>`Optional` `Sample value: Volumes.1.Size=100&Volumes.2.Size=100`

The volume capacity.


* Argument \- N: indicates the serial number of the volume. Valid range: 1–15. N = 1 indicates a system volume, and N ≥ 2 indicates a data volume.

* Value \- Size: indicates the volume capacity. Unit: GiB. Value:

* System volume:

   * ESSD_PL0: 20~2048

   * PTSSD：10~500

* Data volume:

   * ESSD_PL0: 10~32768

   * PTSSD：20~8192

* Separate multiple volumes with ampersands (&).



**Volumes.N.DeleteWithInstance**<span data-label="purple"> boolean[] </span>`Optional Sample value: Volumes.1. DeleteWithInstance=true&Volumes.2. DeleteWithInstance=false`

Indicates whether to release the volume with the instance.


* Argument \- N: indicates the serial number of the volume. Valid range: 1–15. N = 1 indicates the system volume. By default, the system volume is released with the instance and cannot be retained. N ≥ 2 indicates the data volume.

* Value \- DeleteWithInstance: Whether to release the volume with the instance.

   * true (default): The volume is released with the instance. When "false" is passed in, this configuration is invalid on the system volume. By default, the system volume is released with the instance and cannot be retained.

   * false: The volume is not released with the instance.

* Separate multiple volumes with ampersands (&).



**Eip.Bandwidth ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The maximum bandwidth for the EIP. Unit: Mbps.


* Value range: 1 to 500.

* Default value: 1


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you configure Eip.Bandwidth or Eip.ISP, an EIP is assigned when the scaling group creates an instance, with the default billing mode of pay\-as\-you\-go (pay\-by\-bandwidth).</div>




**Eip.ISP**<span data-label="purple"> string</span>` Optional Sample value: BGP`

The EIP ISP type. Valid values:


* BGP: BGP (Multi\-ISP).

* If your account has applied for and enabled permission for the static single\-ISP, you can pass in the following values:

   * ChinaMobile: China Mobile static single\-ISP.

   * ChinaTelecom: China Telecom static single\-ISP.

   * ChinaUnicom: China Unicom static single\-ISP.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you configure Eip.Bandwidth or Eip.ISP, an EIP is assigned when the scaling group creates an instance, with the default billing mode of pay\-as\-you\-go (pay\-by\-bandwidth).</div>




**Eip.BandwidthPackageId**<span data-label="purple"> string</span>` Optional Sample value: bwp-2zeo05qre24nhrqpy****`

ID of the shared bandwidth package. This indicates adding the EIP to the specified shared bandwidth package. You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) operation to query IDs of shared bandwidth packages. To associate an EIP with a shared bandwidth package, the following conditions are required:


* The EIP and bandwidth package must be of the same security mode.

* The EIP and shared bandwidth package must be of the same ISP type.

* Shared bandwidth package is of the IPv4 type.



**Eip.SecurityProtectionTypes.N ** <span data-label="purple">string[] </span>`Optional Sample value: AntiDDoS_Enhanced`

The security protection type of EIP.


* N specifies the serial number of the protection type. Currently, only 1 is supported.

* Valid values:

   * AntiDDoS_Enhanced: Apply for an EIP with enhanced protection, which can be added to a Anti\-DDoS Origin (Enterprise Edition) instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If AntiDDoS_Enhanced is set, EipAddress.ChargeType cannot be set to PrePaid and EipAddress.ISP must be set to BGP.</div>


* <div data-tips="true" data-tips-type="tip">EIPs with enhanced protection are in Beta. If you need a trial, please <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> or contact your account manager to apply.</div>


* If no argument is passed in, this indicates applying for an EIP of the basic protection type.



**Eip.SecurityProtectionInstanceId ** <span data-label="purple">integer </span>`Optional` `Sample value: 151`

ID of the Anti\-DDoS Origin (Enterprise Edition).


* You can call the DescInstanceList operation to query the ID of DDoS Native Protection (Enterprise Edition).

* When SecurityProtectionTypes.N is set to AntiDDoS_Enhanced, this parameter is required to be passed in.



**SpotPriceLimit ** <span data-label="purple">float </span>`Optional` `Sample value: 0.78`

The maximum hourly price for spot instances. A maximum of three decimal places for the price is supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only when SpotStrategy=SpotWithPriceLimit.</div>


When you create an instance launch template, the spot instance price is not restricted or validated. However, you may fail to create an instance using the template due to an inappropriate bid price for the spot instance in the template.



**ScheduledInstance.ScheduledInstanceName ** <span data-label="purple">string </span>`Optional` `Sample value: ESI-Name`

Name of the ESI order. Value:


* Cannot start with a number, a hyphen (\-), or an underscore (_)

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The length limit is 1 to 128 characters.

* Special characters are currently not supported.



**ScheduledInstance.ScheduledInstanceDescription ** <span data-label="purple">string </span>`Optional` `Sample value: this is a test order`

The description of the ESI order.


* Start with a letter or Chinese character only.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.

* If left blank, the parameter defaults to an empty string.



**Eip.BillingType ** <span data-label="purple">integer </span>`Optional` `Sample value: 2`

The metering method of Elastic IP address (EIP). Valid values:


* 2: Pay\-as\-you\-go (pay\-by\-bandwidth).

* 3: Pay\-as\-you\-go (pay\-by\-data\-transfer).



**SuffixIndex ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The starting number of sequential suffixes.


* Value range: 1 ~ 999.

* Default value: 1



**UniqueSuffix ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Indicates whether to add sequential suffixes to the hostnames and instance names when you create multiple instances. Value:


* true: Enables the sequential suffix feature.

* false (default): Disables the sequential suffix feature.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you enable the sequential suffix feature and Hostname is left empty, the system automatically generates hostnames without a sequential suffix.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**LaunchTemplateVersionNumber ** <span data-label="purple">integer </span>`Sample value: 2`

The version number of the instance launch template.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateLaunchTemplateVersion&Version=2020-04-01&LaunchTemplateId=lt-ysxc16auaugh9zfy**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220419160338010225133143077B****",
        "Action": "CreateLaunchTemplateVersion",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "LaunchTemplateVersionNumber": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
