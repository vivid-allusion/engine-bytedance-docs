---
title: "RunInstances - Creates instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/RunInstances"
---

1. Call the RunInstances operation to create one or more ECS instances.


<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* To associate an EIP with a created instance, call the [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress) operation.

* If you need to create an instance based on a whole image with this operation, pass in the ID of the target whole image through `ImageId`. For detailed steps, refer to [Purchasing ECS instances with whole images](https://docs.byteplus.com/en/docs/ecs/Using-whole-images-to-buy-ECS).

* When creating GPU instances by using this API, you can pass a Base64\-encoded [GPU driver installation script](https://docs.byteplus.com/en/docs/gpu/Automatically_installing_Tesla_drivers_during_instance_creation#1rTgcdc4) through the `Userdata` parameter to automatically install the specified versions of the GPU driver, CUDA, and cuDNN libraries.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

This operation is asynchronous. After you send a request, an instance ID is returned. However, this does not indicate that the instance is created. This is because the instance cannot be created and started immediately. To view the instance status, you can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation. When the return of `Status` is `RUNNING`, the instance is created and started.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=RunInstances&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|AsNZvQ">必选</span>` Sample value: RunInstances`

The action that you want to perform. Value: RunInstances.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|rvjsI6">必选</span>  `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**AffinityGroupSize ** <span data-label="purple">integer </span>`Optional` `Sample value: 2`

Affinity group specification. Value: 2.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only HPC\-optimized NPU hpcpci3 instances (Beta) support affinity groups.</div>


* <div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, please contact your account manager.</div>




**AutoRenew ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to automatically renew the instance after it expires. Value:


* true: Enables automatic renewal

* false (default): Disables automatic renewal


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only when the value of <code>InstanceChargeType</code> is <code>PrePaid</code>.</div>




**AutoRenewPeriod ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The duration for each automatic renewal.


* When `AutoRenew` is set to `True`, this parameter is valid. The default value is 1.

* When `PeriodUnit` is set to `Month`, this parameter takes one of the values 1, 2, 3, 6, or 12.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure request idempotency. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Count ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

Number of instances to be created. Value: 1–100. When 0 is passed in, the default number is 1.



**CpuMaxFrequency ** <span data-label="purple">float </span>`Optional` `Sample value: 2.8`

Specify the maximum CPU frequency in GHz. The valid range is between the processor base frequency and turbo frequency.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only g3al (4xlarge, 8xlarge, 16xlarge, 32xlarge), c3al (4xlarge, 8xlarge, 16xlarge, 32xlarge), r3al (4xlarge, 8xlarge, 16xlarge), g4i, c4i, r4i, g4ie, c4ie, and r4ie instances support this parameter. For more information on processor base frequency or turbo frequency, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types</a>.</div>


* <div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, please contact your account manager to apply.</div>




**CreditSpecification ** <span data-label="purple">string </span>`Optional` `Sample value: Standard`

The running mode of Burstable instances. Value:


* Standard: the standard mode

* Unlimited: the unlimited performance mode (currently unavailable)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>InstanceTypeId</code> is ecs.t2 instance family (burstable instance).</div>


* <div data-tips="true" data-tips-type="tip">When no parameter is passed or this parameter is empty, the burstable instance defaults to <code>Standard </code>mode.</div>




**DeletionProtection ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

The attribute of instance deletion protection. Specify whether to delete the instance through the console or API. Valid values:


* true: Enable instance deletion protection.

* false (default): Disable instance deletion protection.



**DeploymentSetGroupNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

When the deployment set policy that an ECS instance is to join or adjust to is the availability group (AvailabilityGroup), this parameter can be used to specify the group number of the instance in the deployment set. The value is from 1 to 7.



**DeploymentSetId ** <span data-label="purple">string </span>`Optional` `Sample value: dps-yc1o9aahks5m57nk****`

The ID of the deployment set that the instance is added to.



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: ECS instance for testing.`

Description of the instance. Default value: empty string.


* Must start with a letter or a Chinese character.

* Only Chinese characters, letters, digits, dots (.), spaces, underscores (_), hyphens (\-), equal signs (=), English commas (,), Chinese commas (，), and Chinese periods (。) are allowed.

* The length is limited to 255 characters.



**DryRun ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Specifies whether to precheck this request. Valid values:


* true: sends a check request without instance creation. Check items include: whether required parameters are specified, request format, business restrictions, and ECS inventory. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the value of<code> DryRun</code> is <code>true </code>and a value is set for the <code>Count </code>or<code> Mincount </code>parameter, the value must be 1.   </div>
   

* false (default): Send a normal request and directly create an instance after the check passes.



**EipAddress.BandwidthMbps ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The maximum bandwidth for the EIP, in Mbps. Default value is 1.


* When `ChargeType` is set to `PayByBandwidth`: 1–500.

* When `ChargeType` is set to` PayByTraffic`: 1–200.



**EipAddress.BandwidthPackageId ** <span data-label="purple">string </span>`Optional` `Sample value: bwp-2zeo05qre24nhrqpy****`

ID of the shared bandwidth package. This indicates adding the EIP to the specified shared bandwidth package.


* You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) operation to query the ID of shared bandwidth package.

* To associate an EIP with a shared bandwidth package, the following conditions must be met:

   * The EIP and the shared bandwidth package must have the same security protection type.

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

The ISP for EIP, which by default is BGP. Valid values:


* BGP: BGP (Multi\-ISP).

* If your account has applied for and enabled permission for the static single\-ISP, you can pass in the following values:

   * ChinaMobile: China Mobile static single\-ISP.

   * ChinaTelecom: China Telecom static single\-ISP.

   * ChinaUnicom: China Unicom static single\-ISP.

* If your account has applied for and enabled permission for the BGP single\-ISP, you can pass in SingleLine_BGP.

* If your account has applied for and enabled static BGP permission, you can pass in Static_BGP.



**EipAddress.ReleaseWithInstance ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether the EIP is deleted along with the instance. This feature is only available for pay\-as\-you\-go EIPs. Valid values:


* true: The EIP is deleted along with the instance. When an instance is automatically reclaimed by the system (for example, 24 hours after unsubscription or upon expiration) or deleted via the [DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) or [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API, the EIP is released along with the instance.

* false (default): The EIP is not deleted when the instance is deleted.



**EipAddress.SecurityProtectionInstanceId ** <span data-label="purple">integer </span>`Optional` `Sample value: 20`

ID of the Anti\-DDoS Origin (Enterprise Edition).


* You can call the DescInstanceList operation to query the ID of DDoS Native Protection (Enterprise Edition).

* When `SecurityProtectionTypes` is set to `AntiDDoS_Enhanced`, this parameter is required.



**EipAddress.SecurityProtectionTypes.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: SecurityProtectionTypes.1 =AntiDDoS_Enhanced`

The security protection type of EIP.


* N specifies the serial number of the protection type. Currently, only 1 is supported.

* Valid values:

   * AntiDDoS_Enhanced: Apply for an EIP with enhanced protection, which can be added to a Anti\-DDoS Origin (Enterprise Edition) instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If <code>EipAddress.SecurityProtectionTypes.N</code> is passed in <code>AntiDDoS_Enhanced</code>, then <code>EipAddress.ChargeType</code> must not be <code>PrePaid</code>, and <code>EipAddress.ISP</code> must pass in <code>BGP</code>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">EIPs with enhanced protection are currently in Beta. If you need a trial, please contact your account manager.      </div>
      

   * If this parameter is not passed in, the system applies for an EIP of the default protection type.



**EnablePrimaryInterfaceHighBandwidthType ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether the primary network interface can be specified as the high\-bandwidth type Valid values:


* true: Supported.

* false (default): Not supported.



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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If no argument is filled in, the hostname is automatically generated based on the rule of "iv\- + initial hostname". For example,</div>


   <div data-tips="true" data-tips-type="tip">iv\-3tigy72q3u3vj0\*\*\*\*\*\*.   </div>
   

* <div data-tips="true" data-tips-type="tip">Generation logic of the initial hostname:</div>


   * <div data-tips="true" data-tips-type="tip">Linux instances: Extract all characters after instance ID i\-.</div>


   * <div data-tips="true" data-tips-type="tip">Windows instances: Extract the last 12 characters after instance ID i\-.</div>


* <div data-tips="true" data-tips-type="tip">When creating instances in a batch, you can set sequential hostnames in the <code>name_prefix[begin_number,bits]name_suffix</code> format. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames">Configuring sequential instance names or hostnames in a batch</a>.</div>




**HpcClusterId**<span data-label="purple"> string </span>`Optional Sample value: hpcCluster-l8u24ovdmoab6opf****`

ID of the HPC cluster to which the instance belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect and is required only for the creation of HPC\-optimized instances.</div>




**HttpTokens ** string `Optional` `Sample value: optional`

The access mode of instance metadata. You can set whether to enable the security hardening mode. Valid values:


* optional (default): Not mandatory (Normal Mode and Security Hardening Mode). This allows instance metadata access either directly through the standard method or via the token\-based authentication method.

* required: Mandatory (Security Hardening Mode). This only allows instance metadata access through a token\-based authentication method.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For information on how to view metadata and the available metadata items, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata">Viewing instance metadata</a>.</div>


* <div data-tips="true" data-tips-type="tip">Security Hardening Mode is currently in Beta. If you need a trial, please contact your account manager to apply.</div>




**ImageId**<span data-label="purple"> string</span><span data-api-tag="require|Aiq9Rk">必选</span> ` Sample value: image-3tefr6wgx63vj0x1****`

ID of the image used for instance startup

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/ecs/DescribeImages">DescribeImages</a> operation and enter the ID of needed instance type in the <code>InstanceTypeId</code> to query the corresponding images supported and the image ID.</div>




**ImageReleaseVersion ** <span data-label="purple">string </span>`Optional` `Sample value: 20241115`

The specific version number of the image used.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter only takes effect when the used image is a public image.</div>


* <div data-tips="true" data-tips-type="tip">If this parameter is empty, the latest version of the image is used.</div>




**InstallRunCommandAgent ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to install cloud assistant Agent on startup during instance creation. Value:


* true: Install during creation.

* false (default): Do not install during creation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about Cloud assistant, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant">Cloud assistant overview</a>.</div>




**InstanceChargeType ** <span data-label="purple">string </span>`Optional` `Sample value: PostPaid`

The billing methods for instance and volume. Value:


* PostPaid: Pay\-as\-you\-go.

* PrePaid: Subscription. Please make sure that your account supports balance payment or credit control payment. Otherwise, an error message "InvalidInstanceChargeType" is returned.



**InstanceName ** <span data-label="purple">string  </span><span data-api-tag="require|30Z68Q">必选</span>`Sample value: instance-test`

The instance name.


* Start with a letter or a Chinese character.

* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If <code>SuffixIndex</code> is set for the instance, the instance name length includes the suffix.</div>


* <div data-tips="true" data-tips-type="tip">When creating instances in a batch, you can set sequential instance names in the <code>name_prefix[begin_number,bits]name_suffix</code> format. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames">Configuring sequential instance names or hostnames in a batch</a>.</div>




**InstanceTypeId ** <span data-label="purple">string </span><span data-api-tag="require|ab4Eqx">必选</span> `Sample value: ecs.g1ie.xlarge`

Instance type.


* Instance type selection: You can refer to the [ECS instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types) or call the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) operation to view the performance data of instance types. You can also refer to [Best practices for instance type selection](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice) for selection guide.

* Inventory query: You can call the [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) operation to query the inventory information of computing resources in the availability zone.



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




**MinCount ** <span data-label="purple">integer </span>`Optional Sample value: 2`

Specify the minimum number of ECS instances that can be created. Value:


* `MinCount `(the minimum number of ECS instances that can be created) is less than or equal to `Count` (the number of instances to be created).

* When available inventory exceeds `Count` (the number of instances to be created), instances are created based on `Count`.

* When available resources are between `MinCount` (the minimum number of ECS instances that can be created) and `Count` (the number of instances to be created), instances are created based on available inventory resources.

* When available resources are less than `MinCount `(the minimum number of ECS instances that can be created), a creation failure occurs due to insufficient inventory.



**NetworkInterfaces.N.SecurityGroupIds.N ** <span data-label="purple">string[]</span><span data-api-tag="require|ONbXHD">必选</span>  `Sample value: NetworkInterfaces.1.SecurityGroupIds.1=sg-3ti78x9h8t4bw*****&NetworkInterfaces.2.SecurityGroupIds.1=sg-3cj59ih2v9hj46c6rr******`

ID of the security group associated with the network interface.


* The first N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* The second N: indicates the serial number of the security group associated with the network interface. Value: 1–5.

* Separate multiple security group IDs with ampersands (&).



**NetworkInterfaces.N.SubnetId ** <span data-label="purple">string[] </span><span data-api-tag="require|Qi6mCM">必选</span> `Sample value: NetworkInterfaces.1.SubnetId=subnet-3tispp1nai4e8i******& NetworkInterfaces.2.SubnetId=subnet-2ff1nczrx2lts5oxru******`

The ID of the subnet of the instance VPC. When creating an instance, you can associate secondary network interfaces with it.


* Argument \- N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* Separate multiple VPC subnet IDs with ampersands (&).



**NetworkInterfaces.N.Ipv6AddressCount ** <span data-label="purple">integer[] </span>`Optional` `Sample value: NetworkInterfaces.1.Ipv6AddressCount=1`

The number of private IPv6 addresses assigned to the primary network interface, which can only be 1.


* If this parameter is passed in, the system automatically allocates the corresponding number of idle private IPv6 addresses from the subnet that the network interface belongs to. Then the system assigns idle private IPv6 addresses as the private IPv6 addresses of the network interface.

* When you create an instance, you can assign IPv6 address to the primary network interface only. To assign an IPv6 address to a secondary network interface, refer to [CreateNetworkInterface](https://docs.byteplus.com/en/docs/vpc/CreateNetworkInterface).

* Argument \- N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface. Therefore, when N ≥ 2 is passed in, this parameter is ignored.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The feature of assigning IPv6 addresses to the network interface is currently in Beta. If you need a trial, please contact your account manager.</div>




**NetworkInterfaces.N.PrimaryIpAddress ** <span data-label="purple">string[] </span>`Optional` `Sample value: NetworkInterfaces.1.PrimaryIpAddress=192.168.XX.XX`

The specified primary IP address of the network interface. Currently, primary IP addresses can only be assigned for primary network interfaces or secondary network interfaces.


* Argument \- N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* Separate multiple network interfaces with ampersands (&).



**NetworkInterfaces.N.PrivateIpAddresses.N**<span data-label="purple"> string[] </span>`Optional Sample value: NetworkInterfaces.1.PrivateIpAddresses.1=172.16.XX.XX&NetworkInterfaces.1.PrivateIpAddresses.2=172.16.XX.XX`

The specified secondary IP address of the primary network interface. Currently, only secondary IPs for the primary network interface are supported.


* The first N: indicates the serial number of the primary network interface. Currently, one ECS instance can only be associated with one primary network interface.

* The second N: indicates the serial number of the secondary IP address for the primary network interface. The maximum number of secondary IP addresses that can be assigned is equal to the number of private IP addresses supported by a network interface for this [instance type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types), minus one (for the primary private IP address).

* Separate multiple secondary IP addresses with ampersands (&).



**NetworkOptions.EnableJumboFrame ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether jumbo frames are enabled for the instance. Valid values:


* false: Jumbo frames are not enabled. The MTU value of all network interfaces of the instance is 1500.

* true: Jumbo frames are enabled. The MTU value of all network interfaces of the instance is 8500.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is only supported for certain instances. For instances that support jumbo frames, see <a href="https://docs.byteplus.com/en/docs/ecs/Enabling_or_Disabling_jumbo_frames">Enabling/disabling jumbo frames</a>.</div>




**Password ** <span data-label="purple">string</span>` Optional Sample value: password@123`

If you need to log in to an instance with "Password", specify the initial login password of the administrator account through this parameter. The Linux administrator account is root, and the Windows administrator account is Administrator.

Password complexity requirements are as follows:


* The length limit is 8 to 30 characters.

* Passwords can only consist of uppercase letters, lowercase letters, numbers, and special characters, and must include at least three of these elements.

* Valid special characters: `~!@#$%^&\*()_\-+=|{}[]:;'<\>,.?/

* The password cannot start with "/" or "$6$".


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For login credentials, "Password", "Key Pair", and "Keep image settings" are available. If you choose to use a password, specify a complex password to improve security.</div>




**Period ** <span data-label="purple">integer </span>`Optional` `Sample value: 12`

The subscription duration of resource (unit: month).


* Value: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, 60

* Default value: 1


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect and is required only when the value of <code>InstanceChargeType</code> is <code>PrePaid</code>.</div>




**PeriodUnit ** <span data-label="purple">string</span>` Optional Sample value: Month`

The unit of purchase duration of resources. Value: Month (default).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect and is required only when the value of <code>InstanceChargeType</code> is <code>PrePaid</code>.</div>




**Placement.Affinity ** <span data-label="purple">string </span>`Optional` `Sample value: Default`

For ECS instances in economical mode, some resources are released after instances are stopped. You can use this parameter to select whether the instances are still deployed on the original host when restarted. Valid values:


* Host: When instances in economical mode are restarted, they are still deployed on the original host.

* Default: When the instance with Economical Mode enabled restarts, it will be preferentially migrated to a host that supports automatic deployment. If resources on the host that supports automatic deployment are insufficient, the instance restarts on the original host.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: project_a`

The project to which the resource belongs. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**SecurityEnhancementStrategy ** <span data-label="purple">string </span>`Optional` `Sample value: Active`

Whether to enable security enhancement. Value:


* Active: Enables security enhancement. This feature is effective for public images only.

* InActive: Disables security enhancement. This feature is effective for all image types.



**SpotPriceLimit ** <span data-label="purple">double </span>`Optional` `Sample value: 0.78`

The maximum hourly price for spot instances. A maximum of three decimal places for the price is supported.

This parameter takes effect only when `SpotStrategy` is set to `SpotWithPriceLimit`.



**SpotStrategy ** <span data-label="purple">string </span>`Optional` `Sample value: NoSpot`

The spot strategy for the instance billed in pay\-as\-you\-go mode. Value:


* NoSpot (default): Creates a regular Pay\-as\-you\-go instance.

* SpotAsPriceGo: The system automatically bids based on the current market price for the spot instance.

* SpotWithPriceLimit: Spot instance with a price limit.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>InstanceChargeType</code> is set to <code>PostPaid</code>, this parameter takes effect.</div>


* <div data-tips="true" data-tips-type="tip">For details on bidding patterns of spot instances, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance">Purchasing spot instances</a>.</div>




**SuffixIndex ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The starting number of the sequential suffix, with the value from 1 to 999. Default value: 1



**Tags.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The key of the tag.


* Parameter \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with ampersands (&).


Naming rules:


* It cannot start with `volc:` or `sys:` in any combination of uppercase and lowercase letters.

* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The user tag value.


* Parameter \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with &.


Naming rules:


* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

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




**UserData ** <span data-label="purple">string </span>`Optional Sample value: ZWNobyBoZWxsbyBlY3Mh`

Instance custom data. The specified custom data must be Base64 encoded, and the size of the custom data before Base64 encoding must not exceed 16 KB.

If left blank, the parameter defaults to an empty value.



**Volumes.N.Size**<span data-label="purple"> integer[]</span><span data-api-tag="require|7SGvcO">必选</span> ` Sample value: Volumes.1.Size=100&Volumes.2.Size=100`

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

The type of additional performance for the volume. This feature is only supported by ESSD FlexPL data volumes. Valid values:


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

The volume type. Valid values:


* ESSD_PL0 (default): ESSD PL0

* ESSD_FlexPL: ESSD FlexPL


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume, and N ≥ 2 indicates the data volume.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**ZoneId ** <span data-label="purple">string </span><span data-api-tag="require|SEw5c2">必选</span> `Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceIds ** <span data-label="purple">string[] </span>`Sample value: [ "i-3tigy72q3u3vj0x2****","i-3tigy72q3u3vj0x2****" ]`

The ID of the instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=RunInstances&Version=2020-04-01&ZoneId=cn-beijing-a&ImageId=image-3tefr6wgx63vj0******&InstanceTypeId=ecs.g1ie.xlarge&InstanceName=instance-test&Count=1&Password=password@123&NetworkInterfaces.1.SubnetId=subnet-3tispp1nai4e8i****&NetworkInterfaces.1.SecurityGroupIds.1=sg-3ti78x9h8t4bw*****&Volumes.1.VolumeType=ESSD_PL0&Volumes.1.Size=40&EipAddress.ChargeType=PayByBandwidth&EipAddress.BandwidthMbps=5 HTTP/1.1
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
        "Action": "RunInstances",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceIds": [
            "i-3tigy72q3u3vj0******",
            "i-3tigy72q3u3vj0******"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidBandwidthPackageStatus |The status of the specified bandwidth package does not support this request. |The status of the specified bandwidth package does not support this request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidCount.Malformed |The specified count is malformed. |The specified Count is invalid. |
|400 |InvalidCreditSpecification.Malformed |The specified credit specification is malformed. |The specified mode of the burstable instance is invalid. |
|400 |InvalidDedicatedHostStatus.Unsupported |The status of the specified dedicated host does not support this request. |The dedicated host in the current status does not support this action. |
|400 |InvalidDeploymentSetGroupNumber |The specified DeploymentSetGroupNumber is invalid. |The specified deployment set group is invalid. |
|400 |InvalidEipAddressChargeType.Malformed |The specified ChargeType of elastic ip is malformed. |The specified billing method of EIP is invalid. |
|400 |InvalidExtraPerformanceTypeId.Malformed |The specified ExtraPerformanceTypeId is malformed. |The specified type of additional performance package is invalid. |
|400 |InvalidExtraPerformanceValue.Malformed |The specified ExtraPerformance Value is malformed. |The specified ExtraPerformance value is invalid. |
|400 |InvalidHostname.Malformed |The specified Hostname is malformed. |The specified hostname is invalid. |
|400 |InvalidHttpTokens.Malformed |The specified HttpTokens is malformed, you can use optional(default) or required. |The specified value for HttpTokens is invalid. Please use optional (default) or required. |
|400 |InvalidHttpTokensForImage.Unsupported |The specified image does not support security hardening mode for accessing metadata. |The specified image does not support access of instance metadata through Security Hardening Mode. |
|400 |InvalidImageForConfidentialComputing.UnSupported |The specified image does not support confidential computing. |The specified image does not support confidential computing. |
|400 |InvalidInstanceChargeType |The specified InstanceChargeType is invalid. |The specified instance billing method is invalid. |
|400 |InvalidInstanceDescription.Malformed |The specified InstanceDescription is malformed. |The specified instance description is not valid. |
|400 |InvalidInstanceName.Malformed |The specified InstanceName is malformed. |The specified instance name is invalid. |
|400 |InvalidInstanceType.ImageMismatch |The specified InstanceType and Image do not match. |The specified instance type and image do not match. |
|400 |InvalidInstanceTypeForAffinityGroupSize.Unsupported |The specified instance type does not support the affinity group size. |The specified instance type does not match the specification required by the affinity group. |
|400 |InvalidInstanceTypeForConfidentialComputing.NotSupported |The specified instance type does not support confidential computing. |The specified instance type does not support confidential computing. |
|400 |InvalidInstanceTypeForCreateSpotInstance.Unsupported |The specified InstanceType does not support creation of spot instances. |The specified instance type does not support the creation of spot instances. |
|400 |InvalidInstanceTypeForNonAffinityGroup.Unsupported |The specified instance type does not support the non affinity group. |For the specified instance type, instances that you want to create must be added to an affinity group. |
|400 |InvalidIpv6AddressCount.Malformed |The specified Ipv6AddressCount is malformed. |The specified number of IPv6 addresses is invalid. |
|400 |InvalidIpv6OnlySubnet.Unsupported |The specified ipv6 only subnet is unsupported. |Currently, you cannot create an instance associated with the IPv6\-only subnet. |
|400 |InvalidKeyPairForWindows.Unsupported |The OSType of this specified instance is Windows, which does not support key pairs. |The specified instance is based on the Windows operating system and does not support key pairs. |
|400 |InvalidMinCount.Malformed |The specified MinCount is malformed. |The specified minimum purchase quantity for the instance is invalid. |
|400 |InvalidNetworkInterfaceType |The type of specified elastic network interface is illegal for the request. |The specified type of elastic network interface cannot respond to this request. |
|400 |InvalidParameterCombination |Indicates an incorrect combination of parameters. |The parameter combination is incorrect, or a parameter is missing. |
|400 |InvalidPassword.Malformed |The specified password is malformed. |The specified password format is invalid. |
|400 |InvalidPeriod |The specified period is not valid. |The specified number of billing cycles is invalid. |
|400 |InvalidPeriodUnit |The specified PeriodUnit is not valid, is unsupported, or cannot be used. |The specified billing cycle is invalid. |
|400 |InvalidPlacementAffinity.Malformed |The specified placement affinity is malformed. |The specified Placement.Affinity is invalid. |
|400 |InvalidPlacementTenancy.Malformed |The specified placement tenancy is malformed. |The specified Placement.Tenancy is invalid. |
|400 |InvalidPrimaryInterfaceHighBandwidthType.Unsupported |The specified instance type does not support specify primary to interface high bandwidth type. |The specified instance type does not support the primary network interface of the high\-bandwidth type. |
|400 |InvalidProjectName |The specified ProjectName is invalid. |The specified project name is invalid. |
|400 |InvalidSecurityEnhancementStrategy.Malformed |The specified SecurityEnhancementStrategy is malformed. |The specified security enhancement policy is invalid. |
|400 |InvalidSecurityGroupStatus |The specified security group is not in the correct status for the request. |The specified security group is not in the correct status for the request. |
|400 |InvalidSecurityGroupType.Malformed |The specified SecurityGroupType is malformed. |The specified security group type is invalid. |
|400 |InvalidSecurityProtectionInstanceStatus |The specified security protection instance is not in the correct status for the request. |The specified security protection instance is not in the correct status for the request. |
|400 |InvalidSecurityProtectionTypes.Malformed |The specified security protection type is malformed. |The specified security protection level is not supported. |
|400 |InvalidSnapshotStatus |The status of the specified snapshot does not support this request. |The specified snapshot status does not support this operation. |
|400 |InvalidSpotPriceLimit.Malformed |The specified SpotPriceLimit is malformed. |The specified spot instance price is invalid. |
|400 |InvalidSpotStrategy.Malformed |The specified SpotStrategy is malformed. |The specified spot strategy is invalid. |
|400 |InvalidSubnetStatus |The specified subnet is not in the correct status for the request. |The specified subnet is not in the correct status for the request. |
|400 |InvalidSuffixIndex.Malformed |The specified SuffixIndex is malformed. |The specified sequential suffix is invalid. |
|400 |InvalidSystemVolumeForExtraPerformance.Unsupported |The specified SystemVolume does not support extra performance. |The specified system volume does not support purchase of additional performance. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidTopologyType.Malformed |The specified TopologyType is malformed. |The specified TopologyType is invalid. |
|400 |InvalidUserData.Malformed |The specified UserData is malformed. |The specified UserData is invalid. |
|400 |InvalidVolumeKindForExtraPerformance.Unsupported |The specified VolumeKind does not support extra performance. |The specified volume type does not support the purchase of additional performance. |
|400 |InvalidVolumeReleaseType.Malformed |The specified VolumeReleaseType is malformed. |The specified type of volume release is invalid. |
|400 |InvalidVolumeSizeForExtraPerformance.Unsupported |The specified VolumeSize does not support extra performance. |The specified volume capacity does not support the purchase of additional performance. |
|400 |InvalidVolumeStatus |The status of the specified volume does not support this request. |The volume in current status does not support this action. |
|400 |InvalidVolumeType.Malformed |The specified VolumeType is malformed. |The specified volume type is invalid. |
|400 |InvalidVolumeTypeForExtraPerformance.Unsupported |The specified VolumeType does not support extra performance. |The specified volume type does not support the purchase of additional performance. |
|400 |InvalidVolumeTypeForSnapshot.UnSupported |The specified VolumeType cannot be used for create snapshot. |The specified volume type does not support snapshots. |
|400 |LimitExceeded.DataVolumeSize |The specified data volume size exceeds the limit. |The specified data volume size (GiB) exceeds the limit. |
|400 |LimitExceeded.ExtraPerformance |You've reached the limit on the number of ExtraPerformance that you can set. |The maximum limit of additional performance is reached. |
|400 |LimitExceeded.ExtraPerformanceThroughput |You've reached the limit on the number of ExtraPerformanceThroughput that you can set. |The throughput has reached the maximum limit. No additional performance required. |
|400 |LimitExceeded.MaximumDeploymentSetInstances |You've reached the limit on the number of instances that can be added to the deployment set. |The number of instances in the specified deployment set exceeds the maximum limit. |
|400 |LimitExceeded.MaximumEipBandwidth |The specified elastic ip bandwidth value exceeds the maximum limit. |The specified EIP bandwidth value exceeds the maximum limit. |
|400 |LimitExceeded.MaximumExtraPerformanceIOPS |The number of specified ExtraPerformanceIOPS exceeds the maximum limit. |The specified additional performance IOPS exceeds the maximum limit. |
|400 |LimitExceeded.MaximumExtraPerformanceThroughputMB |The number of specified ExtraPerformanceThroughputMB exceeds the maximum limit. |The specified additional performance throughput exceeds the maximum limit. |
|400 |LimitExceeded.MaximumHighPerformanceNetworkInterfaces |You've reached the limit on the number of HighPerformance NetworkInterfaces that can be attached to the instance. |The number of network interfaces in RDMA communication mode associated with the specified instance exceeds the upper limit. |
|400 |LimitExceeded.MaximumNetworkInterfaces |You've reached the limit on the number of NetworkInterfaces that can be attached to the instance. |The specified number of network interfaces associated with the instance exceeds the upper limit. |
|400 |LimitExceeded.MaximumSecurityProtectionTypes |You've reached the limit on the number of SecurityProtectionTypes that you can set. |The specified number of SecurityProtectionTypes exceeds the maximum limit. |
|400 |LimitExceeded.MaximumSubnetIps |The number of specified subnet IP addresses exceeds the maximum limit. |The specified number of subnet IP addresses reaches the maximum limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |LimitExceeded.MaximumVolumes |You've reached the limit on the number of volumes that can be attached to the instance. |The specified number of volumes mounted to the instance exceeds the upper limit. |
|400 |LimitExceeded.MinimumEipBandwidth |The specified elastic ip bandwidth value exceeds the minimum limit. |The bandwidth value of the specified EIP exceeds the minimum limit. |
|400 |LimitExceeded.MinimumExtraPerformanceIOPS |The number of specified ExtraPerformanceIOPS exceeds the minimum limit. |The specified additional performance IOPS exceeds the minimum limit. |
|400 |LimitExceeded.MinimumExtraPerformanceThroughputMB |The number of specified ExtraPerformanceThroughputMB exceeds the minimum limit. |The specified additional performance throughput exceeds the minimum limit. |
|400 |LimitExceeded.SystemVolumeSize |The specified system volume size exceeds the limit. |The specified system volume size (GiB) exceeds the limit. |
|400 |MissingParameter.HpcClusterId |The required parameter HpcClusterId is not supplied. |HPC Cluster ID cannot be empty. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|400 |MissingParameter.InstanceName |The required parameter InstanceName is not supplied. |The instance name cannot be empty. |
|400 |MissingParameter.InstanceTypeId |The required parameter InstanceTypeId is not supplied. |The ID of the instance type cannot be empty. |
|400 |MissingParameter.NetworkInterfaces |The required parameter NetworkInterfaces is not supplied. |Network interface information cannot be empty. |
|400 |MissingParameter.PasswordAndKeyPair |The required parameter PasswordAndKeyPair is not supplied. |The password and key pair cannot both be empty. |
|400 |MissingParameter.SecurityGroupIds |The required parameter SecurityGroupIds is not supplied. |The security group ID cannot be empty. |
|400 |MissingParameter.SubnetId |The required parameter SubnetId is not supplied. |The subnet ID cannot be left empty. |
|400 |MissingParameter.VolumeType |The required parameter VolumeType is not supplied. |The volume type cannot be empty. |
|400 |MissingParameter.Volumes |The required parameter Volumes is not supplied. |Volume information cannot be empty. |
|400 |MissingParameter.ZoneId |The required parameter ZoneId is not supplied. |Availability zone ID cannot be empty. |
|400 |OperationDenied.PurchaseLimited |You are not authorized to purchase ecs. |The permission to purchase an ECS instance is not granted. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the number of instances that you can create, please submit ticket to request an increase in quota. |The number of bandwidth packages you can create reaches the limit. Please submit a ticket to increase the quota. |
|400 |QuotaExceeded.MaximumEipAddresses |You've reached the limit on the number of EIP address that you can create, please submit ticket to request an increase in quota. |The number of EIP addresses you can create reaches the limit. Please submit a ticket to increase the quota. |
|400 |QuotaExceeded.MaximumEipInterfaceLimit |You've reached the limit of calling EIP API, please submit a ticket to increase the limit. |The number of EIP API requests reaches the limit. Please submit a ticket to increase the limit. |
|400 |QuotaExceeded.MaximumEips |You've reached the limit on the number of EIP that you can create, please submit ticket to request an increase in quota. |Insufficient EIP quota. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumGeneralCpus |You've reached the limit on the number of general instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu] quota. |The CPU quota of the General\-purpose instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic] quota. |The GPU card quota for GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance] quota. |The GPU card quota for HPC\-optimized instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceCpus |You've reached the limit on the number of instance CPU that you can create, please submit ticket to request an increase in quota. |The quota of instance CPU number is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceTypeInstances |You've reached the limit on the number of instance type instances that you can create, please submit ticket to request an increase in quota. |The quota of the specified instance type that you can create is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumInstances |You've reached the limit on the number of instances that you can create, please submit ticket to request an increase in quota. |The quota of the instance number is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumLocalVolumeCpus |You've reached the limit on the number of local volume instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu] quota. |The CPU quota of the Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumNetworkInterfaces |You've reached the limit on the number of elastic network interface that you can create, please submit ticket to request an increase in quota. |Network interface quota is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGeneralCpus |You've reached the limit on the number of general reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu_ri_regional] quota. |The CPU quota of the general\-purpose instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic_ri_regional] quota. |The GPU card quota of regional RIs that can be used for purchasing GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU reserved instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance_ri_regional] quota. |The GPU card quota for HPC\-optimized instances that can be deducted by regional RIs is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus |You've reached the limit on the number of local volume reserved instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [local_volume_vcpu_ri_regional] quota. |The CPU quota of regional RIs that can be used for purchasing Local SSD instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumSecurityGroupIps |You've reached the limit on the number of SecurityGroupIps that you can create, please submit ticket to request an increase in quota. |The IP addresses that can be associated with security groups are insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumSecurityGroupNetworkInterfaces |You've reached the limit on the number of SecurityGroupEnis that you can create, please submit ticket to request an increase in quota. |The quota for network interfaces that can be associated with the security group is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumSecurityGroups |You've reached the limit on the number of SecurityGroups that you can create, please submit ticket to request an increase in quota. |Security group quota is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumVolumes |You've reached the limit on the capacity of Volumes that you can create, please submit ticket to request an increase in quota. |The volume quota is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.SecurityProtectionInstance |You've reached the limit on the number of security protection instance that you can add. |The maximum limit on the number of instances that can enable security protection is reached. |
|403 |AccessDeniedErr |User is not authorized to perform: vpc:AllocateEipAddress on resource: [] |The user does not have permission to call the vpc:AllocateEipAddress operation to create a cloud host with an EIP. |
|403 |InvalidChargeTypeForDeletionProtection.Unsupported |Deletion protection is only valid for postPaid instance. |The deletion protection feature can only be used on general pay\-as\-you\-go resources. |
|403 |RequestForbidden |Request is forbidden by the server. |Your ECS services are suspended because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|404 |InvalidBandwidthPackage.NotFound |The specified BandwidthPackage does not exist. |The specified Shared Bandwidth Package does not exist. |
|404 |InvalidDedicatedHost.NotFound |The specified dedicated host does not exist. |The specified dedicated host does not exist. |
|404 |InvalidDedicatedHostCluster.NotFound |The specified dedicated host cluster does not exist. |The specified DDH cluster does not exist. |
|404 |InvalidDeploymentSet.NotFound |The specified DeploymentSet does not exist. |The specified deployment set does not exist. |
|404 |InvalidHpcCluster.NotFound |The specified HpcCluster does not exist. |The specified HPC cluster does not exist. |
|404 |InvalidISP.NotFound |The specified ISP does not exist. |The specified ISP does not exist. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|404 |InvalidKeyPair.NotFound |The specified KeyPair does not exist. |The specified key pair does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSecurityGroup.NotFound |The specified SecurityGroup does not exist. |The specified security group does not exist. |
|404 |InvalidSecurityProtectionInstance.NotFound |The specified security protection instance does not exist. |The specified instance that enables security protection does not exist. |
|404 |InvalidSnapshot.NotFound |The specified Snapshot does not exist. |The specified snapshot does not exist. |
|404 |InvalidSubnet.DisableIPv6 |Specified subnet disable IPv6. |The subnet does not have IPv6 enabled. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|409 |InvalidNetworkInterfacesVpc.Conflict |Multiple vpcs are not supported for instances in the same HpcCluster. |RDMA instances in the same high\-performance cluster cannot be associated with multiple VPCs. |
|409 |InvalidPrimaryIpAddress.Conflict |The specified PrimaryIpAddress already exists. |The specified PrimaryIpAddress already exists. |
|409 |InvalidPrivateIpAddresses.Conflict |The specified PrivateIpAddresses already exists. |The specified PrivateIpAddresses already exists. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |Insufficient.AclCapacity |You've reached the limit number of ACLs on the switch. |The number of ACLs on the switch exceeds the limit. |
|412 |InvalidAffinityGroupSize.CountMismatch |The specified AffinityGroupSize and Count conflict. |The specified affinity group specification does not match the instance number. The number of instances must be an integer multiple of the affinity group specification. |
|412 |InvalidAffinityGroupSize.DeploymentSetIdMismatch |The specified AffinityGroupSize and DeploymentSetId conflict. |Affinity group and deployment set can not be enabled for one instance at the same time. |
|412 |InvalidAffinityGroupSize.MinCountMismatch |The specified AffinityGroupSize and MinCount conflict. |Affinity group and minimum creation number cannot be enabled at the same time. |
|412 |InvalidCreditSpecification.InstanceTypeIdMismatch |The specified credit specification and instance type id do not match. |The specified mode of the burstable instance does not match the instance type. |
|412 |InvalidDedicatedHost.InstanceTypeIdMismatch |The specified DedicatedHostId does not match InstanceTypeId. |The ID of the specified dedicated host does not match the instance type. |
|412 |InvalidDedicatedHostCluster.InstanceTypeIdMismatch |The specified DedicatedHostClusterId does not match InstanceTypeId. |The dedicated host cluster with the specified ID does not match the instance type. |
|412 |InvalidDedicatedHostClusterId.DedicatedHostIdMismatch |The specified DedicatedHostClusterId does not match DedicatedHostId. |The specified dedicated host cluster does not match the dedicated host. |
|412 |InvalidEnableVrdma.JumboFrameMismatch |The specified request includes an unsupported operation. It is not supported to enable vRDMA ENI without jumbo frame on the ECS. |You must enable JumboFrame before enabling vRDMA. |
|412 |InvalidHpcCluster.InstanceTypeIdMismatch |The specified HpcClusterId does not match InstanceTypeId. |The HPC cluster does not match the instance type. |
|412 |InvalidHpcCluster.VpcMismatch |The specified Vpc and the Vpc of HpcCluster do not match. |The VPC does not match. The specified VPC and the VPC of HPC cluster do not match. |
|412 |InvalidHpcCluster.ZoneMismatch |The specified HpcCluster and Instance's ZoneId do not match. |The HPC cluster is not within the scope of the instance availability zone. |
|412 |InvalidISP.BandwidthPackageMismatch |The specified ISP of EIP and bandwidth package do not match. |The specified ISPs for the EIP and bandwidth package do not match. |
|412 |InvalidImage.InstanceTypeMismatch |The specified image and instance type do not match. |The specified image does not support the specified instance type. |
|412 |InvalidImageArchitecture.InstanceTypeArchitectureMismatch |The specified image architecture and instance type architecture do not match. |The architecture type of the image is not supported by the instance type. |
|412 |InvalidImageId.KeepImageCredentialMismatch |The specified ImageId and KeepImageCredential do not match. |The specified ImageId and KeepImageCredential do not match. |
|412 |InvalidInstanceChargeType.AffinityGroupSizeMismatch |The specified InstanceChargeType does not match AffinityGroupSize. |The specified billing method does not match the specification required by the affinity group. The billing method of affinity group instances can not be subscription. |
|412 |InvalidInstanceTenancy.DeploymentSetIdMismatch |The specified instance tenancy and deployment set id do not match. |The ECS instance deployed on a dedicated host cannot be added to the deployment set. |
|412 |InvalidInstanceTypeId.DeploymentSetIdMismatch |The specified instance type id and deployment set id do not match. |The specified instance type cannot be added to the deployment set. |
|412 |InvalidIpv6OnlyNetworkInterfaceAndIpv4NetworkInterface.Mismatch |The specified ipv6 only network interface and ipv4 network interface do not match. |IPv6\-only instances do not support IPv4 network interfaces. |
|412 |InvalidKeyPairName.KeepImageCredentialMismatch |The specified KeyPairName and KeepImageCredential do not match. |The specified KeyPairName and KeepImageCredential do not match. |
|412 |InvalidPassword.KeepImageCredentialMismatch |The specified Password and KeepImageCredential do not match. |The specified Password and KeepImageCredential do not match. |
|412 |InvalidReleaseWithInstance.ChargeTypeMismatch |The specified release with instance and charge type do not match. |The specified EIP deletion attribute (the EIP is deleted along with the instance) does not match the billing method. |
|412 |InvalidSecurityGroup.SubnetMismatch |The specified SecurityGroup and Subnet do not match. |The VPC of the security group does not match the VPC of the subnet. |
|412 |InvalidSecurityProtectionInstance.RegionMismatch |The specified security protection instance is not in the specified region. |The specified security protection instance is not in the specified region. |
|412 |InvalidSecurityProtectionInstance.SpecMismatch |The specified security protection instance and EIP are in different specifications. |The specified security protection instance and EIP specification do not match. |
|412 |InvalidSecurityProtectionTypes.BandwidthPackageIdMismatch |The specified security protection types and bandwidth package id do not match. |The specified EIP security protection level does not match the shared bandwidth level. |
|412 |InvalidSnapshotZoneId.Mismatch |The specified ZoneId does not match the snapshot ZoneId. |The specified ZoneId does not match the snapshot ZoneId. |
|412 |InvalidSubnet.ZoneMismatch |The specified subnet and instance are in different Availability Zones. |The availability zone associated with the subnet is different from the one where the instance resides. |
|412 |InvalidSubnetImage.Mismatch |The specified image does not match the specified subnet. |The specified image does not match the specified subnet. |
|412 |InvalidTenancy.DedicatedHostIdMismatch |The specified Tenancy does not match DedicatedHostId. |The specified Tenancy does not match ID of the dedicated host. |
|412 |InvalidTenancy.InstanceTypeIdMismatch |The specified Tenancy does not match InstanceTypeId. |The specified Tenancy does not match the instance type. |
|412 |InvalidVolumeSize.ImageSizeMismatch |The specified system disk size is smaller than the image file size. |The specified system volume capacity is smaller than the image file size. |
|412 |InvalidVolumeType.ImageMismatch |The specified VolumeType and Image do not match. |The specified volume type and image do not match. |
|412 |InvalidVolumeType.InstanceTypeMismatch |The specified VolumeType and InstanceType do not match. |The specified volume type and instance type do not match. |
|412 |InvalidVolumeTypes.Mismatch |Mismatch between attached Volume types. |The types of mounted volumes do not match. |
|412 |NotPaymentQualified |Your account has not passed the payment qualified yet. |The account has no payment authentication. |
|412 |OperationDenied.AccountCountryAreaInvalid |This product is temporarily not available for sale in the country or region where you registered your account. |This product is temporarily not available for sale in the country or region where you registered your account. |
|412 |OperationDenied.AccountDeleted |The specified action is denied because the account has been deleted. |The specified action is denied because the account has been deleted. |
|412 |OperationDenied.AccountTaxNoInvalid |To purchase BytePlus products, you need to provide a Goods and Services Tax (GST) number. |To purchase BytePlus products, you need to provide a Goods and Services Tax (GST) number. |
|412 |OperationDenied.AccountWeakVerified |The specified action is denied because the account failed to pass the weak real\-name authentication. |The specified action is denied because the account failed to pass the weak real\-name authentication. |
|412 |OperationDenied.MainAccountNotSupportPaypal |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |Paypal is not supported for the pay\-as\-you\-go product in this order. Please contact the root user for an alternative payment method. |
|412 |OperationDenied.NotOpeningQualified |The specified action is denied because the account has not completed account authentication. |The specified action is denied because the account has not completed account authentication. |
|412 |OperationDenied.NotSupportPaypal |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |Paypal is not supported for the pay\-as\-you\-go product in this order. Please provide an alternative payment method. |
|412 |OperationDenied.RiskInterception |The specified action is denied. Due to risk interception, this feature is temporarily unavailable. |The specified action is denied. Due to risk interception, this feature is temporarily unavailable. |
|412 |OperationDenied.SpecifiedSecurityGroupNotAuthorized |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |As the specified security group is a service\-managed security group, the user has no permission to perform actions on the specified security group. |
|412 |OperationDenied.TrafficModeNotAuthorized |The specified operation is denied as you are not authorized to use traffic mode. |The specified action was denied because you have no permission to perform actions on the specified network interface. |
|412 |OperationDenied.EnableJumboFrameForceDisabled |The specified operation is denied because Jumbo Frame is force\-disabled for the account. |The specified operation is rejected because JumboFrame is forcibly disabled for the current account. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |You have exceeded the rate limit for resource requests. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The resources are currently insufficient. Try again later or select other instance types. |
|500 |Insufficient.VolumePoolCapacity |There is not enough capacity to fulfill your request. |Insufficient capacity of the current storage pool. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
