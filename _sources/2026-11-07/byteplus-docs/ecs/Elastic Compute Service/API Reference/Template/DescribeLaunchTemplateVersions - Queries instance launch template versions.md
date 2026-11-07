---
title: "DescribeLaunchTemplateVersions - Queries instance launch template versions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplateVersions"
---

Call the DescribeLaunchTemplateVersions operation to query instance launch template versions.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeLaunchTemplateVersions&groupName=%E5%90%AF%E5%8A%A8%E6%A8%A1%E7%89%88&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|lOLXYJ">必选</span> `Sample value: DescribeLaunchTemplateVersions`

The action that you want to perform. Value: DescribeLaunchTemplateVersions.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|tmANYV">必选</span> ` Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**LaunchTemplateId ** <span data-label="purple">string </span>`Optional` `Sample value: lt-ysxc16auaugh9zfy****`

The ID of the instance launch template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to specify the template.</div>




**LaunchTemplateName ** <span data-label="purple">string </span>`Optional` `Sample value: test`

The name of the instance launch template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You are required to specify LaunchTemplateId or LaunchTemplateName to specify the template.</div>




**DefaultVersion ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Indicates whether to query the default version. Valid values:


* true (default): Queries the default version.

* false: Does not query the default version.



**NextToken ** <span data-label="purple">string </span>`Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the NextToken parameter to the value returned by the previous API call.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries per page.


* Maximum value: 100

* Default value: 10



**LaunchTemplateVersions.N ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 1`

The version of the instance launch template. Up to 30 versions are supported.


* Argument \- N: specifies the serial number of the instance launch template.

* Separate multiple versions with &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken ** <span data-label="purple">string </span>`Sample value: --`

The pagination token returned by this call. If this value is empty, the current page is the last page.





**LaunchTemplateVersions ** <span data-label="purple">object[] </span>`Sample value:`

The information of the instance launch template that meets the condition.


**LaunchTemplateId ** <span data-label="purple">string </span>`Sample value: lt-ysxc16auaugh9zfy****`

The ID of the instance launch template.



**VersionDescription ** <span data-label="purple">string </span>`Sample value: test`

The template version description.



**LaunchTemplateVersionData ** <span data-label="purple">object </span>`Sample value: --`

The template configuration information.


**InstanceTypeId ** <span data-label="purple">string </span>`Sample value: ecs.g1.large`

The instance type.



**KeyPairName ** <span data-label="purple">string </span>`Sample value: kp-test-123`

The key pair associated with the instance.



**UserData ** <span data-label="purple">string </span>`Sample value: ZWNobyBoZWxsbyBlY3Mh`

The custom data of the instance.



**InstanceName ** <span data-label="purple">string </span>`Sample value: instance-test`

The instance name.



**Description ** <span data-label="purple">string </span>`Sample value: ECS`

Instance description.



**HostName ** <span data-label="purple">string </span>`Sample value: instance-host-name`

Instance hostname.



**ZoneId ** <span data-label="purple">string </span>`Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-3thbinq64t4bwbha****`

VPC ID.



**HpcClusterId ** <span data-label="purple">string </span>`Sample value: hpcCluster-l8u24ovdmoab6opf****`

The HPC cluster ID.



**InstanceChargeType ** <span data-label="purple">string </span>`Sample value: PostPaid`

The billing method of the instance and volume. Value:


* PostPaid: Pay\-as\-you\-go.

* PrePaid: Subscription.



**SuffixIndex ** <span data-label="purple">integer </span>`Sample value: 1`

The starting number of sequential suffixes.



**UniqueSuffix ** <span data-label="purple">boolean </span>`Sample value: false`

Whether to enable the sequential suffix feature. Valid values:


* true: Enables the sequential suffix feature.

* false: Disables the sequential suffix feature.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The project to which the instance belongs.



**SpotStrategy ** <span data-label="purple">string </span>`Sample value: NoSpot`

The spot strategy for the pay\-as\-you\-go instance. Value:


* NoSpot: Instances are billed in pay\-as\-you\-go mode.

* SpotAsPriceGo: The system automatically bids based on the current market price for the spot instance.

* SpotWithPriceLimit: spot instance with a price limit.



**SpotPriceLimit ** <span data-label="purple">float </span>`Sample value: 0.78`

The maximum hourly price of the spot instance.



**ImageId ** <span data-label="purple">string </span>`Sample value: image-ybmhzqo8u4l8j1ii****`

The image ID.



**SecurityEnhancementStrategy ** <span data-label="purple">string </span>`Sample value: Active`

Whether to enable security enhancement. Value:


* Active: Enables security enhancement. This feature is effective for public images only.

* InActive: Disables security enhancement. This feature is effective for all images.



**Volumes ** <span data-label="purple">object[]</span>

The information about the volume associated with the instance.


**VolumeType ** <span data-label="purple">string </span>`Sample value: ESSD_PL0`

The volume type. Value:


* ESSD_PL0: ESSD PL0.

* PTSSD: PTSSD.



**Size ** <span data-label="purple">integer </span>`Sample value: 100`

The volume capacity. Unit: GiB.



**DeleteWithInstance ** <span data-label="purple">boolean </span>`Sample value: false`

Whether to release the volume with the instance. Value:


* true: The volume is released with the instance.

* false: The volume is not released with the instance.



**ExtraPerformanceTypeId ** <span data-label="purple">string </span>`Sample value: Balance`

The type of additional performance for the volume. This feature is only supported by ESSD FlexPL data volumes. For more information about additional performance, please refer to [Volume additional performance](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume). Valid range:


* Balance: Balanced additional performance.

* IOPS: IOPS additional performance.

* Throughput: Additional performance related to throughput.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**ExtraPerformanceIOPS ** <span data-label="purple">integer </span>`Sample value: 1`

The capacity of additional IOPS performance (unit:ops/sec, operations per second) for the volume. Only ESSD FlexPL data volumes support additional IOPS performance. When `ExtraPerformanceTypeId` is set to `Balance` or `IOPS`, configure this parameter. The value ranges for each type of extra performance are as follows:


* IOPS: 1–50000

* Balance: 1–50000


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid value: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**ExtraPerformanceThroughputMB ** <span data-label="purple">integer </span>`Sample value: 1`

The capacity of additional throughput performance (unit: MB/s) for the volume. Only ESSD FlexPL data volumes support additional throughput performance. When `ExtraPerformanceTypeId` is `Throughput`, configure this parameter. Value range: 1–650.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume, and this parameter can be normally passed in.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple volumes with ampersands (&).</div>




**SnapshotId ** <span data-label="purple">string </span>`Sample value: snap-31ak39j5bh8rubsn****`

Only data volumes can be created with a snapshot. You can call the [DescribeSnapshots](https://docs.byteplus.com/en/docs/ecs/Describesnapshots) operation to query the snapshot ID.


* Argument \- N: indicates the serial number of the volume. Valid range: 1–16. N = 1 indicates the system volume. When N is passed in as 1, this parameter is ignored. N ≥ 2 indicates the data volume. Therefore, you can pass in the snapshot ID for the target data volume.

* Multiple volumes are separated with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only ESSD supports volume creation using snapshots. PTSSD does not support snapshot\-related features.</div>


* <div data-tips="true" data-tips-type="tip">Only snapshots in "Available" status support new volume creation. Snapshots in statuses "Creating", "Rolling Back", "Deleting", and "Error" do not support new volume creation.</div>





**NetworkInterfaces ** <span data-label="purple">object[]</span>

Information about the network interface mounted to the instance.


**SubnetId ** <span data-label="purple">string </span>`Sample value: subnet-3tispp1nai4e8i****`

Subnet ID.



**SecurityGroupIds ** <span data-label="purple">string[] </span>`Sample value: [sg-3ti78x9h8t4bw*****,sg-3cj59ih2v9hj46c6rr******]`

The security group ID.




**Eip ** <span data-label="purple">object</span>

The information about the EIP associated with the instance.


**Bandwidth ** <span data-label="purple">integer </span>`Sample value: 1`

The maximum bandwidth for the EIP. Unit: Mbps.


* Value range: 1 to 200.

* Default value: 1



**ISP ** <span data-label="purple">string </span>`Sample value: BGP`

The EIP ISP type. Valid values:


* BGP: BGP (Multi\-ISP).

* ChinaMobile: China Mobile static single\-ISP.

* ChinaTelecom: China Telecom static single\-ISP.

* ChinaUnicom: China Unicom static single\-ISP.



**SecurityProtectionTypes ** <span data-label="purple">string[] </span>`Sample value: [AntiDDoS_Enhanced]`

The security protection type of EIP. Value:


* AntiDDoS_Enhanced: Apply for EIP with enhanced protection type. Then the instance can be secured with Anti\-DDoS Origin (Enterprise Edition).



**BandwidthPackageId ** <span data-label="purple">string </span>`Sample value: bwp-2zeo05qre24nhrqpy****`

The ID of the shared bandwidth package.



**SecurityProtectionInstanceId ** <span data-label="purple">integer </span>`Sample value: 151`

The ID of the security package.



**BillingType ** <span data-label="purple">integer </span>`Sample value: 2`

The metering method of Elastic IP address (EIP). Valid values:


* 2: Pay\-as\-you\-go (pay\-by\-bandwidth).

* 3: Pay\-as\-you\-go (pay\-by\-data\-transfer).



**ReleaseWithInstance ** <span data-label="purple">boolean </span>`Sample value: false`

Whether the EIP is deleted along with the instance. This feature is only available for pay\-as\-you\-go EIPs. Value:


* true: The EIP is deleted along with the instance. When an instance is automatically reclaimed by the system (for example, 24 hours after unsubscription or upon expiration) or deleted via the [DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) or [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API, the EIP is released along with the instance.

* false (default): The EIP is not deleted when the instance is deleted.




**Tags ** <span data-label="purple">object[]</span>

The tag information of the instance.


**Key ** <span data-label="purple">string </span>`Sample value: keydemo`

Tag key of the instance.



**Value ** <span data-label="purple">string </span>`Sample value: valuedemo`

The tag value of the instance.




**ScheduledInstance ** <span data-label="purple">object</span>

The information of the ESI order.


**ScheduledInstanceName ** <span data-label="purple">string </span>`Sample value: ESI-Name`

The name of the ESI order.



**ScheduledInstanceDescription ** <span data-label="purple">string </span>`Sample value: this is a test order`

The description of the ESI order.




**DeploymentSetId ** <span data-label="purple">string </span>`Sample value: dps-yc1o9aahks5m57nk****`

The ID of the deployment set that the instance is added to.



**DeploymentSetGroupNumber ** <span data-label="purple">integer </span>`Sample value: 1`

When an ECS instance is to join or adjust to a deployment set with the AvailabilityGroup policy, this parameter can be used to specify the group number of the instance within the deployment set.



**KeepImageCredential ** <span data-label="purple">boolean </span>`Sample value: false`

Whether to keep image settings. Value:


* true: Keep image settings. This allows you to use the password or key pair specified for the image to log in to the ECS instance.

* false (default): Does not keep image settings.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only custom images and shared images support this feature.</div>


* <div data-tips="true" data-tips-type="tip">When the value of this parameter is <code>true</code>, do not pass in <code>KeyPairName</code>.</div>





**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2022-04-10T18:29:38+08:00`

The creation time of the instance launch template.



**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2022-04-14T18:29:38+08:00`

The update time of the instance launch template.



**VersionNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The template version number.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeLaunchTemplateVersions&Version=2020-04-01&LaunchTemplateId=lt-ysxc16auaugh9zfy**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202401301658273AB316284D07320****",
        "Action": "DescribeLaunchTemplateVersions",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "",
        "LaunchTemplateVersions": [
            {
                "LaunchTemplateId": "lt-ysxc16auaugh9zfy****",
                "VersionNumber": 1,
                "VersionDescription": "",
                "LaunchTemplateVersionData": {
                    "ZoneId": "",
                    "InstanceTypeId": "ecs.t2-c1m1.large",
                    "ImageId": "image-yco8plt02em0t*******",
                    "InstanceChargeType": "",
                    "InstanceName": "for-test",
                    "Description": "",
                    "HostName": "test",
                    "UniqueSuffix": true,
                    "SuffixIndex": 1,
                    "KeyPairName": "******",
                    "SecurityEnhancementStrategy": "InActive",
                    "UserData": "ZWNobyBoZWxsbyxxxxxxx",
                    "HpcClusterId": "",
                    "Volumes": [
                        {
                            "VolumeType": "ESSD_PL0",
                            "Size": 40,
                            "DeleteWithInstance": false
                        },
                        {
                            "VolumeType": "ESSD_PL0",
                            "Size": 40,
                            "DeleteWithInstance": false
                        }
                    ],
                    "NetworkInterfaces": [
                        {
                            "SubnetId": "subnet-imc2pmpasbuo8gbssz******",
                            "SecurityGroupIds": [
                                "sg-2ff4fhdtlo8ao59gp67******"
                            ]
                        }
                    ],
                    "Eip": {
                        "Bandwidth": 1,
                        "ISP": "BGP",
                        "BillingType": 3,
                        "BandwidthPackageId": "",
                        "SecurityProtectionTypes": [],
                        "SecurityProtectionInstanceId": 0
                    },
                    "VpcId": "",
                    "ProjectName": "",
                    "Tags": [],
                    "SpotStrategy": "",
                    "SpotPriceLimit": 0,
                    "ScheduledInstance": {
                        "ScheduledInstanceName": "",
                        "ScheduledInstanceDescription": ""
                    }
                },
                "CreatedAt": "2024-03-22T14:24:48+08:00",
                "UpdatedAt": "2024-03-22T14:24:48+08:00"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).
