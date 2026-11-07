---
title: "DescribeInstances - Queries instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInstances"
---

Call the DescribeInstances operation to obtain instance information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

When you call this operation, the number of instances queried via `TagFilters.N.Key` and `TagFilters.N.Values.N` can not exceed 1,000. If the number of instances to be queried exceeds 1,000, call the [DesribeTags](https://docs.byteplus.com/en/docs/ecs/DescribeTags) operation.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstances&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|onhxkg">必选</span> `Sample value: DescribeInstances`

The action that you want to perform. Value: DescribeInstances.



**Version**<span data-label="purple"> string </span><span data-api-tag="require|ODuLct">必选</span> ` Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**AffinityGroupIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: AffinityGroupIds.1=affinityGroup-ydp80pygaoujldck****&AffinityGroupIds.2=affinityGroup-ydp7hq2wowujldck****`

Affinity group ID. A maximum of 100 affinity group IDs is supported.


* Argument \- N: specifies the serial number of the affinity group.

* Multiple IDs are divided with ampersands (&).



**DeploymentSetGroupNumbers.N ** <span data-label="purple">integer[] </span>`Optional` `Sample value: DeploymentSetGroupNumbers.1=1&DeploymentSetGroupNumbers.2=2`

Use the group number of a deployment set to query instances within the corresponding deployment set group.


* Argument \- N: Indicates the serial number of the deployment set group. The value range is 1 to 7.

* Multiple DeploymentSetGroupNumber values are divided with &.



**DeploymentSetIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: DeploymentSetIds.1=dps-yc1o9aahks5m57nk****&DeploymentSetIds.2=dps-ybr1vulgy87grbt6****`

Use the deployment set ID to query the instances within the corresponding deployment set.


* Argument \- N: specifies the serial number of the deployment set. Valid range: 1\-100.

* Separate multiple deployment set IDs with &.



**EipAddresses.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: EipAddresses.1=12.XX.XX.89&EipAddresses.2=12.XX.XX.35`

EIP address. A maximum of 100 EIP addresses is supported. You can call the [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) operation to query EIP addresses.


* Argument \- N: specifies the serial number of the EIP address.

* Multiple EIP addresses are divided with ampersands (&).



**HpcClusterId ** <span data-label="purple">string </span>`Optional` `Sample value: hpcCluster-3tean8ni5m3vj0wz****`

When you query an HPC\-optimized instance, you can specify the HPC Cluster ID for the instance.



**InstanceChargeType ** <span data-label="purple">string </span>`Optional` `Sample value: PostPaid`

Billing method of the instance. Value:


* PostPaid: pay\-as\-you\-go

* PrePaid: subscription



**InstanceIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: InstanceIds.1=i-3ti9101aju3vj0******&InstanceIds.2=i-3tiegs1y963vj0******`

The instance ID. A maximum of 100 instance IDs are supported.


* Parameter \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with ampersands (&).



**InstanceName ** <span data-label="purple">string </span>`Optional` `Sample value: instance-test`

The name of the instance. Fuzzy queries with keywords are supported.



**InstanceTypeFamilies.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: InstanceTypeFamilies.1=ecs.g2i&InstanceTypeFamilies.2=ecs.c2i`

Filter instances by instance family. A maximum of 100 instance families are supported.


* Parameter \- N: specifies the serial number of the instance.

* Multiple instance families are divided with &.



**InstanceTypeIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: InstanceTypeIds.1=ecs.g2i.2xlarge&InstanceTypeIds.2=ecs.c2i.2xlarge`

Filter instances by instance type. A maximum of 100 instance types are supported.


* Parameter \- N: specifies the serial number of the instance.

* Multiple instance types are separated by &.



**Ipv6Addresses.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: Ipv6Addresses.1=2406:d440:103:5f00:a4a2:cbe2:efa0:****`

The IPv6 address of the instance.


* Argument \- N: specifies the serial number of the IPv6 address. Valid range: 1\-100.

* Multiple network interfaces are separated by &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The feature of assigning IPv6 addresses to network interfaces is currently in Beta.  If you need a trial, contact your account manager.</div>




**KeyPairName ** <span data-label="purple">string </span>`Optional` `Sample value: kp-test-123`

Name of the key pair.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Maximum value: 100

* Default value: 10



**NextToken ** <span data-label="purple">string </span>`Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**PrimaryIpAddress ** <span data-label="purple">string </span>`Optional` `Sample value: 172.16.XX.XX`

Private IP address of the instance, such as the IP address of the primary network interface or secondary network interface.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: project_a`

The project to which the resource belongs. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**ScheduledInstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: esi-ycmfqs85zrm0tqlp****`

ESI order ID.

You can call [DescribeScheduledInstances](https://docs.byteplus.com/en/docs/ecs/DescribeScheduledInstances) operation to query the ESI order ID.



**Status ** <span data-label="purple">string </span>`Optional` `Sample value: RUNNING`

The status of the instance. Value:


* CREATING: The instance is being created.

* RUNNING: The instance is running.

* Stopping: The instance is being stopped.

* Stopped: The instance is stopped.

* Rebooting: The instance is being restarted.

* Starting: The instance is being started.

* Rebuilding: The instance is being reinstalled.

* Resizing: The instance is being resized.

* Error: Error occurred.

* Deleting: The instance is being deleted.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Key=k1`

The specified tag key when querying resources based on tags.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with &.

* Tag keys must be unique.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The tag value specified when resources are queried based on tags.


* The first N: the serial number of the tag key. Value range: 1–10.

* The second N specifies the serial number of the tag value. Valid range: 1\-3. That is, you can query up to three tag values of the same tag key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




**VpcId ** <span data-label="purple">string </span>`Optional` `Sample value: vpc-3thbinq64t4bwbha****`

VPC ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) operation to query VPCs that meet the condition.



**ZoneId**<span data-label="purple"> string </span>`Optional Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Instances ** <span data-label="purple">object[] </span>`Sample value: --`

The information about instances that meet the conditions.


**RdmaNetworkInterfaceDetails ** <span data-label="purple">object[] </span>`Sample value: --`

When you query HPC\-optimized instances, information about each network interface is returned in list format.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is currently in Beta. To request a trial, please contact the customer manager.</div>



**Gateway ** <span data-label="purple">string </span>`Sample value: 26.xx.xx.46`

The gateway address.



**Ip ** <span data-label="purple">string </span>`Sample value: 26.xx.xx.2`

The IP address.



**Mask ** <span data-label="purple">string </span>`Sample value: 255.xx.xx.254`

The subnet mask.



**SwitchName ** <span data-label="purple">string </span>`Sample value: HB****.VEGS0-0-01`

The switch name.



**SwitchPort ** <span data-label="purple">string </span>`Sample value: ethernet1a`

The switch port.




**AffinityGroupId ** <span data-label="purple">string </span>`Sample value: affinityGroup-ydp80pygaoujldck****`

Affinity group ID.



**CpuOptions ** <span data-label="purple">object </span>`Sample value: --`

CPU configuration detail.


**CoreCount ** <span data-label="purple">integer </span>`Sample value: 4`

The number of CPU physical cores



**ThreadsPerCore ** <span data-label="purple">integer </span>`Sample value: 2`

Number of threads per CPU core. It indicates whether hyper\-threading is enabled for the CPU.

Valid values:


* 1: Disable hyper\-threading

* 2: Enable hyper\-threading

   vCPU count = number of physical CPU cores \* number of threads per core




**Cpus ** <span data-label="purple">integer </span>`Sample value: 4`

Number of CPUs.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2021-06-28T18:29:38+08:00`

The creation time.



**DeletionProtection ** <span data-label="purple">boolean </span>`Sample value: true`

The attribute of instance deletion protection. Specify whether to delete the instance through the console or API. Valid values:


* true: Enable instance deletion protection.

* false: Disable instance deletion protection.



**DeploymentSetGroupNumber ** <span data-label="purple">integer </span>`Sample value: 2`

Serial number of the deployment set group.



**DeploymentSetId ** <span data-label="purple">string </span>`Sample value: dps-yc1o9aahks5m57nk****`

The ID of deployment set to which the instance belongs.



**Description ** <span data-label="purple">string </span>`Sample value: ECS instance for testing.`

Instance description.



**EipAddress ** <span data-label="purple">object </span>`Sample value: --`

The list of EIPs associated with the instance.


**AllocationId ** <span data-label="purple">string </span>`Sample value: eip-2749d8a20h4hs7fap8taa****`

The ID of an EIP.



**IpAddress ** <span data-label="purple">string </span>`Sample value: 101.126.XX.XX`

EIP address.




**ElasticScheduledInstanceType ** <span data-label="purple">string </span>`Sample value: NoEsi`

The ESI type. Value:


* NoEsi: non\-ESI type.

* Esi: ESI type.

* Segmented: ESI\-Segmented



**EnableJumboFrame ** <span data-label="purple">boolean </span>`Sample value: false`

Whether jumbo frames are enabled for the instance. Valid values:


* true: NAT Traversal is enabled.

* false: NAT Traversal is not enabled.



**ExpiredAt ** <span data-label="purple">string </span>`Sample value: 2200-01-01T00:00:00+08:00`

Expiration time of the instance.

This argument can be returned only when `InstanceChargeType` is set to `PrePaid`.



**Hostname ** <span data-label="purple">string </span>`Sample value: instance-host-name`

Instance hostname.



**HpcClusterId ** <span data-label="purple">string </span>`Sample value: hpcCluster-3tean8ni5m3vj0******`

The HPC cluster ID.



**ImageId ** <span data-label="purple">string </span>`Sample value: image-3tefr6wgx63vj0******`

The image ID.



**InstanceChargeType ** <span data-label="purple">string </span>`Sample value: PostPaid`

Billing method of the instance. Value:


* PostPaid: pay\-as\-you\-go

* PrePaid: subscription



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-3ti9101aju3vj0******`

The instance ID.



**InstanceName ** <span data-label="purple">string </span>`Sample value: instance-test`

The instance name.



**InstanceTypeId ** <span data-label="purple">string </span>`Sample value: ecs.c2i.xlarge`

Instance type.



**KeyPairId ** <span data-label="purple">string </span>`Sample value: kp-3tgh3ifp8j44kd******`

Key pair ID.



**KeyPairName ** <span data-label="purple">string </span>`Sample value: kp-test-123`

The name of the key pair.



**LocalVolumes ** <span data-label="purple">object[] </span>`Sample value: --`

The local volume configuration of the instance​.


**Count ** <span data-label="purple">integer </span>`Sample value: 4`

The number of local volumes mounted on the instance.



**Size ** <span data-label="purple">integer </span>`Sample value: 200`

The capacity of one local volume mounted on the instance. Unit: GiB



**VolumeType ** <span data-label="purple">string </span>`Sample value: LOCAL_SSD`

The local volume type. Valid values:


* LOCAL_SSD: local SSD

* LOCAL_HDD: local HDD




**MemorySize ** <span data-label="purple">integer </span>`Sample value: 32768`

Memory size. Unit: MiB.



**MetadataOptions ** <span data-label="purple">object </span>`Sample value: --`

Instance metadata option set.


**HttpTokens ** <span data-label="purple">string </span>`Sample value: optional`

The access mode of instance metadata. You can set whether to enable the security hardening mode. Valid value:


* optional: not mandatory (Normal Mode and Security Hardening Mode)

* required: mandatory (Security Hardening Mode).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information on how to view metadata and the available metadata items, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata">Viewing instance metadata</a>.</div>





**NetworkInterfaces ** <span data-label="purple">object[] </span>`Sample value: --`

Information about the network interface mounted to the instance.


**Ipv6Addresses ** <span data-label="purple">string[] </span>`Sample value: ["2408::153:3921:XX:XX:7b12:1c5f", "2408:4008:2cf:XX:XX:dd1e:2a22:5ddf"]`

IPv6 address of the network interface.



**MacAddress ** <span data-label="purple">string </span>`Sample value: 00:16:3e:5b:** :**`

MAC address.



**NetworkInterfaceId ** <span data-label="purple">string </span>`Sample value: eni-3tiu4lmhwq4e8i******`

Network interface ID.



**PrimaryIpAddress ** <span data-label="purple">string </span>`Sample value: 172.16.XX.XX`

Private IP address.



**SecurityGroupIds ** <span data-label="purple">string[] </span>`Sample value: ["sg-mj48avnqyio05smt1a******","sg-3cj59ih2v9hj46c6rr******"]`

ID of the security group associated with the network interface.



**SubnetId ** <span data-label="purple">string </span>`Sample value: subnet-3tisodmzai4e8i******`

Subnet ID.



**Type ** <span data-label="purple">string </span>`Sample value: primary`

The network interface attribute. Value:


* primary: the primary network interface

* secondary: the secondary network interface



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-3thbinq64t4bwb******`

VPC ID.




**OsName ** <span data-label="purple">string </span>`Sample value: CentOS 7.6 64位`

The operating system of the image.



**OsType ** <span data-label="purple">string </span>`Sample value: Linux`

OS type:


* Linux

* Windows



**Placement ** <span data-label="purple">object </span>`Sample value: --`

Information of the ECS instance deployed on a dedicated host.


**Affinity ** <span data-label="purple">string </span>`Sample value: Default`

For ECS instances in economical mode, some resources are released after instances are stopped. This argument is used to check whether the instances are still deployed on the original host when restarted. Valid values:


* Host: When instances in economical mode are restarted, they are still deployed on the original host.

* Default: When the instance with Economical Mode enabled restarts, it will be preferentially migrated to a host that supports automatic deployment. If resources on the host that supports automatic deployment are insufficient, the instance restarts on the original host.



**DedicatedHostClusterId ** <span data-label="purple">string </span>`Sample value: dc-ycle6b76kgv2wrsm****`

The ID of dedicated host cluster where the instance is deployed.​



**DedicatedHostId ** <span data-label="purple">string </span>`Sample value: dh-bp67acfmxazb4p****`

The ID of the dedicated host on which the instance is deployed.



**Tenancy ** <span data-label="purple">string </span>`Sample value: Default`

Whether to create an instance on a dedicated host. Value:


* Default (default): Create a regular ECS instance.

* Host: Create an ECS instance deployed on a dedicated host. If you do not specify `DedicatedHostId`, the instance is deployed on the dedicated host selected automatically by the system.




**ProjectName ** <span data-label="purple">string </span>`Sample value: project_a`

The project to which the resource belongs. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**RdmaIpAddresses ** <span data-label="purple">string[] </span>`Sample value: ["198.18.xx.xx","198.18.xx.xx"]`

When HPC\-optimized instances are queried, the RDMA IP addresses of each network interface are returned in a list format.



**ScheduledInstanceId ** <span data-label="purple">string </span>`Sample value: esi-ycmfqs85zrm0tqlp****`

ESI order ID.



**SpotPriceLimit ** <span data-label="purple">float </span>`Sample value: 0.78`

The maximum hourly price for spot instances. A maximum of three decimal places for the price is supported.

This argument can be returned only when `SpotStrategy` is set to `SpotWithPriceLimit`.



**SpotStrategy ** <span data-label="purple">string </span>`Sample value: NoSpot`

The spot strategy for the instance billed in pay\-as\-you\-go mode. Value:


* NoSpot (default): Instances are billed in pay\-as\-you\-go mode.

* SpotAsPriceGo: The system automatically bids based on the current market price for the spot instance.

* SpotWithPriceLimit: Spot instance with a price limit.



**Status ** <span data-label="purple">string </span>`Sample value: RUNNING`

Instance state.



**StoppedMode ** <span data-label="purple">string </span>`Sample value: KeepCharging`

Whether the instance enables economical mode. Value:


* KeepCharging (default): Normal Mode. In this mode, after you stop the instance, charges continue and relevant resources are retained.

* StopCharging: Economical Mode. For more information, refer to [Economical mode for pay-as-you-go instances](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances).

* NotApplicable: indicates that this instance does not support economical mode.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

Information about tags associated with resources.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

Tag key of the instance.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value of the instance.




**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2021-06-29T18:11:46+08:00`

Update time.



**Uuid ** <span data-label="purple">string </span>`Sample value: 4f35e8f7-f549-5c55-9531-5f43ca78****`

The unique identifier of the instance. This information does not change with the instance status.



**Volumes ** <span data-label="purple">object[] </span>`Sample value: --`

Information about the volume mounted to the instance.


**VolumeId ** <span data-label="purple">string </span>`Sample value: vol-3wbz8gzti84g6no9****`

Volume ID.




**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-3thbinq64t4bwb******`

VPC ID.



**ZoneId ** <span data-label="purple">string </span>`Sample value: cn-beijing-a`

The availability zone ID.




**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The pagination token returned by this call. If this value is empty, the current page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeInstances&Version=2020-04-01&InstanceIds.1=i-3ti9101aju3vj0****** HTTP/1.1
Host: open.volcengineapi.com
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250220105008F21A3268CDC9D9A2****",
        "Action": "DescribeInstances",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "Instances": [
            {
                "CreatedAt": "2025-02-19T14:43:45+08:00",
                "UpdatedAt": "2025-02-19T14:43:53+08:00",
                "ZoneId": "cn-beijing-b",
                "ImageId": "image-38deuiek3bg6tehx****",
                "Status": "RUNNING",
                "InstanceName": "ECS-MwaP",
                "Description": "",
                "VpcId": "vpc-mj48apqnmcqo5smt1arf****",
                "NetworkInterfaces": [
                    {
                        "NetworkInterfaceId": "eni-mimrg8yzp0jk5smt1axz****",
                        "VpcId": "vpc-mj48apqnmcqo5smt1arf****",
                        "SubnetId": "subnet-rr9k4pzqcb28v0x58k1****",
                        "PrimaryIpAddress": "192.168.**.**",
                        "Type": "primary",
                        "MacAddress": "00:16:3e:42:**:**",
                        "Ipv6Addresses": [],
                        "SecurityGroupIds": [
                            "sg-mj48avnqyio05smt1awh****"
                        ]
                    }
                ],
                "RdmaIpAddresses": [],
                "RdmaNetworkInterfaceDetails": [
                    {
                        "Ip": "26.xx.xx.2",
                        "Mask": "255.xx.xx.254",
                        "Gateway": "26.xx.xx.46",
                        "SwitchName": "HB****.VEGS0-0-7",
                        "SwitchPort": "ethernet1a"
                    }
                ],
                "HpcClusterId": "",
                "KeyPairName": "**",
                "KeyPairId": "kp-yd6njlvoj6ldcrkn****",
                "StoppedMode": "NotApplicable",
                "InstanceChargeType": "PostPaid",
                "DeploymentSetId": "",
                "Tags": [
                    {
                        "Key": "sys:tag:createdBy",
                        "Value": "IAMUser:3723****:****"
                    }
                ],
                "Volumes": [
                    {
                        "VolumeId": "vol-3wbz8gzti84g6no9****"
                    }
                ],
                "InstanceTypeId": "ecs.d2s.xlarge",
                "ProjectName": "default",
                "EipAddress": {
                    "IpAddress": "180.184.**.**",
                    "AllocationId": "eip-13fncoh4gd81s3n6nu5tn****"
                },
                "ExpiredAt": "2200-01-01T00:00:00+08:00",
                "OsType": "Linux",
                "OsName": "CentOS 6.9 64-bit",
                "Cpus": 4,
                "MemorySize": 16384,
                "InstanceId": "i-ydpq4a603kwh2yov****",
                "Hostname": "iv-ydpq4a603kwh2yov****",
                "Uuid": "000c67b5-7da0-0000-000b-b79d02******",
                "EnableJumboFrame": false,
                "LocalVolumes": [
                    {
                        "VolumeType": "LOCAL_HDD",
                        "Size": 7452,
                        "Count": 2
                    }
                ],
                "CpuOptions": {
                    "CoreCount": 2,
                    "ThreadsPerCore": 2
                },
                "DeletionProtection": true,
                "SpotStrategy": "NoSpot",
                "DeploymentSetGroupNumber": 0,
                "Placement": {
                    "DedicatedHostId": "",
                    "Tenancy": "Default",
                    "Affinity": "Default",
                    "DedicatedHostClusterId": ""
                },
                "SpotPriceLimit": 0,
                "ScheduledInstanceId": "",
                "ElasticScheduledInstanceType": "NoEsi",
                "AffinityGroupId": ""
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
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidCpuOptionsCoreCount.Malformed |The specified cpu options core count is malformed. |The specified CoreCount argument is invalid. |
|400 |InvalidCpuOptionsThreadsPerCore.Malformed |The specified cpu options threads per core is malformed. |The specified ThreadsPerCore argument is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The format of the specified tag key for query is invalid.​ ​​ |
|400 |InvalidTagFilterValue.Malformed |The specified TagFilterValue is malformed. |The format of the specified tag value for query is invalid. |
|400 |LimitExceeded.MaximumAffinityGroupIds |The number of specified AffinityGroupIds exceeds the maximum limit. |The specified number of AffinityGroupIds exceeds the maximum limit. |
|400 |LimitExceeded.MaximumDeploymentSetGroupNumbers |You've reached the limit on the number of DeploymentSetGroupNumbers that you can set. |The specified DeploymentSetGroupNumbers exceed the maximum limit. |
|400 |LimitExceeded.MaximumDeploymentSetIds |You've reached the limit on the number of DeploymentSetIds that you can set. |The number of specified deployment sets exceeds the upper limit. |
|400 |LimitExceeded.MaximumEipAddresses |The number of specified EipAddresses exceeds the maximum limit. |The number of specified EipAddresses exceeds the maximum limit. |
|400 |LimitExceeded.MaximumInstanceIds |You've reached the limit on the number of InstanceIds that you can set. |The specified number of instance IDs exceeds the upper limit. |
|400 |LimitExceeded.MaximumInstanceTypeFamilies |You've reached the limit on the number of InstanceTypeFamilies that you can set. |The specified number of InstanceTypeFamilies exceeds the maximum limit. |
|400 |LimitExceeded.MaximumInstanceTypeIds |You've reached the limit on the number of InstanceTypeIds that you can set. |The specified number of InstanceTypeIds exceeds the maximum limit. |
|400 |LimitExceeded.MaximumIpv6Addresses |The number of specified Ipv6Addresses exceeds the maximum limit. |The number of specified Ipv6Addresses exceeds the maximum limit. |
|400 |LimitExceeded.MaximumTagFilterKeys |You've reached the limit on the number of TagFilterKeys that you can set. |The specified query tag key is out of range. |
|400 |LimitExceeded.MaximumTagFilterResults |You've reached the limit on the number of resources that you can describe by TagFilters. |The number of resources filtered by tag exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterValues |You've reached the limit on the number of TagFilterValues that you can set. |The specified query tag value exceeds the valid range. |
|400 |LimitExceeded.PrimaryIpAddresses |You've reached the limit on the number of PrimaryIpAddresses that you can set. |The number of specified IP addresses exceeds the maximum limit. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The requested API does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |You have exceeded the rate limit for resource requests. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
