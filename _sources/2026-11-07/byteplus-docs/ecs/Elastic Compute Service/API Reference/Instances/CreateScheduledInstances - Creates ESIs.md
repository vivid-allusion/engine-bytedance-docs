---
title: "CreateScheduledInstances - Creates ESIs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateScheduledInstances"
---

Call the CreateScheduledInstances operation to create an Elastic Scheduled Instance (ESI).

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

For information on the operation process, applicable scenarios, and limits for ESI, refer to [Elastic Scheduled Instances (ESI) overview](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateScheduledInstances&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|YBeURX">必选</span> `Sample value: CreateScheduledInstances`

The action that you want to perform. Value: CreateScheduledInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|N0MtXP">必选</span> `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**AutoReleaseAt ** <span data-label="purple">string </span>`Optional` `Sample value: 2023-03-29T18:50:00+08:00`

The automatic release time for the instance, which must fall on a full 10\-minute mark.

When `ElasticScheduledInstanceType` is set to Segmented, this parameter must be passed in. Valid range:


* When `DeliveryType` is set to Reserve, the earliest release time for the instance is 1 hour after the reserved delivery time period.

* When `DeliveryType` is set to Immediate, the earliest auto release time is the next full ten\-minute mark from the current time. For example, if the current time is 5:02, the earliest auto release time would be 5:20.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. The client automatically generates a token to ensure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Count ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The number of instances to create. Valid range:


* If `ElasticScheduledInstanceType` is set to `Esi`, the valid range is 1 \- 500.

* If `ElasticScheduledInstanceType` is set to `Segmented`, and:

   * `DeliveryType` is `Reserve`, with a valid range of 1–500.

   * `DeliveryType` is `Immediate`, with a valid range of 1–100.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The value defaults to 1 if you enter a value of 0.</div>




**CpuMaxFrequency ** <span data-label="purple">float </span>`Optional` `Sample value: 2.8`

Specify the maximum CPU frequency in GHz. The valid range is between the processor base frequency and turbo frequency.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only g3al (4xlarge, 8xlarge, 16xlarge, 32xlarge), c3al (4xlarge, 8xlarge, 16xlarge, 32xlarge), r3al (4xlarge, 8xlarge, 16xlarge), g4i, c4i, r4i, g4ie, c4ie, and r4ie instances support this parameter. For more information on processor base frequency or turbo frequency, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types</a>.</div>


* <div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, please contact your account manager to apply.</div>




**DeletionProtection ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

The attribute of instance deletion protection. Specify whether to delete the instance through the console or API. Value:


* true: Enable instance deletion protection.

* false (default): Disable instance deletion protection.



**DeliveryType ** <span data-label="purple">string </span>`Optional` `Sample value: Reserve`

Delivery type of Elastic Scheduled Instances\-Segmented. Value:


* Reserve (default): Scheduled delivery

* Immediate: Immediate delivery


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You need to pass in this parameter only when <code>ElasticScheduledInstanceType</code> is set to <code>Segmented</code>.</div>


* <div data-tips="true" data-tips-type="tip">The Elastic Scheduled Instances\-Segmented type is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**Description ** <span data-label="purple">string </span>`Optional` `Sample value: ECS instance for testing.`

Description of the instance. Default value: empty string.


* It must start with a letter or a Chinese character.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.



**DryRun ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to only precheck this request. Value:


* true: sends a check request without instance creation. Check items include: whether required parameters are filled, request format, business restrictions, and ECS inventory. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the value of DryRun is <code>true</code> and a value is set for the <code>Count</code> or <code>Mincount</code> parameter, the value must be 1.   </div>
   

* false (default): Send a normal request and directly create an instance after the check passes.



**EipAddress.BandwidthMbps ** <span data-label="purple">integer </span>`Optional` `Sample value: 5`

The maximum bandwidth for the EIP, in Mbps. Default value is 1.


* When `ChargeType` is set to `PayByBandwidth`: 1–500.

* When `ChargeType` is set to` PayByTraffic`: 1–200.



**EipAddress.BandwidthPackageId ** <span data-label="purple">string </span>`Optional` `Sample value: bwp-2zeo05qre24nhrqpy****`

ID of the shared bandwidth package. This indicates adding the EIP to the specified shared bandwidth package.


* You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) operation to query the ID of shared bandwidth package.

* To associate an EIP with a shared bandwidth package, the following conditions must be met:

   * The EIP and bandwidth package must be of the same security mode.

   * The EIP and bandwidth package belong to the same region.

   * The billing method of the EIP must be "Pay\-as\-you\-go".

   * Shared bandwidth package is of the IPv4 type.



**EipAddress.ChargeType ** <span data-label="purple">string </span>`Optional` `Sample value: PayByBandwidth`

The metering method of Elastic IP address (EIP). Valid values:


* PayByBandwidth (default): Pay\-by\-bandwidth

* PayByTraffic: Pay\-by\-data\-transfer

* PrePaid: Subscription.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the billing method <code>InstanceChargeType</code> of the instance is <code>PostPaid</code>, this parameter cannot be set to <code>PrePaid</code>.</div>




**EipAddress.ISP ** <span data-label="purple">string </span>`Optional` `Sample value: BGP`

The ISP for EIP, which by default is BGP. Value:


* BGP: BGP (Multi\-ISP).

* If your account has applied for and enabled permission for the static single\-ISP, you can pass in the following values:

* ChinaMobile: China Mobile static single\-ISP.

* ChinaTelecom: China Telecom static single\-ISP.

* ChinaUnicom: China Unicom static single\-ISP.

* If your account has applied for and enabled permission for the BGP single\-ISP, you can pass in SingleLine_BGP.

* If your account has applied for and enabled static BGP permission, you can pass in Static_BGP.



**EipAddress.ReleaseWithInstance ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether the EIP is deleted along with the instance. Value:


* true: The EIP is deleted along with the instance.

* false (default): The EIP is not deleted when the instance is deleted.



**EipAddress.SecurityProtectionInstanceId ** <span data-label="purple">integer </span>`Optional` `Sample value: 20`

ID of the Anti\-DDoS Origin (Enterprise Edition).


* You can call the DescInstanceList operation to query the ID of DDoS Native Protection (Enterprise Edition).

* When `SecurityProtectionTypes` is set to `AntiDDoS_Enhanced`, this parameter is required.



**EipAddress.SecurityProtectionTypes.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: SecurityProtectionTypes.1 =AntiDDoS_Enhanced`

The security protection type of EIP.


* N specifies the serial number of the protection type. Currently, only 1 is supported.

* Valid values:

   * AntiDDoS_Enhanced: Apply for EIP with enhanced protection type. Then the instance can be secured with Anti\-DDoS Origin (Enterprise Edition).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If <code>EipAddress.SecurityProtectionTypes.N</code> is passed in <code>AntiDDoS_Enhanced</code>, then <code>EipAddress.ChargeType</code> must not be <code>PrePaid</code>, and <code>EipAddress.ISP</code> must pass in <code>BGP</code>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">EIPs with enhanced protection are currently in Beta. If you need a trial, please contact your account manager.      </div>
      

   * If this parameter is not passed in, the system applies for an EIP of the default protection type.



**ElasticScheduledInstanceType ** <span data-label="purple">string </span>`Optional` `Sample value: Esi`

The ESI type. Valid values:


* Esi (default): Elastic Scheduled Instances (ESI)

* Segmented: Elastic Scheduled Instances\-Segmented


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Elastic Scheduled Instances\-Segmented type is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**EndDeliveryAt ** <span data-label="purple">string </span>`Optional` `Sample value: 2023-03-29T18:10:00+08:00`

The end delivery time of instances must fall on a full 10\-minute mark, and the interval between it and `StartDeliveryAt` must be 10 minutes.


* When `ElasticScheduledInstanceType` is set to `Esi`, the end delivery time of instances is within the range of 4 to 8 hours after the reservation.

* When `ElasticScheduledInstanceType` is set to `Segmented`:

   * If `DeliveryType` is `Reserve`, the end delivery time of instances is within 24 hours after the reservation.

   * If `DeliveryType` is `Immediate`, you do not need to pass in this parameter.



**Hostname ** <span data-label="purple">string </span>`Optional` `Sample value: instance-host-name`

The hostname is the internal computer name within the operating system of an instance.


* Linux instances:

   * Letters, numbers, periods ".", and hyphens "\-" are allowed.

   * Cannot start or end with a hyphen or period. Hyphens and periods cannot be used consecutively.

   * The length limit is 2 to 63 characters.

* Windows instances:

   * Letters, numbers, or hyphens "\-" are allowed. But the name cannot be comprised of numbers only.

   * Cannot start or end with a hyphen. Hyphens cannot be used consecutively.

   * The length limit is 2 to 15 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If no argument is filled in, the hostname is automatically generated based on the rule of "iv\- + initial hostname". For example,</div>


   <div data-tips="true" data-tips-type="tip">iv\-3tigy72q3u3vj0\*\*\*\*\*\*.   </div>
   

* <div data-tips="true" data-tips-type="tip">Generation logic of the initial hostname:</div>


   * <div data-tips="true" data-tips-type="tip">Linux instances: Extract all characters after instance ID i\-.</div>


   * <div data-tips="true" data-tips-type="tip">Windows instances: Extract the last 12 characters after instance ID i\-.</div>


* <div data-tips="true" data-tips-type="tip">When creating instances in a batch, you can set sequential hostnames in the <code>name_prefix[begin_number,bits]name_suffix</code> format. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames">Configuring sequential instance names or hostnames in a batch</a>.</div>




**HpcClusterId ** <span data-label="purple">string </span>`Optional Sample value: hpcCluster-l8u24ovdmoab6opf****`

When you create an HPC\-optimized instance, specify the HPC Cluster ID.



**HttpTokens ** string `Optional` `Sample value: optional`

The access mode of instance metadata. You can set whether to enable the security hardening mode. Value:


* optional (default): Not mandatory (Normal Mode and Security Hardening Mode). This allows instance metadata access either directly through the standard method or via the token\-based authentication method.

* required: Mandatory (Security Hardening Mode). This only allows instance metadata access through a token\-based authentication method.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For information on how to view metadata and the available metadata items, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata">Viewing instance metadata</a>.</div>


* <div data-tips="true" data-tips-type="tip">Security Hardening Mode is currently in Beta. If you need a trial, please contact your account manager to apply.</div>




**ImageId ** <span data-label="purple">string </span><span data-api-tag="require|BMIqMs">必选</span> `Sample value: image-3tefr6wgx63vj0x1****`

The image ID used during the instance startup.

You can query available image resources through [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages).



**InstallRunCommandAgent ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to install cloud assistant Agent on startup during instance creation. Value:


* true: Install during creation.

* false (default): Do not install during creation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about Cloud assistant, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant">Cloud assistant overview</a>.</div>




**InstanceName ** <span data-label="purple">string </span><span data-api-tag="require|RV7RF0">必选</span> `Sample value: instance-test`

The instance name.


* Start with a letter or Chinese.

* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If <code>SuffixIndex</code> is set for the instance, the instance name length includes the suffix.</div>


* <div data-tips="true" data-tips-type="tip">When creating instances in a batch, you can set sequential instance names in the <code>name_prefix[begin_number,bits]name_suffix</code> format. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames">Configuring sequential instance names or hostnames in a batch</a>.</div>




**InstanceTypeId ** <span data-label="purple">string </span><span data-api-tag="require|PXnRwJ">必选</span> `Sample value: ecs.g1ie.xlarge`

Instance type:


* For instance types available for reservation, refer to [Elastic Scheduled Instances (ESI) overview](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview).

* You can call the [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) operation to query the inventory information of instances in the availability zone.



**KeepImageCredential ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to keep image settings. Value:


* true: Keeps image settings. This allows you to use the password or key pair specified for the image to log in to the ECS instance.

* false (default): Does not keep image settings.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only custom images and shared images support this feature.</div>


* <div data-tips="true" data-tips-type="tip">When the value of this parameter is <code>true</code>, do not pass in <code>Password</code> and <code>KeyPairName</code>.</div>




**KeyPairName ** <span data-label="purple">string </span>`Optional` `Sample value: kp-test-123`

If you need to use the "SSH Key" to log in to the instance, specify the name of an already created key pair.

You can call the [DescribeKeyPairs](https://docs.byteplus.com/en/docs/ecs/DescribeKeyPairs) operation to view existing key pairs. If no key pair is available, call the [CreateKeyPair](https://docs.byteplus.com/en/docs/ecs/CreateKeyPair) operation to create a new one.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Windows instances do not support the SSH Key method. Even if this parameter is passed in, only the parameter <code>Password</code> takes effect.</div>


* <div data-tips="true" data-tips-type="tip">Linux instances support login with both password and key pair. If both <code>KeyPairName</code> and <code>Password</code> are set, only the key pair <code>KeyPairName</code> takes effect when you call this operation.</div>




**MinCount ** <span data-label="purple">integer</span>` Optional Sample value: 2`

Specify the minimum number of ESIs that can be created. Valid range:


* General\-purpose ESI, Segmented\-ESI (Scheduled delivery): 1–500

* Segmented\-ESI (Immediate delivery): 1–100


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><code>MinCount</code> (the minimum number of ECS instances that can be created) is less than or equal to <code>Count</code> (the number of instances to be created).</div>


* <div data-tips="true" data-tips-type="tip">When available inventory exceeds <code>Count</code> (the number of instances to be created), instances are created based on <code>Count</code>.</div>


* <div data-tips="true" data-tips-type="tip">When available resources are between <code>MinCount</code> (the minimum number of ECS instances that can be created) and <code>Count</code> (the number of instances to be created), instances are created based on available inventory resources.</div>


* <div data-tips="true" data-tips-type="tip">When available resources are less than <code>MinCount</code> (the minimum number of ECS instances that can be created), a creation failure occurs due to insufficient inventory.</div>




**NetworkInterfaces.N.SecurityGroupIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|c5QDY0">必选</span> `Sample value: NetworkInterfaces.1.SecurityGroupIds.1=sg-3ti78x9h8t4bw*****& NetworkInterfaces.2.SecurityGroupIds.1=sg-3cj59ih2v9hj46c6rr******`

ID of the security group associated with the network interface.


* The first N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* The second N: indicates the serial number of the security group associated with the network interface. Value: 1–5.

* Separate multiple security group IDs with ampersands (&).



**NetworkInterfaces.N.SubnetId ** <span data-label="purple">string[] </span><span data-api-tag="require|k6DOuu">必选</span> `Sample value: NetworkInterfaces.1.SubnetId=subnet-3tispp1nai4e8i******& NetworkInterfaces.2.SubnetId=subnet-2ff1nczrx2lts5oxru******`

The ID of the subnet of the instance VPC. When creating an instance, you can associate secondary network interfaces with it.


* Argument \- N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* Separate multiple VPC subnet IDs with ampersands (&).



**NetworkInterfaces.N.PrimaryIpAddress ** <span data-label="purple">string[] </span>`Optional` `Sample value: NetworkInterfaces.1.PrimaryIpAddress=192.168.XX.XX`

The specified primary IP address of the network interface. Currently, primary IP addresses can only be assigned for primary network interfaces or secondary network interfaces.


* Argument \- N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* Separate multiple network interfaces with ampersands (&).



**NetworkInterfaces.N.PrivateIpAddresses.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: NetworkInterfaces.1.PrivateIpAddresses.1=172.16.XX.XX&NetworkInterfaces.1.PrivateIpAddresses.2=172.16.XX.XX`

The specified secondary IP address of the primary network interface. Currently, only secondary IPs for the primary network interface are supported.


* The first N: indicates the serial number of the primary network interface. Currently, one ECS instance can only be associated with one primary network interface.

* The second N: indicates the serial number of the secondary IP address for the primary network interface. The maximum number of secondary IP addresses that can be assigned is equal to the number of private IP addresses supported by a network interface for this [instance type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types), minus one (for the primary private IP address).

* Separate multiple secondary IP addresses with ampersands (&).



**Password ** <span data-label="purple">string </span>`Optional` `Sample value: password@123`

If you need to log in to an instance with "Password", specify the initial login password of the administrator account through this parameter. The Linux administrator account is root, and the Windows administrator account is Administrator.

Password complexity requirements are as follows:


* The length limit is 8 to 30 characters.

* Passwords can only consist of uppercase letters, lowercase letters, numbers, and special characters, and must include at least three of these elements.

* Valid special characters: `~!@#$%^&\*()_\-+=|{}[]:;'<\>,.?/

* The password cannot start with "/" or "$6$".


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For login credentials, "Password", "Key Pair", and "Keep image settings" are available. If you choose to use a password, specify a complex password to improve security.</div>




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: project_a`

The project to which the resource belongs. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**ScheduledInstanceDescription ** <span data-label="purple">string </span>`Optional` `Sample value: ScheduledInstance for testing.`

The description of the ESI order. Default value is an empty string.


* Start with a letter or Chinese character only.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.



**ScheduledInstanceName ** <span data-label="purple">string </span><span data-api-tag="require|Va9LDN">必选</span> `Sample value: ESI-Name`

ESI order name. Value:


* Cannot start with a number, a hyphen (\-), or an underscore (_).

* Only Chinese, letters, numbers, underscores and hyphens are allowed.

* The length limit is 1 to 128 characters.

* Special characters are currently not supported.



**SecurityEnhancementStrategy ** <span data-label="purple">string </span>`Optional` `Sample value: Active`

Whether to enable security enhancement. Value:


* Active: Enables security enhancement. This feature is effective for public images only.

* InActive: Disables security enhancement. This feature is effective for all image types.



**StartDeliveryAt ** <span data-label="purple">string </span>`Optional` `Sample value: 2023-03-29T17:50:00+08:00`

The instance delivery start time must be at 10\-minute intervals on the hour.


* When `ElasticScheduledInstanceType` is set to `Esi`, the instance delivery time is within the range of 4 to 8 hours after the reservation.

* When `ElasticScheduledInstanceType` is set to `Segmented`:

   * When `Delivery Type` is `Reserve`, the instance delivery time is within 24 hours after reservation.

   * When `Delivery Type` is `Immediate`, you do not need to pass in this parameter.



**SuffixIndex ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The starting number of the sequential suffix, with a valid range of 1–999. Default value: 1



**Tags.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The key of the tag.


* Argument \- N: Specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple keys with ampersands (&).

   Naming rules:

* It cannot start with `volc:` or `sys:` in any case form.

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The user tag value.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple key values with ampersands (&).

   Naming rules:

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It can be empty. Length limit: 0–256 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




**UniqueSuffix ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Specify whether to add sequential suffixes to `Hostname` and `InstanceName` when you create multiple instances.


* true: Enable sequential suffix.

* false (default): Disables the sequential suffix feature.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you enable the sequential suffix and <code>Hostname</code> is empty, the system automatically generates hostnames without a sequential suffix.</div>


* <div data-tips="true" data-tips-type="tip">If you enable the sequential suffix and specify the naming format <code>[begin_number,bits]</code> for <code>Hostname</code> and <code>InstanceName</code>, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames">Setting sequential instance or host names in a batch</a> for the final naming effect.</div>




**UserData ** <span data-label="purple">string </span>`Optional` `Sample value: ZWNobyBoZWxsbyBlY3Mh`

Instance custom data. The custom data for an instance must be encoded in Base64 format, and the data cannot exceed 16KB before Base64 encoding.

If left blank, the parameter defaults to an empty value.



**Volumes.N.Size ** <span data-label="purple">integer[] </span><span data-api-tag="require|3Vahse">必选</span> `Sample value: Volumes.1.Size=100&Volumes.2.Size=100`

The volume capacity. Unit: GiB. The valid range of N is 1–16. N = 1 indicates the system volume, and N ≥ 2 indicates the data volume. Separate multiple volumes with ampersands (&).

Valid range of volume capacity.


* System volume:

   * ESSD_PL0: 20～2048

   * ESSD_FlexPL: 20～2048

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Default value: max{40, the capacity of the image corresponding to ImageId}.   </div>
   

* Data volume:

   * ESSD_PL0: 10～32768

   * ESSD_FlexPL: 10～32768

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If this parameter is not passed in, the data volume capacity is based on the snapshot size corresponding to <code>Volumes.N.SnapshotId</code>. If <code>Volumes.N.SnapshotId</code> is not passed in, the system returns the error LimitExceeded.DataVolumeSize.   </div>
   



**Volumes.N.DeleteWithInstance ** <span data-label="purple">boolean[] </span>`Optional` `Sample value: Volumes.1.DeleteWithInstance=true&Volumes.2.DeleteWithInstance=false`

Whether to release the volume with the instance. Value:


* true (default): The volume is released with the instance.

* false: The volume is not released with the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume that is released with the instance and cannot be retained by default. N ≥ 2 indicates the data volume, so you can choose whether to release it with the instance.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Volumes.N.ExtraPerformanceIOPS ** <span data-label="purple">integer[] </span>`Optional Sample value: Volumes.2.ExtraPerformanceIOPS=100`

The size of additional IOPS of the volume. This feature is only supported by ESSD FlexPL data volumes, with the unit being operations per second (ops/sec).

When `ExtraPerformanceTypeId` is set to `Balance` or `IOPS`, configure this parameter. The value ranges for each type of extra performance are as follows:


* IOPS: 1–50000

* Balance: 1–50000


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Volumes.N.ExtraPerformanceThroughputMB ** <span data-label="purple">integer[] </span>`Optional` `Sample value: Volumes.2.ExtraPerformanceThroughputMB=100`

The capacity of additional throughput performance (unit: MB/s) for the volume. Only ESSD FlexPL data volumes support additional throughput performance.

When `ExtraPerformanceTypeId` is set to `Throughput`, configure this parameter.

Valid range: 1–650.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Volumes.N.ExtraPerformanceTypeId ** <span data-label="purple">string[] </span>`Optional` `Sample value: Volumes.2.ExtraPerformanceTypeId=IOPS`

The type of additional performance for the volume. This feature is only supported by ESSD FlexPL data volumes. Valid range:


* Balance: Balanced additional performance.

* IOPS: IOPS additional performance.

* Throughput: Additional performance related to throughput.

   For more information about additional performance, please refer to [Volume additional performance](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Volumes.N.SnapshotId ** <span data-label="purple">string[] </span>`Optional` `Sample value: Volumes.1.SnapshotId=snap-31akybwsxi8rudc6****&Volumes.2.SnapshotId=snap-31ak39j5bh8rubsn****`

Only data volumes can be created with a snapshot. You can call the [DescribeSnapshots](https://docs.byteplus.com/en/docs/ecs/Describesnapshots) operation to query the snapshot ID.


* Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume. Therefore, you can pass in the snapshot ID for the target data volume.

* Multiple volumes are separated with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only ESSD supports volume creation using snapshots. PTSSD does not support snapshot\-related features.</div>


* <div data-tips="true" data-tips-type="tip">Only snapshots in "Available" status support new volume creation. Snapshots in statuses "Creating", "Rolling Back", "Deleting", and "Error" do not.</div>




**Volumes.N.VolumeType ** <span data-label="purple">string[] </span>`Optional` `Sample value: Volumes.1.VolumeType=ESSD_PL0&Volumes.2.VolumeType=ESSD_PL0`

The volume type. Value:


* ESSD_PL0: ESSD PL0

* ESSD_FlexPL: ESSD FlexPL


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume, and N ≥ 2 indicates the data volume.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**ZoneId ** <span data-label="purple">string </span><span data-api-tag="require|g91rUt">必选</span> `Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScheduledInstanceId ** <span data-label="purple">string </span>`Sample value: esi-ycvw0gtwjql8j1c3****`

ESI order ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateScheduledInstances&Version=2020-04-01&ZoneId=cn-beijing-a&ScheduledInstanceName=ESI-Name&StartDeliveryAt=2023-03-29T17:50:00+08:00&EndDeliveryAt=2023-03-29T18:10:00+08:00&ImageId=image-3tgt71djf14bwbh7****&InstanceTypeId=ecs.g1ie.xlarge&InstanceName=test-***&Count=1&Password=test@123&NetworkInterfaces.1.SubnetId=subnet-3thbjdy3rh4bwbh8****&NetworkInterfaces.1.SecurityGroupIds.1=sg-3thbinrkp94bwbha****&Volumes.1.VolumeType=ESSD_PL0&Volumes.1.Size=40 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024010316352515498DC927A20055****",
        "Action": "CreateScheduledInstances",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "ScheduledInstanceId": "esi-ycvw0gtwjql8j1c3****"
    }
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
|400 |InvalidAutoReleaseAt.Malformed |The specified AutoReleaseAt is malformed. |The specified auto release time is invalid. |
|400 |InvalidBandwidthPackageStatus |The status of the specified bandwidth package does not support this request. |The status of the specified bandwidth package does not support this request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidCount.Malformed |The specified count is malformed. |The specified Count is invalid. |
|400 |InvalidDeliveryTimeIntervalForCreateScheduledInstance.Unsupported |The specified delivery time interval does not support creation of scheduled instances. |The specified delivery time period is unavailable for ESI creation. |
|400 |InvalidDeliveryType.Malformed |The specified DeliveryType is malformed. |The specified delivery type is invalid. |
|400 |InvalidDeliveryTypeForCreateScheduledInstanceNow.Unsupported |The specified delivery type does not support creation of scheduled instances at the current time. |The specified delivery method is unavailable for ESI creation. |
|400 |InvalidEipAddressChargeType.Malformed |The specified ChargeType of elastic ip is malformed. |The specified billing method of EIP is invalid. |
|400 |InvalidElasticScheduledInstanceType.Malformed |The specified ElasticScheduledInstanceType is malformed. |The specified ESI type is invalid. |
|400 |InvalidEndDeliveryAt.Malformed |The specified EndDeliveryAt is malformed. |The specified delivery end time is invalid. |
|400 |InvalidExtraPerformanceTypeId.Malformed |The specified ExtraPerformanceTypeId is malformed. |The specified type of additional performance package is invalid. |
|400 |InvalidHostname.Malformed |The specified Hostname is malformed. |The specified hostname is invalid. |
|400 |InvalidImageForCreateScheduledInstance.UnSupported |The specified image does not support create scheduled instance. |The specified image does not support ESI creation. |
|400 |InvalidImageSize.Malformed |The specified ImageSize is malformed. |The specified image size is invalid. |
|400 |InvalidInstanceChargeType |The specified InstanceChargeType is invalid. |The specified instance billing method is invalid. |
|400 |InvalidInstanceDescription.Malformed |The specified InstanceDescription is malformed. |The specified instance description is not valid. |
|400 |InvalidInstanceName.Malformed |The specified InstanceName is malformed. |The specified instance name is invalid. |
|400 |InvalidInstanceTypeForCreateScheduledInstance.Unsupported |The specified InstanceType does not support creation of scheduled instances. |The specified instance type does not support ESI creation. |
|400 |InvalidKeyPairForWindows.Unsupported |The OSType of this specified instance is Windows, which does not support key pairs. |The specified instance is based on the Windows operating system and does not support key pairs. |
|400 |InvalidMinCount.Malformed |The specified MinCount is malformed. |The specified minimum purchase quantity for the instance is invalid. |
|400 |InvalidParameterCombination |Indicates an incorrect combination of parameters. |The parameter combination is incorrect, or a parameter is missing. |
|400 |InvalidPassword.Malformed |The specified password is malformed. |The specified password format is invalid. |
|400 |InvalidProjectName |The specified ProjectName is invalid. |The specified project name is invalid. |
|400 |InvalidScheduledInstanceDescription.Malformed |The specified ScheduledInstanceDescription is malformed. |The specified ESI order description is invalid. |
|400 |InvalidScheduledInstanceName.Malformed |The specified ScheduledInstanceName is malformed. |The specified ESI order name is invalid. |
|400 |InvalidSecurityEnhancementStrategy.Malformed |The specified SecurityEnhancementStrategy is malformed. |The specified security enhancement policy is invalid. |
|400 |InvalidSecurityGroupStatus |The specified security group is not in the correct status for the request. |The specified security group is not in the correct status for the request. |
|400 |InvalidSecurityGroupType.Malformed |The specified SecurityGroupType is malformed. |The specified security group type is invalid. |
|400 |InvalidSecurityProtectionInstanceStatus |The specified security protection instance is not in the correct status for the request. |The specified security protection instance is not in the correct status for the request. |
|400 |InvalidSecurityProtectionTypes.Malformed |The specified security protection type is malformed. |The specified security protection level is not supported. |
|400 |InvalidSnapshotStatus |The status of the specified snapshot does not support this request. |The specified snapshot status does not support this operation. |
|400 |InvalidStartDeliveryAt.Malformed |The specified StartDeliveryAt is malformed. |The specified delivery start time is invalid. |
|400 |InvalidSuffixIndex.Malformed |The specified SuffixIndex is malformed. |The specified sequential suffix is invalid. |
|400 |InvalidSystemVolumeForExtraPerformance.Unsupported |The specified SystemVolume does not support extra performance. |The specified system volume does not support purchase of additional performance. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidUserData.Malformed |The specified UserData is malformed. |The specified UserData is invalid. |
|400 |InvalidVolumeReleaseType.Malformed |The specified VolumeReleaseType is malformed. |The specified type of volume release is invalid. |
|400 |InvalidVolumeSizeForExtraPerformance.Unsupported |The specified VolumeSize does not support extra performance. |The specified volume capacity does not support the purchase of additional performance. |
|400 |InvalidVolumeType.Malformed |The specified VolumeType is malformed. |The specified volume type is invalid. |
|400 |InvalidVolumeTypeForExtraPerformance.Unsupported |The specified VolumeType does not support extra performance. |The specified volume type does not support the purchase of additional performance. |
|400 |LimitExceeded.DataVolumeSize |The specified data volume size exceeds the limit. |The specified data volume size (GiB) exceeds the limit. |
|400 |LimitExceeded.ExtraPerformanceThroughput |You've reached the limit on the number of ExtraPerformanceThroughput that you can set. |The throughput has reached the maximum limit. No additional performance required. |
|400 |LimitExceeded.MaximumEipBandwidth |The specified elastic ip bandwidth value exceeds the maximum limit. |The specified EIP bandwidth value exceeds the maximum limit. |
|400 |LimitExceeded.MaximumExtraPerformanceIOPS |The number of specified ExtraPerformanceIOPS exceeds the maximum limit. |The specified additional performance IOPS exceeds the maximum limit. |
|400 |LimitExceeded.MaximumExtraPerformanceThroughputMB |The number of specified ExtraPerformanceThroughputMB exceeds the maximum limit. |The specified additional performance throughput exceeds the maximum limit. |
|400 |LimitExceeded.MaximumNetworkInterfaces |You've reached the limit on the number of NetworkInterfaces that can be attached to the instance. |The specified number of network interfaces associated with the instance exceeds the upper limit. |
|400 |LimitExceeded.MaximumSecurityProtectionTypes |You've reached the limit on the number of SecurityProtectionTypes that you can set. |The specified number of SecurityProtectionTypes exceeds the maximum limit. |
|400 |LimitExceeded.MaximumSubnetIps |The number of specified subnet IP addresses exceeds the maximum limit. |The specified number of subnet IP addresses reaches the maximum limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |LimitExceeded.MaximumVolumes |You've reached the limit on the number of volumes that can be attached to the instance. |The specified number of volumes mounted to the instance exceeds the upper limit. |
|400 |LimitExceeded.MinimumEipBandwidth |The specified elastic ip bandwidth value exceeds the minimum limit. |The bandwidth value of the specified EIP exceeds the minimum limit. |
|400 |LimitExceeded.MinimumExtraPerformanceIOPS |The number of specified ExtraPerformanceIOPS exceeds the minimum limit. |The specified additional performance IOPS exceeds the minimum limit. |
|400 |LimitExceeded.MinimumExtraPerformanceThroughputMB |The number of specified ExtraPerformanceThroughputMB exceeds the minimum limit. |The specified additional performance throughput exceeds the minimum limit. |
|400 |LimitExceeded.SystemVolumeSize |The specified system volume size exceeds the limit. |The specified system volume size (GiB) exceeds the limit. |
|400 |MissingParameter.AutoReleaseAt |The required parameter AutoReleaseAt is not supplied. |The auto release time for Segmented ESI order can not be empty. |
|400 |MissingParameter.EndDeliveryAt |The required parameter EndDeliveryAt is not supplied. |The delivery end time can not be empty. |
|400 |MissingParameter.HpcClusterId |The required parameter HpcClusterId is not supplied. |HPC Cluster ID cannot be empty. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|400 |MissingParameter.InstanceName |The required parameter InstanceName is not supplied. |The instance name cannot be empty. |
|400 |MissingParameter.InstanceTypeId |The required parameter InstanceTypeId is not supplied. |The ID of the instance type cannot be empty. |
|400 |MissingParameter.NetworkInterfaces |The required parameter NetworkInterfaces is not supplied. |Network interface information cannot be empty. |
|400 |MissingParameter.PasswordAndKeyPair |The required parameter PasswordAndKeyPair is not supplied. |The password and key pair cannot both be empty. |
|400 |MissingParameter.ScheduledInstanceName |The required parameter ScheduledInstanceName is not supplied. |The ESI order name can not be empty. |
|400 |MissingParameter.SecurityGroupIds |The required parameter SecurityGroupIds is not supplied. |The security group ID cannot be empty. |
|400 |MissingParameter.StartDeliveryAt |The required parameter StartDeliveryAt is not supplied. |The delivery start time can not be empty. |
|400 |MissingParameter.SubnetId |The required parameter SubnetId is not supplied. |The subnet ID cannot be left empty. |
|400 |MissingParameter.VolumeType |The required parameter VolumeType is not supplied. |The volume type cannot be empty. |
|400 |MissingParameter.Volumes |The required parameter Volumes is not supplied. |Volume information cannot be empty. |
|400 |MissingParameter.ZoneId |The required parameter ZoneId is not supplied. |Availability zone ID cannot be empty. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the number of instances that you can create, please submit ticket to request an increase in quota. |The number of bandwidth packages you can create reaches the limit. Please submit a ticket to increase the quota. |
|400 |QuotaExceeded.MaximumEips |You've reached the limit on the number of EIP that you can create, please submit ticket to request an increase in quota. |Insufficient EIP quota. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumGeneralCpus |You've reached the limit on the number of general instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu] quota. |The CPU quota of the General\-purpose instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic] quota. |The GPU card quota for GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance] quota. |The GPU card quota for HPC\-optimized instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumLocalVolumeCpus |You've reached the limit on the number of local volume instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu] quota. |The CPU quota of the Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumNetworkInterfaces |You've reached the limit on the number of elastic network interface that you can create, please submit ticket to request an increase in quota. |Network interface quota is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumScheduledInstanceCpus |You've reached the limit on the number of scheduled instance CPU that you can create, please submit ticket to request an increase in quota. |Insufficient ESI quota. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumSecurityGroupIps |You've reached the limit on the number of SecurityGroupIps that you can create, please submit ticket to request an increase in quota. |The IP addresses that can be associated with security groups are insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumSecurityGroupNetworkInterfaces |You've reached the limit on the number of SecurityGroupEnis that you can create, please submit ticket to request an increase in quota. |The quota for network interfaces that can be associated with the security group is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumSecurityGroups |You've reached the limit on the number of SecurityGroups that you can create, please submit ticket to request an increase in quota. |Security group quota is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumVolumes |You've reached the limit on the capacity of Volumes that you can create, please submit ticket to request an increase in quota. |The volume quota is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.SecurityProtectionInstance |You've reached the limit on the number of security protection instance that you can add. |The maximum limit on the number of instances that can enable security protection is reached. |
|403 |InvalidChargeTypeForDeletionProtection.Unsupported |Deletion protection is only valid for postPaid instance. |The deletion protection feature can only be used on general pay\-as\-you\-go resources. |
|403 |RequestForbidden |Request is forbidden by the server. |Your ECS services are suspended because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|404 |InvalidBandwidthPackage.NotFound |The specified BandwidthPackage does not exist. |The specified Shared Bandwidth Package does not exist. |
|404 |InvalidHpcCluster.NotFound |The specified HpcCluster does not exist. |The specified HPC cluster does not exist. |
|404 |InvalidISP.NotFound |The specified ISP does not exist. |The specified ISP does not exist. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|404 |InvalidKeyPair.NotFound |The specified KeyPair does not exist. |The specified key pair does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSecurityGroup.NotFound |The specified SecurityGroup does not exist. |The specified security group does not exist. |
|404 |InvalidSecurityProtectionInstance.NotFound |The specified security protection instance does not exist. |The specified instance that enables security protection does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|409 |InvalidNetworkInterfacesVpc.Conflict |Multiple vpcs are not supported for instances in the same HpcCluster. |RDMA instances in the same high\-performance cluster cannot be associated with multiple VPCs. |
|409 |InvalidPrimaryIpAddress.Conflict |The specified PrimaryIpAddress already exists. |The specified PrimaryIpAddress already exists. |
|409 |InvalidPrivateIpAddresses.Conflict |The specified PrivateIpAddresses already exists. |The specified PrivateIpAddresses already exists. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still being processed. Please try again later. |
|412 |Insufficient.AclCapacity |You've reached the limit number of ACLs on the switch. |The number of ACLs on the switch exceeds the limit. |
|412 |InvalidHpcCluster.VpcMismatch |The specified Vpc and the Vpc of HpcCluster do not match. |The VPC does not match. The specified VPC and the VPC of HPC cluster do not match. |
|412 |InvalidHpcCluster.ZoneMismatch |The specified HpcCluster and Instance's ZoneId do not match. |The HPC cluster is not within the scope of the instance availability zone. |
|412 |InvalidISP.BandwidthPackageMismatch |The specified ISP of EIP and bandwidth package do not match. |The specified ISPs for the EIP and bandwidth package do not match. |
|412 |InvalidImage.InstanceTypeMismatch |The specified image and instance type do not match. |The specified image does not support the specified instance type. |
|412 |InvalidImageArchitecture.InstanceTypeArchitectureMismatch |The specified image architecture and instance type architecture do not match. |The architecture type of the image is not supported by the instance type. |
|412 |InvalidImageId.KeepImageCredentialMismatch |The specified ImageId and KeepImageCredential do not match. |The specified ImageId and KeepImageCredential do not match. |
|412 |InvalidKeyPairName.KeepImageCredentialMismatch |The specified KeyPairName and KeepImageCredential do not match. |The specified KeyPairName and KeepImageCredential do not match. |
|412 |InvalidPassword.KeepImageCredentialMismatch |The specified Password and KeepImageCredential do not match. |The specified Password and KeepImageCredential do not match. |
|412 |InvalidReleaseWithInstance.ChargeTypeMismatch |The specified release with instance and charge type do not match. |The specified EIP deletion attribute (the EIP is deleted along with the instance) does not match the billing method. |
|412 |InvalidSecurityGroup.SubnetMismatch |The specified SecurityGroup and Subnet do not match. |The VPC of the security group does not match the VPC of the subnet. |
|412 |InvalidSecurityProtectionInstance.RegionMismatch |The specified security protection instance is not in the specified region. |The specified security protection instance is not in the specified region. |
|412 |InvalidSecurityProtectionInstance.SpecMismatch |The specified security protection instance and EIP are in different specifications. |The specified security protection instance and EIP specification do not match. |
|412 |InvalidSecurityProtectionTypes.BandwidthPackageIdMismatch |The specified security protection types and bandwidth package id do not match. |The specified EIP security protection level does not match the shared bandwidth level. |
|412 |InvalidStartDeliveryAtEndDeliveryAt.Mismatch |The specified StartDeliveryAt does not match EndDeliveryAt. |The specified delivery start time does not match the delivery end time. |
|412 |InvalidSubnet.ZoneMismatch |The specified subnet and instance are in different Availability Zones. |The availability zone associated with the subnet is different from the one where the instance resides. |
|412 |InvalidVolumeSize.ImageSizeMismatch |The specified system disk size is smaller than the image file size. |The specified system volume capacity is smaller than the image file size. |
|412 |InvalidVolumeType.ImageMismatch |The specified VolumeType and Image do not match. |The specified volume type and image do not match. |
|412 |InvalidVolumeType.InstanceTypeMismatch |The specified VolumeType and InstanceType do not match. |The specified volume type and instance type do not match. |
|412 |InvalidVolumeTypes.Mismatch |Mismatch between attached Volume types. |The types of mounted volumes do not match. |
|412 |OperationDenied.AccountCountryAreaInvalid |This product is temporarily not available for sale in the country or region where you registered your account. |This product is temporarily not available for sale in the country or region where you registered your account. |
|412 |OperationDenied.AccountDeleted |The specified action is denied because the account has been deleted. |The specified action is denied because the account has been deleted. |
|412 |OperationDenied.AccountTaxNoInvalid |To purchase BytePlus products, you need to provide a Goods and Services Tax (GST) number. |To purchase BytePlus products, you need to provide a Goods and Services Tax (GST) number. |
|412 |OperationDenied.AccountWeakVerified |The specified action is denied because the account failed to pass the weak real\-name authentication. |The specified action is denied because the account failed to pass the weak real\-name authentication. |
|412 |OperationDenied.ImageNotSnapshot |The specified image has not taken a snapshot and this operation is not supported. |The specified image has no corresponding snapshot. So this action is not supported. |
|412 |OperationDenied.NotOpeningQualified |The specified action is denied because the account has not completed account authentication. |The specified action is denied because the account has not completed account authentication. |
|412 |OperationDenied.RiskInterception |The specified action is denied. Due to risk interception, this feature is temporarily unavailable. |The specified action is denied. Due to risk interception, this feature is temporarily unavailable. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |Resource request rate exceeds the limit. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The resources are currently insufficient. Try again later or select other instance types. |
|500 |Insufficient.ScheduledInstanceCapacity |The specified delivery time interval is full, please select another delivery time interval. |The specified time period is fully booked. Please select another delivery time period. |
|500 |Insufficient.ScheduledInstanceDeliveryCapacity |The scheduled instance exceeds the delivery limit. |Reserved instances exceed the delivery limit. |
|500 |Insufficient.VolumePoolCapacity |There is not enough capacity to fulfill your request. |Insufficient capacity of the current storage pool. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
