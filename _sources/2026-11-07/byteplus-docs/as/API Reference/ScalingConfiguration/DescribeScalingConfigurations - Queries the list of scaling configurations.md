---
title: "DescribeScalingConfigurations - Queries the list of scaling configurations"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations"
---

Query scaling configuration information. If there is no matching scaling configuration, the non\-matching item will be automatically ignored and the query of other scaling configurations will continue.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeScalingConfigurations&groupName=%E4%BC%B8%E7%BC%A9%E9%85%8D%E7%BD%AE&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|zlhciE">必选</span> `Sample value: DescribeScalingConfigurations`

The operation that you want to perform. Valid value: DescribeScalingConfigurations.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OWvG4r">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ScalingGroupId ** <span data-label="purple">string </span>`Optional` `Sample value: scg-ybmssdnnhn5pkgyd****`

The ID of the scaling group. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.



**ScalingConfigurationIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID. Value:


* Parameter \- N: specifies the serial number of the scaling configuration. Valid value: 1–10.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The page number of the list. The default value is 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries on each page in a pagination query. Valid values: 1–100.

Default value: 10.



**ScalingConfigurationNames.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: scaling-config-1`

The name of the scaling configuration. Valid value:


* Parameter \- N: specifies the serial number of the scaling configuration. Valid value: 1–10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries per page.



**ScalingConfigurations ** <span data-label="purple">object[] </span>`Sample value: --`

The information of scaling configurations that meet the conditions.


**HostName ** <span data-label="purple">string </span>`Sample value: instance-host-name`

Instance hostname.



**ImageId ** <span data-label="purple">string </span>`Sample value: image-ybmihi8jc7l8j1tz****`

The image ID.



**InstanceDescription ** <span data-label="purple">string </span>`Sample value: ECS instance`

The description of the instance.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2022-04-10T18:29:38+08:00`

The creation time of the scaling configuration.



**Eip ** <span data-label="purple">object </span>`Sample value: --`

The detailed information of the EIP.


**ReleaseWithInstance ** <span data-label="purple">boolean</span>

Whether the EIP is deleted along with the instance. This feature is only available for pay\-as\-you\-go EIPs. This parameter takes effect only when an instance with a Pay\-as\-you\-go EIP is deleted in the ECS console. For the retention rules of EIPs when instances are removed from the scaling group, see the detailed description in [Instance management](https://docs.byteplus.com/en/docs/as/Managing-instances). Value:


* true: The EIP is deleted along with the instance.

* false: The EIP is not deleted when the instance is deleted.



**Bandwidth ** <span data-label="purple">integer </span>`Sample value: 1`

The peak bandwidth of the EIP. Unit: Mbps.

If the scaling configuration does not have an EIP configured, an empty value is returned.



**BillingType ** <span data-label="purple">string </span>`Sample value: PostPaidByBandwidth`

The billing method of the EIP. Valid values:


* PostPaidByBandwidth: Pay\-as\-you\-go\-Pay\-by\-bandwidth.

* PostPaidByTraffic: Pay\-as\-you\-go\-Pay\-by\-data\-transfer.



**ISP ** <span data-label="purple">string </span>`Sample value: BGP`

The EIP line type. Valid values:


* BGP: BGP line.

* If your account has applied for static single\-line access, the ISP parameter can also be set to ChinaMobile (China Mobile), ChinaTelecom (China Telecom), or ChinaUnicom (China Unicom).

* If the scaling configuration does not have an EIP configured, an empty value is returned.



**BandwidthPackageId ** <span data-label="purple">string </span>`Sample value: bwp-2zeo05qre24nhrqpy****`

ID of the Shared Bandwidth Package.



**SecurityProtectionInstanceId ** <span data-label="purple">integer </span>`Sample value: 193`

The ID of the security package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Data is returned only when <code>Eip.SecurityProtectionTypes.N</code> is not empty.</div>




**SecurityProtectionTypes ** <span data-label="purple">string[] </span>`Sample value: AntiDDoS_Enhanced`

The security protection type of EIP. Value:


* AntiDDoS_Enhanced: EIP of the Security Enhanced type, which can be added to an Anti\-DDoS Origin instance.

* If no value is specified, an EIP of the basic protection type is used.




**LifecycleState ** <span data-label="purple">string </span>`Sample value: Active`

The status of the scaling configuration in the scaling group. Valid value:


* InActive: Idle.

* Active: Associated with the scaling group.



**SecurityEnhancementStrategy ** <span data-label="purple">string </span>`Sample value: Active`

Whether to enable security enhancement. Value:


* Active: Enables security enhancement. This feature is effective for public images only.

* InActive: Disables security enhancement. This feature is effective for all images.



**ScalingGroupId ** <span data-label="purple">string </span>`Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID.



**InstanceName ** <span data-label="purple">string </span>`Sample value: instance-1`

The instance name.



**InstanceTypes ** <span data-label="purple">string[] </span>`Sample value: ecs.c2i.xlarge`

The instance type.



**KeyPairName ** <span data-label="purple">string </span>`Sample value: kp-test-123`

The name of the key pair.



**ScalingConfigurationId ** <span data-label="purple">string </span>`Sample value: scc-ybmt16auaugh9zfy****`

The scaling configuration ID.



**UpdatedAt ** <span data-label="purple">string </span>`Sample value: 2022-04-14T18:29:38+08:00`

The update time of the scaling configuration.



**UserData ** <span data-label="purple">string </span>`Sample value: ZWNobyBoZWxsbyBlY3Mh`

Instance custom data.



**ZoneId ** <span data-label="purple">string </span>`Sample value: cn-beijing-a`

The ID of the availability zone to which the instance belongs.



**Volumes ** <span data-label="purple">object[] </span>`Sample value: --`

The information about the volume.


**ExtraPerformanceTypeId ** <span data-label="purple">string </span>`Sample value: IOPS`

The type of additional performance for the volume. This feature is only supported by ESSD FlexPL data volumes. For more information about additional performance, please refer to [Volume additional performance](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume).

Valid range:


* Balance: balanced additional performance.

* IOPS: IOPS additional performance.

* Throughput: throughput additional performance.



**ExtraPerformanceIOPS ** <span data-label="purple">integer </span>`Sample value: 40`

The capacity of additional IOPS performance (unit:ops/sec, operations per second) for the volume. Only ESSD FlexPL data volumes support additional IOPS performance. A return value is available when ExtraPerformanceTypeId is set to Balance or IOPS.



**ExtraPerformanceThroughputMB ** <span data-label="purple">integer </span>`Sample value: 40`

The additional throughput performance of the volume. Only supported for ESSD FlexPL data volumes. Unit: MB/s. A return value is available when ExtraPerformanceTypeId is set to Balance or IOPS.



**Size ** <span data-label="purple">integer </span>`Sample value: 100`

The volume capacity. Unit: GiB.



**VolumeType ** <span data-label="purple">string </span>`Sample value: ESSD_PL0`

The volume type. Valid values:


* ESSD_FlexPL: ESSD FlexPL.

* ESSD_PL0: ESSD PL0.



**DeleteWithInstance ** <span data-label="purple">boolean </span>`Sample value: true`

Whether the volume is released with the instance:


* true: The volume is released with the instance.

* false: The volume is not released with the instance.


When "false" is passed in, this configuration is invalid on the system volume. By default, the system volume is released with the instance and can not be retained.




**SecurityGroupIds ** <span data-label="purple">string[] </span>`Sample value: sg-3ti78x9h8t4bw*****`

The list of security group IDs associated with the instance's primary network interface.



**ScalingConfigurationName ** <span data-label="purple">string </span>`Sample value: scaling-config-test`

The scaling configuration name.



**HpcClusterId ** <span data-label="purple">string </span>`Sample value: hpcCluster-ycdj7d9ios38dfny****`

The ID of the HPC cluster to which the instance belongs.

A return value is available only when the scaling configuration is associated with the HPC\-optimized instance type.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The project to which the instance created based on the scaling configuration belongs.



**InstanceChargeType ** <span data-label="purple">string </span>`Sample value: PostPaid`

The billing method of instances created based on the scaling configuration. Value:


* PostPaid: Pay\-as\-you\-go.



**SpotStrategy ** <span data-label="purple">string </span>`Sample value: NoSpot`

The spot policy of the instances. Value:


* NoSpot: Creates regular Pay\-as\-you\-go instances.

* SpotAsPriceGo: Creates spot instances with auto\-bidding that follows the current market price.

* SpotWithPriceLimit: Creates spot instances with a user\-defined maximum bid price.



**Ipv6AddressCount ** <span data-label="purple">integer </span>`Sample value: 0`

Whether to assign IPv6 addresses to the instance's network interfaces. Value:


* 0: Do not assign IPv6 addresses.

* 1: Assign IPv6 addresses. The system automatically allocates an IPv6 CIDR block.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tag information of instances created based on the scaling configuration.


**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**InstanceTypeOverrides ** <span data-label="purple">object[] </span>`Sample value: --`

The type information of spot instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A return value is available only when <code>SpotStrategy</code> is set to SpotWithPriceLimit.</div>



**InstanceType ** <span data-label="purple">string </span>`Sample value: ecs.g2i.large`

The type of spot instances.



**PriceLimit ** <span data-label="purple">float </span>`Sample value: 0.001`

The maximum hourly price for the spot instance type.





**TotalCount ** <span data-label="purple">integer </span>`Sample value: 20`

The total number of scaling configurations that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeScalingConfigurations&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T095413Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2024050717541713422813223986CA3B",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 10,
    "ScalingConfigurations": [
      {
        "Eip": {
          "Bandwidth": 1,
          "BillingType": "PostPaidByBandwidth",
          "ISP": "BGP",
          "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
          "SecurityProtectionInstanceId": 193,
          "SecurityProtectionTypes": [
            "AntiDDoS_Enhanced"
          ]
        },
        "HostName": "instance-host-name",
        "ImageId": "image-ybmihi8jc7l8j1tz****",
        "InstanceDescription": "云服务器实例",
        "CreatedAt": "2022-04-10T18:29:38+08:00",
        "ScalingConfigurationName": "scaling-config-test\t",
        "SecurityGroupIds": [
          "sg-3ti78x9h8t4bw*****"
        ],
        "LifecycleState": "Active",
        "SecurityEnhancementStrategy": "Active",
        "Volumes": [
          {
            "Size": 100,
            "VolumeType": "ESSD_PL0",
            "DeleteWithInstance": true
          }
        ],
        "ZoneId": "cn-beijing-a",
        "UserData": "ZWNobyBoZWxsbyBlY3Mh",
        "UpdatedAt": "2022-04-14T18:29:38+08:00",
        "ScalingConfigurationId": "scc-ybmt16auaugh9zfy****",
        "KeyPairName": "kp-test-123\t",
        "InstanceTypes": [
          "ecs.c1.xlarge"
        ],
        "InstanceName": "instance-1",
        "ScalingGroupId": "scc-ybmt16auaugh9zfy****",
        "HpcClusterId": "hpcCluster-ycdj7d9ios38dfny****",
        "ProjectName": "default",
        "InstanceChargeType": "PostPaid",
        "SpotStrategy": "NoSpot",
        "Ipv6AddressCount": 0,
        "Tags": [
          {
            "Key": "k1",
            "Value": "v1"
          },
        ],
        "InstanceTypeOverrides": [
          {
            "InstanceType": "ecs.g2i.large",
            "PriceLimit": 0.001
          }
        ]
      },
    ],
    "TotalCount": 20
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.ScalingConfigurationIds |You've reached the limit on the number of ScalingConfigurationIds. |The number of scaling configuration IDs has reached the upper limit. |
|400 |LimitExceeded.ScalingConfigurationNames |You've reached the limit on the number of ScalingConfigurationName. |The number of scaling configuration names has reached the upper limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
