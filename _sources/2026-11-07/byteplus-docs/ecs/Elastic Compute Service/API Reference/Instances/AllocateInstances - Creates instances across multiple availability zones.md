---
title: "AllocateInstances - Creates instances across multiple availability zones"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/AllocateInstances"
---

Call the AllocateInstances operation to create one or more instances (with availability zone flexibility).

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

This feature is in Beta. If you need a trial, please contact your account manager.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

We recommend that you use the operation to create instances in the following scenarios:


* **No specific requirements for the availability zone**: You can use the [random availability zone](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) feature to create an instance based on the `ZoneId` parameter. The system will automatically select a main availability zone within the region based on the type of the instance you want to purchase. You do not need to specify an availability zone. This operation also allows you to create an instance in the specified availability zone.

* **Batch deployment of instances across availability zones**: When you create multiple instances, you can configure the `BatchCreateInMultiZone` parameter to deploy instances in different availability zones within the same region. This helps prevent creation failures caused by insufficient resources in a single availability zone.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also call the <a href="https://docs.byteplus.com/en/docs/ecs/RunInstances">RunInstances</a> operation to create instances in a specific availability zone. Compared with RunInstances, this operation offers availability zone flexibility but does not allow you to specify the IP addresses </div>


<div data-tips="true" data-tips-type="tip">(<code>NetworkInterfaces.N.PrimaryIpAddress</code> and <code>NetworkInterfaces.N.PrivateIpAddresses.N</code>) of the network interface, and the minimum number of instances to be created (<code>MinCount</code>).</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|8PIhlG">必选</span> `Sample value: AllocateInstances`

The operation that you want to perform. Valid value: AllocateInstances.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|2sxhV5">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**AutoRenew** <span data-label="purple">boolean</span> `Optional` `Sample value: Boolean`

Whether to automatically renew the instance after it expires. Value:


* true: Enable automatic renewal

* false (default): Disable automatic renewal


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect only when the value of <code>InstanceChargeType</code> is <code>PrePaid</code>.</div>




**AutoRenewPeriod** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The duration for each automatic renewal.


* When `AutoRenew` is set to `True`, this parameter is valid. The default value is 1.

* When `PeriodUnit` is set to `Month`, this parameter takes a value from 1, 2, 3, 6, and 12.



**BatchCreateInMultiZone** <span data-label="purple">boolean</span> `Optional` `Sample value: true`

Whether to support deployment across multiple random availability zones. Valid values:


* true: ECS instances created in a batch are deployed across multiple availability zones.

* false (default): ECS instances created in a batch are deployed in a single availability zone.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This field takes effect when <code>ZoneId</code> is empty.</div>




**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Count** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

Number of instances to be created. Value: 1–100. When 0 is passed in, the default number is 1.



**CreditSpecification** <span data-label="purple">string</span> `Optional` `Sample value: Standard`

The running mode of Burstable instances. Value:


* Standard: the standard mode

* Unlimited: the unlimited performance mode (currently unavailable)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>InstanceTypeId</code> is ecs.t2 instance family (burstable instance).</div>


* <div data-tips="true" data-tips-type="tip">When no parameter is passed or this parameter is empty, the burstable instance defaults to <code>Standard</code> mode.</div>




**DeploymentSetGroupNumber** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

When an ECS instance is to join or adjust to a deployment set with the AvailabilityGroup policy, this parameter can be used to specify the group number of the instance within the deployment set. Valid range of the parameter: 1\-3.



**DeploymentSetId** <span data-label="purple">string</span> `Optional` `Sample value: dps-yc1o9aahks5m57nk****`

The ID of the deployment set that the instance is added to.



**Description** <span data-label="purple">string</span> `Optional` `Sample value: ECS instance for testing.`

Description of the instance. Default value: empty string.


* Start with a letter or Chinese

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.



**DryRun** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Whether to only precheck this request. Value:


* true: Send a check request without instance creation. Check items include whether required parameters are filled, request format, business restrictions, and ECS inventory. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of <code>DryRun</code> is <code>true</code>, if the <code>Count</code> parameter is specified, its value must be 1.</div>



* false (default): Send a normal request and directly create an instance after the check passes.



**EipAddress.BandwidthMbps** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The maximum bandwidth for the EIP, in Mbps. Default value is 1.


* Pass `PayByBandwidth` in `ChargeType`. Valid range: 1–500.

* Pass `PayByTraffic` in `ChargeType`. Valid range: 1–200.



**EipAddress.BandwidthPackageId** <span data-label="purple">string</span> `Optional` `Sample value: bwp-2zeo05qre24nhrqpy****`

ID of the shared bandwidth package. This means you add the EIP to the specified shared bandwidth package.


* You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) operation to query the ID of shared bandwidth package.

* To add an EIP to a shared bandwidth package, the following conditions must be met:

   * The EIP and bandwidth package must be of the same security mode.

   * The EIP and bandwidth package belong to the same region.

   * The billing method of the EIP must be "Pay\-as\-you\-go".

   * Shared bandwidth package is of the IPv4 type.



**EipAddress.ChargeType** <span data-label="purple">string</span> `Optional` `Sample value: PayByBandwidth`

Billing method of the EIP. Value:


* PayByBandwidth (default): Pay\-by\-bandwidth

* PayByTraffic: Pay\-by\-data\-transfer

* PrePaid: subscription


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the billing method <code>InstanceChargeType</code> of the instance is <code>PostPaid</code>, this parameter cannot be set to <code>PrePaid</code>.</div>




**EipAddress.ISP** <span data-label="purple">string</span> `Optional` `Sample value: BGP`

The ISP for EIP, which by default is BGP. Value:


* BGP: BGP (Multi\-ISP).

* If your account has applied for and enabled permission for the static single\-ISP, you can pass in the following values:

   * ChinaMobile: China Mobile static single\-ISP.

   * ChinaTelecom: China Telecom static single\-ISP.

   * ChinaUnicom: China Unicom static single\-ISP.

* If your account has applied for and enabled permission for the BGP single\-ISP, you can pass in SingleLine_BGP.

* If your account has applied for and enabled static BGP permission, you can pass in Static_BGP.



**EipAddress.ReleaseWithInstance** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Whether the EIP is deleted along with the instance. This feature is only available for pay\-as\-you\-go EIPs. Value:


* true: The EIP is deleted along with the instance. When an instance is automatically reclaimed by the system (for example, 24 hours after unsubscription or upon expiration) or deleted via the [DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) or [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API, the EIP is released along with the instance.

* false (default): The EIP is not deleted along with the instance.



**EipAddress.SecurityProtectionInstanceId** <span data-label="purple">integer</span> `Optional` `Sample value: 20`

ID of the Anti\-DDoS Origin (Enterprise Edition).

When `SecurityProtectionTypes` is set to `AntiDDoS_Enhanced`, this parameter must be passed in.



**EipAddress.SecurityProtectionTypes.N** <span data-label="purple">string[]</span> `Optional` `Sample value: SecurityProtectionTypes.1=AntiDDoS_Enhanced`

The security protection type of EIP.


* N specifies the serial number of the protection type. Currently, only 1 is supported.

* Valid values:

   * AntiDDoS_Enhanced: Apply for EIP with enhanced protection type. Then the instance can be secured with Anti\-DDoS Origin (Enterprise Edition).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If <code>EipAddress.SecurityProtectionTypes.N</code> is set to <code>AntiDDoS_Enhanced</code>, <code>EipAddress.ChargeType</code> cannot be <code>PrePaid</code> and <code>EipAddress.ISP</code> must be set to <code>BGP</code>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">EIPs with enhanced protection type are currently in Beta. If you need a trial, please contact your account manager.      </div>
      

   * If this parameter is not passed in, the system applies for an EIP of the default protection type.



**Hostname** <span data-label="purple">string</span> `Optional` `Sample value: instance-host-name`

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




**HpcClusterId** <span data-label="purple">string</span> `Optional` `Sample value: hpcCluster-l8u24ovdmoab6opf****`

ID of the HPC cluster to which the instance belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect and is required only for the creation of HPC\-optimized instances.</div>




**ImageId** <span data-label="purple">string</span> <span data-api-tag="require|aSSbrt">必选</span> `Sample value: image-3tefr6wgx63vj0x1****`

ID of the image used for instance startup

You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation and pass the desired instance type in the `InstanceType` parameter to query images that support this type and their ID information.



**ImageReleaseVersion** <span data-label="purple">string</span> `Optional` `Sample value: 20241115`

The specific version number of the image used.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter only takes effect when the used image is a public image.</div>


* <div data-tips="true" data-tips-type="tip">If this parameter is empty, the latest version of the image is used.</div>




**InstallRunCommandAgent** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Whether to install cloud assistant Agent on startup during instance creation. Value:


* true: Install during creation.

* false (default): Do not install during creation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about Cloud assistant, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant">Cloud assistant overview</a>.</div>




**InstanceChargeType** <span data-label="purple">string</span> `Optional` `example value: PostPaid`

The billing methods for instance and volume. Value:


* PostPaid: Pay\-as\-you\-go

* PrePaid: Subscription. Please make sure that your account supports balance payment or credit control payment. Otherwise, an error message "InvalidInstanceChargeType" is returned.



**InstanceName** <span data-label="purple">string</span> <span data-api-tag="require|dsHjP9">必选</span> `Sample value: instance-test`

The instance name.


* Start with a letter or Chinese.

* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If <code>SuffixIndex</code> is set for the instance, the instance name length includes the suffix.</div>


* <div data-tips="true" data-tips-type="tip">When creating instances in a batch, you can set sequential instance names in the <code>name_prefix[begin_number,bits]name_suffix</code> format. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames">Configuring sequential instance names or hostnames in a batch</a>.</div>




**InstanceTypeId** <span data-label="purple">string</span> <span data-api-tag="require|itKtgD">必选</span> `Sample value: ecs.g1ie.xlarge`

Instance type:


* Instance type selection: You can refer to the [ECS instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types) or call the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) operation to view the performance data of instance types. You can also refer to [Best practices for instance type selection](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice) for selection guide.

* Inventory query: You can call the [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) operation to query the inventory information of computing resources in the availability zone.



**KeepImageCredential** <span data-label="purple">boolean</span> `Optional` `Sample value: true`

Whether to keep image settings. Value:


* true: Keeps image settings. This allows you to use the password or key pair specified for the image to log in to the ECS instance.

* false (default): Does not keep image settings.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only custom images and shared images support this feature.</div>


* <div data-tips="true" data-tips-type="tip">When the value of this parameter is <code>true</code>, do not pass in <code>Password</code> and <code>KeyPairName</code>.</div>




**KeyPairName** <span data-label="purple">string</span> `Optional` `Sample value: kp-test-123`

If you need to use the "SSH Key" to log in to the instance, specify the name of an already created key pair.

You can call the [DescribeKeyPairs](https://docs.byteplus.com/en/docs/ecs/DescribeKeyPairs) operation to view existing key pairs. If no key pair is available, call the [CreateKeyPair](https://docs.byteplus.com/en/docs/ecs/CreateKeyPair) operation to create a new one.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Windows instances do not support the SSH Key method. Even if this parameter is passed in, only the parameter <code>Password</code> takes effect.</div>


* <div data-tips="true" data-tips-type="tip">Linux instances support login with both password and key pair. If both <code>KeyPairName</code> and <code>Password</code> are set, only the key pair <code>KeyPairName</code> takes effect when you call this operation.</div>




**NetworkInterfaces.N.SecurityGroupIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|riJx9s">必选</span> `Sample value: NetworkInterfaces.1.SecurityGroupIds.1=sg-3ti78x9h8t4bw*****& NetworkInterfaces.2.SecurityGroupIds.1=sg-3cj59ih2v9hj46c6rr******`

ID of the security group associated with the network interface.


* The first N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* The second N: indicates the serial number of the security group associated with the network interface. Value: 1–5.

* Separate multiple security group IDs with ampersands (&).



**NetworkInterfaces.N.SubnetId.N** <span data-label="purple">string[]</span> <span data-api-tag="require|57bv4x">必选</span> `Sample value: NetworkInterfaces.1.SubnetId.1=subnet-3tispp1nai4e8i******& NetworkInterfaces.1.SubnetId.2=subnet-3tispp1nai4e8i******&NetworkInterfaces.2.SubnetId.1=subnet-3tispp1nai4e8i******&NetworkInterfaces.2.SubnetId.2=subnet-3tispp1nai4e8i******`

The list of private network subnet IDs of the instance.


* The first N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface.

* The second N: indicates the list of private network subnets corresponding to the network interface.

* Separate multiple VPC subnet IDs with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you pass in a list of private network subnet IDs from multiple availability zones, the system will select and associate the subnet that matches the availability zone recommended by the random availability zone feature.</div>




**NetworkInterfaces.N.Ipv6AddressCount** <span data-label="purple">integer[]</span> `Optional` `Sample value: NetworkInterfaces.1.Ipv6AddressCount=1`

The number of private IPv6 addresses assigned to the primary network interface, which can only be 1.


* If this parameter is passed in, the system automatically allocates the corresponding number of idle private IPv6 addresses from the subnet that the network interface belongs to. Then the system assigns idle private IPv6 addresses as the private IPv6 addresses of the network interface.

* When you create an instance, you can assign IPv6 address to the primary network interface only. To assign an IPv6 address to a secondary network interface, refer to [CreateNetworkInterface](https://docs.byteplus.com/en/docs/vpc/CreateNetworkInterface).

* Argument \- N: indicates the serial number of the network interface. N = 1 indicates the primary network interface, and N ≥ 2 indicates the secondary network interface. Therefore, when N ≥ 2 is passed in, this parameter is ignored.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The feature of assigning IPv6 addresses to the network interface is currently in Beta. If you need a trial, please contact your account manager.</div>




**Password** <span data-label="purple">string</span> `Optional` `Sample value: password@123`

If you need to log in to an instance with "Password", specify the initial login password of the administrator account through this parameter. The Linux administrator account is root, and the Windows administrator account is Administrator.

Password complexity requirements are as follows:


* The length limit is 8 to 30 characters.

* Passwords can only consist of uppercase letters, lowercase letters, numbers, and special characters, and must include at least three of these elements.

* Valid special characters: `~!@#$%^&\*()_\-+=|{}[]:;'<\>,.?/

* The password cannot start with "/" or "$6$".


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For login credentials, "Password", "Key Pair", and "Keep image settings" are available. If you choose to use a password, specify a complex password to improve security.</div>




**Period** <span data-label="purple">integer</span> `Optional` `Sample value: 12`

The purchase duration of resources (unit: month).


* Value: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, 60

* Default value: 1


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect and is required only when the value of <code>InstanceChargeType</code> is <code>PrePaid</code>.</div>




**PeriodUnit** <span data-label="purple">string</span> `Optional` `Sample value: Month`

The unit of purchase duration of resources. Value: Month (default).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect and is required only when the value of <code>InstanceChargeType</code> is <code>PrePaid</code>.</div>




**Placement.Affinity** <span data-label="purple">string</span> `Optional` `Sample value: Default`

For ECS instances in economical mode, some resources are released after instances are stopped. You can use this parameter to select whether the instances are still deployed on the original host when restarted. Value:


* Host: When instances in economical mode are restarted, they are still deployed on the original host.

* Default: When instances in economical mode enabled are restarted, they are first migrated to hosts that support automatic deployment. If hosts supporting automatic deployment do not have enough resources, the instances are started on the original host.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: project_a`

The associated project. Each instance can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**SecurityEnhancementStrategy** <span data-label="purple">string</span> `Optional` `Sample value: Active`

Whether to enable security enhancement. Value:


* Active: Enable security enhancement. This feature is effective for public images only.

* InActive: Disables security enhancement. This feature is effective for all image types.



**SpotPriceLimit** <span data-label="purple">float</span> `Optional` `Sample value: 0.78`

The maximum hourly price for spot instances. A maximum of three decimal places for the price is supported.

This parameter takes effect only when `SpotStrategy` is set to `SpotWithPriceLimit`.



**SpotStrategy** <span data-label="purple">string</span> `Optional` `Sample value: NoSpot`

Spot strategy for instance billed in pay\-as\-you\-go mode. Value:


* NoSpot (default): Instances are billed in pay\-as\-you\-go mode.

* SpotAsPriceGo: The system automatically bids based on the current market price for the spot instance.

* SpotWithPriceLimit: spot instance with a price limit.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>InstanceChargeType</code> is set to <code>PostPaid</code>, this parameter takes effect.</div>


* <div data-tips="true" data-tips-type="tip">For details on bidding patterns of spot instances, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance">Purchasing spot instances</a>.</div>




**SuffixIndex** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The starting number of the sequential suffix, with the value from 1 to 999. Default value: 1



**Tags.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the user tag.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple keys with ampersands (&).


Naming rules:


* It cannot start with `volc:` or `sys:` in any case form.

* Only language characters, numbers, space, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the user tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple key values with ampersands (&).


Naming rules:


* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 0 to 256 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to pass in this parameter, first provide the <code>Tags.N.Key</code> parameter.</div>




**UniqueSuffix** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Specify whether to add sequential suffixes to `Hostname` and `InstanceName` when you create multiple instances.


* true: Enable sequential suffix.

* false (default): Disable sequential suffix.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you enable the sequential suffix and <code>Hostname</code> is empty, the system automatically generates hostnames without a sequential suffix.</div>


* <div data-tips="true" data-tips-type="tip">If you enable the sequential suffix and specify the naming format <code>[begin_number,bits]</code> for <code>Hostname</code> and <code>InstanceName</code>, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Batch-configuring-sequential-instance-names-or-hostnames">Setting sequential instance or host names in a batch</a> for the final naming effect.</div>




**UserData** <span data-label="purple">string</span> `Optional` `Sample value: ZWNobyBoZWxsbyBlY3Mh`

Instance custom data. The custom data for an instance must be encoded in Base64 format, and the data cannot exceed 16KB before Base64 encoding.

If left blank, the parameter defaults to an empty value.



**Volumes.N.Size** <span data-label="purple">integer[]</span> <span data-api-tag="require|8QTuVf">必选</span> `Sample value: Volumes.1.Size=100&Volumes.2.Size=100`

The volume capacity. Unit: GiB. The valid range of N is 1–16. N = 1 indicates the system volume, and N ≥ 2 indicates the data volume. Separate multiple volumes with ampersands (&).

Valid range of volume capacity.


* System volume:

* ESSD_PL0: 20～2048

* ESSD_FlexPL: 20～2048


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Default value: max{40, the capacity of the image corresponding to ImageId}.</div>



* Data volume:

* ESSD_PL0: 10～32768

* ESSD_FlexPL: 10\-32768


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is not passed in, the data volume capacity is based on the snapshot size corresponding to <code>Volumes.N.SnapshotId</code>. If <code>Volumes.N.SnapshotId</code> is not passed in, the system returns the error LimitExceeded.DataVolumeSize.</div>




**Volumes.N.ExtraPerformanceIOPS** <span data-label="purple">integer[]</span> `Optional` `Sample value: Volumes.2.ExtraPerformanceIOPS = 100`

The capacity of additional IOPS performance (unit:ops/sec, operations per second) for the volume. Only ESSD FlexPL data volumes support additional IOPS performance.

When `ExtraPerformanceTypeId` is set to `Balance` or `IOPS`, configure this parameter. The value ranges for each type of extra performance are as follows:


* IOPS: 1–50000

* Balance: 1–50000


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Parameter \- N: This specifies the number of the volume. Valid value: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Volumes.N.ExtraPerformanceThroughputMB** <span data-label="purple">integer[]</span> `Optional` `Sample value: Volumes.2.ExtraPerformanceThroughputMB=100`

The capacity of additional throughput performance (unit: MB/s) for the volume. Only ESSD FlexPL data volumes support additional throughput performance.

When `ExtraPerformanceTypeId` is set to `Throughput`, configure this parameter.

Valid range: 1–650.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Volumes.N.ExtraPerformanceTypeId** <span data-label="purple">string[]</span> `Optional` `Sample value: Volumes.2.ExtraPerformanceTypeId=IOPS`

The type of additional performance for the volume. This feature is only supported by ESSD FlexPL data volumes. Valid range:


* Balance: balanced additional performance.

* IOPS: IOPS additional performance.

* Throughput: throughput additional performance.


For more information about additional performance, please refer to [Volume additional performance](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**Volumes.N.SnapshotId** <span data-label="purple">string[]</span> `Optional` `Sample value: Volumes.1.SnapshotId=snap-31akybwsxi8rudc6****&Volumes.2.SnapshotId=snap-31ak39j5bh8rubsn****`

Only data volumes can be created with a snapshot. You can call the [DescribeSnapshots](https://docs.byteplus.com/en/docs/ecs/Describesnapshots) operation to query the snapshot ID.


* Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume. Therefore, you can pass in the snapshot ID for the target data volume.

* Multiple volumes are separated with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only ESSD supports volume creation using snapshots. PTSSD does not support snapshot\-related features.</div>


* <div data-tips="true" data-tips-type="tip">Only snapshots in "Available" status support new volume creation. Snapshots in statuses "Creating", "Rolling Back", "Deleting", and "Error" do not support new volume creation.</div>




**Volumes.N.VolumeType** <span data-label="purple">string[]</span> `Optional` `Sample value: Volumes.1.VolumeType=ESSD_PL0&Volumes.2.VolumeType=ESSD_PL0`

The volume type. Value:


* ESSD_PL0 (default): ESSD PL0

* ESSD_FlexPL: ESSD FlexPL


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume, and N ≥ 2 indicates the data volume.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OperationDetails** <span data-label="purple">object[]</span> `Sample value: --`

The operation details.


**Error** <span data-label="purple">object</span> `Sample value: --`

The error message for the instance being operated on.


**Code** <span data-label="purple">string</span> `Sample value: InvalidArgument`

The error code for the failure of a specific individual request during batch operations. For information about the value, see [Error message for the failure of a specific individual request during batch operations](https://docs.byteplus.com/en/docs/ecs/Error_information_for_specific_individual_request_failures_during_batch_operations).



**Message** <span data-label="purple">string</span> `Sample value: The specified argument is invalid.`

The error information for the failure of a specific individual request during batch operations. For information about the value, see [Error message for the failure of a specific individual request during batch operations](https://docs.byteplus.com/en/docs/ecs/Error_information_for_specific_individual_request_failures_during_batch_operations).




**InstanceIds** <span data-label="purple">string[]</span> `Sample value: ["i-3tigy72q3u3vj0x2****","i-3tigy72q3u3vj0x2****"]`

Instance ID.



**PreorderIds** <span data-label="purple">string[]</span> `Sample value: ["Order7021038849342******"]`

The order number.



**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=AllocateInstances&Version=2020-04-01&ImageId=image-3tefr6wgx63vj0******&InstanceTypeId=ecs.g1ie.xlarge&InstanceName=instance-test&Count=1&Password=password@123&NetworkInterfaces.1.SubnetId.1=subnet-3tispp1nai4e8i******&NetworkInterfaces.1.SecurityGroupIds.1=sg-3ti78x9h8t4bw*****&Volumes.1.Size=40&EipAddress.BandwidthMbps=5 HTTP/1.1
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
        "Action": "AllocateInstances",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OperationDetails": [
            {
                "InstanceId": "i-ybo349sxoncm9t******",
                "PreorderIds": "Order7021038849342******",
                "ZoneId": "cn-beijing-a"
             }
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
|400 |InvalidCount.Malformed |The specified count is malformed. |The specified parameter Count is invalid. |
|400 |InvalidCreditSpecification.Malformed |The specified credit specification is malformed. |The specified mode of the burstable instance is invalid. |
|400 |InvalidDedicatedHostStatus.Unsupported |The status of the specified dedicated host does not support this request. |The dedicated host in current status does not support this action. |
|400 |InvalidDeploymentSetGroupNumber |The specified DeploymentSetGroupNumber is invalid. |The specified deployment set group is invalid. |
|400 |InvalidEipAddressChargeType.Malformed |The specified ChargeType of elastic IP is malformed. |The specified billing method of EIP is invalid. |
|400 |InvalidExtraPerformanceTypeId.Malformed |The specified ExtraPerformanceTypeId is malformed. |The specified type of additional performance package is invalid. |
|400 |InvalidHostname.Malformed |The specified Hostname is malformed. |The specified hostname is invalid. |
|400 |InvalidImageForConfidentialComputing.UnSupported |The specified image not support confidential computing. |The specified image does not support confidential computing. |
|400 |InvalidInstanceChargeType |The specified InstanceChargeType is invalid. |The specified instance billing method is invalid. |
|400 |InvalidInstanceDescription.Malformed |The specified InstanceDescription is malformed. |The specified instance description is not valid. |
|400 |InvalidInstanceName.Malformed |The specified InstanceName is malformed. |The specified instance name is invalid. |
|400 |InvalidInstanceType.ImageMismatch |The specified InstanceType and Image do not match. |The specified instance type and image do not match. |
|400 |InvalidInstanceTypeForConfidentialComputing.NotSupported |The specified instance type not support confidential computing. |The specified instance type does not support confidential computing. |
|400 |InvalidInstanceTypeForCreateSpotInstance.Unsupported |The specified InstanceType does not support creation of spot instances. |The specified instance type does not support the creation of spot instances. |
|400 |InvalidIpv6AddressCount.Malformed |The specified Ipv6AddressCount is malformed. |The specified number of IPv6 addresses is invalid. |
|400 |InvalidIpv6OnlySubnet.Unsupported |The specified ipv6 only subnet is unsupported. |Currently, you cannot create an instance associated with the IPv6\-only subnet. |
|400 |InvalidKeyPairForWindows.Unsupported |The OSType of this specified instance is Windows, which does not support key pairs. |The specified instance is based on the Windows operating system and does not support key pairs. |
|400 |InvalidMinCount.Malformed |The specified MinCount is malformed. |The specified minimum purchase quantity for the instance is invalid. |
|400 |InvalidNetworkInterfaceType |The type of specified elastic network interface is illegal for the request. |The specified type of elastic network interface can not respond to this request. |
|400 |InvalidParameterCombination |Indicates an incorrect combination of parameters. |The parameter combination is incorrect, or a parameter is missing. |
|400 |InvalidPassword.Malformed |The specified password is malformed. |The specified password format is invalid. |
|400 |InvalidPeriod |The specified period is not valid. |The specified number of billing cycles is invalid. |
|400 |InvalidPeriodUnit |The specified PeriodUnit is not valid, is unsupported, or cannot be used. |The specified billing cycle is invalid. |
|400 |InvalidPlacementAffinity.Malformed |The specified placement affinity is malformed. |The specified Placement.Affinity is invalid. |
|400 |InvalidPlacementTenancy.Malformed |The specified placement tenancy is malformed. |The specified Placement.Tenancy is invalid. |
|400 |InvalidProjectName |The specified ProjectName is invalid. |The specified project name is invalid. |
|400 |InvalidSecurityEnhancementStrategy.Malformed |The specified SecurityEnhancementStrategy is malformed. |The specified security enhancement policy is invalid. |
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
|400 |InvalidUserData.Malformed |The specified UserData is malformed. |The specified UserData is invalid. |
|400 |InvalidVolumeReleaseType.Malformed |The specified VolumeReleaseType is malformed. |The specified type of volume release is invalid. |
|400 |InvalidVolumeSizeForExtraPerformance.Unsupported |The specified VolumeSize does not support extra performance. |The specified volume capacity does not support purchase of additional performance. |
|400 |InvalidVolumeType.Malformed |The specified VolumeType is malformed. |The specified volume type is invalid. |
|400 |InvalidVolumeTypeForExtraPerformance.Unsupported |The specified VolumeType does not support extra performance. |The specified volume type does not support purchase of additional performance. |
|400 |InvalidVolumeTypeForSnapshot.UnSupported |The specified VolumeType cannot be used for create snapshot. |The specified volume type does not support the image feature. |
|400 |LimitExceeded.DataVolumeSize |The specified data volume size exceeds the limit. |The specified data volume size (GiB) exceeds the limit. |
|400 |LimitExceeded.ExtraPerformanceThroughput |You've reached the limit on the number of ExtraPerformanceThroughput that you can set. |The throughput has reached the maximum limit. No additional performance required. |
|400 |LimitExceeded.MaximumDeploymentSetInstances |You've reached the limit on the number of instances that can be added to the deployment set. |The number of instances in the specified deployment set exceeds the maximum limit. |
|400 |LimitExceeded.MaximumEipBandwidth |The specified elastic IP bandwidth value exceeds the maximum limit. |The specified EIP bandwidth value exceeds the maximum limit. |
|400 |LimitExceeded.MaximumExtraPerformanceIOPS |The number of specified ExtraPerformanceIOPS exceeds the maximum limit. |The specified additional performance IOPS exceeds the maximum limit. |
|400 |LimitExceeded.MaximumExtraPerformanceThroughputMB |The number of specified ExtraPerformanceThroughputMB exceeds the maximum limit. |The specified additional performance throughput exceeds the maximum limit. |
|400 |LimitExceeded.MaximumHighPerformanceNetworkInterfaces |You've reached the limit on the number of HighPerformance NetworkInterfaces that can be attached to the instance. |The number of network interfaces in RDMA communication mode associated with the specified instance exceeds the maximum limit. |
|400 |LimitExceeded.MaximumNetworkInterfaces |You've reached the limit on the number of NetworkInterfaces that can be attached to the instance. |The specified number of network interfaces associated with the instance exceeds the maximum limit. |
|400 |LimitExceeded.MaximumSecurityProtectionTypes |You've reached the limit on the number of SecurityProtectionTypes that you can set. |The specified number of SecurityProtectionTypes exceeds the maximum limit. |
|400 |LimitExceeded.MaximumSubnetIps |The number of specified subnet IP addresses exceeds the maximum limit. |The specified number of subnet IP addresses reaches the maximum limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |LimitExceeded.MaximumVolumes |You've reached the limit on the number of volumes that can be attached to the instance. |The specified number of volumes mounted to the instance exceeds the maximum limit. |
|400 |LimitExceeded.MinimumEipBandwidth |The specified elastic IP bandwidth value exceeds the minimum limit. |The bandwidth value of the specified EIP exceeds the minimum limit. |
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
|400 |OperationDenied.PurchaseLimited |You are not authorized to purchase ecs. |Permission to purchase an ECS instance is not granted. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the number of instances that you can create, please submit ticket to request an increase in quota. |The number of bandwidth packages you can create reaches the limit. Please submit a ticket to increase the quota. |
|400 |QuotaExceeded.MaximumEips |You've reached the limit on the number of EIP that you can create, please submit ticket to request an increase in quota. |Insufficient EIP quota. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumGeneralCpus |You've reached the limit on the number of general instances CPU that you can create, please submit ticket or sign\-on to the Console to request an increase in [general_vcpu] quota. |The CPU quota of the General\-purpose instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumGpuBasicNums |You've reached the limit on the GPU number of GPU\-accelerated instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_basic] quota. |The GPU card quota for GPU Accelerated instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumHighPerformanceGpus |You've reached the limit on the GPU number of High Performance Computing GPU instances that you can create, please submit ticket or sign\-on to the Console to request an increase in [gpu_high_performance] quota. |The GPU card quota for HPC\-optimized instances is insufficient. Please submit a ticket or go to the console to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceCpus |You've reached the limit on the number of instance CPU that you can create, please submit ticket to request an increase in quota. |The quota of instance CPU number is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumInstanceTypeInstances |You've reached the limit on the number of instance type instances that you can create, please submit ticket to request an increase in quota. |The quota of the number of the specified instance type that you can create is insufficient. Please submit a ticket to request a quota increase. |
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
|403 |RequestForbidden |Request is forbidden by the server. |Your ECS services are suspended because your BytePlus account has violated relevant regulations. To restore the services, please submit a ticket for processing assistance from the service team. |
|404 |InvalidBandwidthPackage.NotFound |The specified BandwidthPackage does not exist. |The specified shared bandwidth package does not exist. |
|404 |InvalidDedicatedHost.NotFound |The specified dedicated host does not exist. |The specified dedicated host does not exist. |
|404 |InvalidDedicatedHostCluster.NotFound |The specified dedicated host cluster does not exist. |The specified dedicated host cluster does not exist. |
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
|409 |InvalidNetworkInterfacesVpc.Conflict |Multiple vpcs are not supported for instances in the same HpcCluster |RDMA instances in the same high\-performance cluster cannot be associated with multiple VPCs. |
|409 |InvalidPrimaryIpAddress.Conflict |The specified PrimaryIpAddress already exists. |The specified PrimaryIpAddress already exists. |
|409 |InvalidPrivateIpAddresses.Conflict |The specified PrivateIpAddresses already exists. |The specified PrivateIpAddresses already exists. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |DryRunOperation |Your request has been validated by the DryRunOperation. |Your request has been validated by "DryRun". |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |Insufficient.AclCapacity |You've reached the limit number of ACLs on the switch. |The number of ACLs on the switch exceeds the limit. |
|412 |InvalidCreditSpecification.InstanceTypeIdMismatch |The specified credit specification and instance type id do not match. |The specified mode of the burstable instance does not match the instance type. |
|412 |InvalidDedicatedHost.InstanceTypeIdMismatch |The specified DedicatedHostId does not match InstanceTypeId. |The ID of the specified dedicated host does not match the instance type. |
|412 |InvalidDedicatedHostCluster.InstanceTypeIdMismatch |The specified DedicatedHostClusterId does not match InstanceTypeId. |The dedicated host cluster with the specified ID does not match the instance type. |
|412 |InvalidDedicatedHostClusterId.DedicatedHostIdMismatch |The specified DedicatedHostClusterId does not match DedicatedHostId. |The specified dedicated host cluster does not match the dedicated host. |
|412 |InvalidHpcCluster.InstanceTypeIdMismatch |The specified HpcClusterId does not match InstanceTypeId. |The HPC cluster does not match the instance type. |
|412 |InvalidHpcCluster.VpcMismatch |The specified Vpc and the Vpc of HpcCluster do not match. |The VPC does not match. The specified VPC and the VPC of HPC Cluster do not match. |
|412 |InvalidHpcCluster.ZoneMismatch |The specified HpcCluster and Instance's ZoneId do not match. |The HPC cluster is not within the scope of the instance availability zone. |
|412 |InvalidISP.BandwidthPackageMismatch |The specified ISP of EIP and bandwidth package do not match. |The specified ISP for the EIP and bandwidth package does not match. |
|412 |InvalidImage.InstanceTypeMismatch |The specified image and instance type do not match. |The specified image does not support the specified instance type. |
|412 |InvalidImageArchitecture.InstanceTypeArchitectureMismatch |The specified image architecture and instance type architecture do not match. |The architecture type of the image is not supported by the instance type. |
|412 |InvalidImageId.KeepImageCredentialMismatch |The specified ImageId and KeepImageCredential do not match. |The specified ImageId and KeepImageCredential do not match. |
|412 |InvalidInstanceTenancy.DeploymentSetIdMismatch |The specified instance tenancy and deployment set id do not match. |The ECS instance deployed on a dedicated host cannot be added to the deployment set. |
|412 |InvalidInstanceTypeId.DeploymentSetIdMismatch |The specified instance type id and deployment set id do not match. |The specified instance type cannot be added to the deployment set. |
|412 |InvalidIpv6OnlyNetworkInterfaceAndIpv4NetworkInterface.Mismatch |The specified ipv6 only network interface and ipv4 network interface do not match. |IPv6\-only instances do not support IPv4 network interfaces. |
|412 |InvalidKeyPairName.KeepImageCredentialMismatch |The specified KeyPairName and KeepImageCredential do not match. |The specified KeyPairName and KeepImageCredential do not match. |
|412 |InvalidPassword.KeepImageCredentialMismatch |The specified Password and KeepImageCredential do not match. |The specified Password and KeepImageCredential do not match. |
|412 |InvalidReleaseWithInstance.ChargeTypeMismatch |The specified release with instance and charge type do not match. |The specified EIP deletion attribute (the EIP is deleted along with the instance) does not match the billing method. |
|412 |InvalidSecurityGroup.SubnetMismatch |The specified SecurityGroup and Subnet do not match. |The VPC of the security group does not match the VPC of the subnet. |
|412 |InvalidSecurityProtectionInstance.RegionMismatch |The specified security protection instance is not in the specified region. |The specified security protection instance is not in the specified region. |
|412 |InvalidSecurityProtectionInstance.SpecMismatch |The specified security protection instance and eip are in different specifications. |The specified security protection instance and EIP specification do not match. |
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
|412 |OperationDenied.SpecifiedSecurityGroupNotAuthorized |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |As the specified security group is a service\-managed security group, the user has no permission to perform actions on the specified security group. |
|412 |OperationDenied.TrafficModeNotAuthorized |The specified operation is denied as you are not authorized to use traffic mode. |The specified operation is rejected because your resource has been locked by another operation. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |Request rate of resources exceeds the limit. |
|500 |Insufficient.InstanceCapacity |There is not enough capacity to fulfill your request. |The capacity resources are currently insufficient. Please try again later or select other instance types. |
|500 |Insufficient.VolumePoolCapacity |There is not enough capacity to fulfill your request. |Insufficient capacity of the current storage pool. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
