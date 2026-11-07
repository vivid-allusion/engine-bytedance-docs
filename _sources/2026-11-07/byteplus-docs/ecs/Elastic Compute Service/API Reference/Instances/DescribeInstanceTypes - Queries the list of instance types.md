---
title: "DescribeInstanceTypes - Queries the list of instance types"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes"
---

Call the DescribeInstanceTypes operation to query information about all instance types provided by ECS, or to query information about the specified instance types.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

You can call this operation to query only the configuration and performance information of instance types. To query instance types that can be purchased in a specific availability zone, use [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstanceTypes&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|VAPBP1">必选</span> `Sample value: DescribeInstanceTypes`

The operation that you want to perform. Valid value: DescribeInstanceTypes.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|NGecOQ">必选</span>  `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ImageId ** <span data-label="purple">string </span>`Optional` `Sample value: image-ydam1k535clzp*****`

The ID of the image. You can specify this parameter to query the types of instances that can be created based on the image.



**InstanceTypeIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: InstanceTypeIds.1=ecs.g3i.large&InstanceTypeIds.2=ecs.g1ve.8xlarge`

The instance type that you want to query. For valid values, see [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).


* Parameter \- N: This specifies the serial number of the instance type. Valid value: 1–100. When N is greater than 100, only the first 100 sequence numbers take effect.

* Separate multiple InstanceTypeId values with &.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, if you do not configure this parameter, information about all instance types is queried.</div>




**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Maximum value: 1000

* Minimum value: 1

* Default value: 10



**NextToken ** <span data-label="purple">string </span>`Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceTypes ** <span data-label="purple">object[] </span>`Sample value: --`

The information about instance types that meet the conditions.


**AffinityGroupSizes ** <span data-label="purple">integer[] </span>`Sample value: 2`

The affinity group specification.



**BaselineCredit ** <span data-label="purple">long </span>`Sample value: 20`

The baseline CPU performance that a burstable instance can steadily provide is determined by its instance type.



**Gpu ** <span data-label="purple">object </span>`Sample value: --`

The GPU specification information.


**GpuDevices ** <span data-label="purple">object[] </span>`Sample value: --`

The list of GPU device information.


**Count ** <span data-label="purple">integer </span>`Sample value: 4`

The number of GPU cards.



**Memory ** <span data-label="purple">object </span>`Sample value: --`

The video memory information.


**EncryptedSize ** <span data-label="purple">integer </span>`Sample value: 8192`

The encrypted memory size. Unit: MiB. Valid range: 0 to 256 \* 1024.


* When the` InstanceTypeFamily `value is ecs.ebmg2t (denoting a Security Enhanced EBM instance), encrypted memory is allocated, with a maximum capacity of 256 GiB. For all other instance types, the default allocated encrypted memory is 0 GiB.

* The Security Enhanced EBM instance is in Beta. If you need a trial, contact your account manager.



**Size ** <span data-label="purple">integer </span>`Sample value: 4096`

Memory size. Unit: MiB.




**ProductName ** <span data-label="purple">string </span>`Sample value: NVIDIA A100`

The GPU model.





**InitialCredit ** <span data-label="purple">long </span>`Sample value: 60`

The CPU credits you can obtain at one time after you create a burstable instance. You can obtain 30 credits per vCPU.



**InstanceTypeFamily ** <span data-label="purple">string </span>`Sample value: ecs.g3i`

The instance family.



**InstanceTypeId ** <span data-label="purple">string </span>`Sample value: ecs.g3i.large`

Instance type.



**IsSupportAffinityGroup ** <span data-label="purple">boolean </span>`Sample value: false`

Whether the instance type supports affinity groups. Valid values:


* true: Supported.

* false: Not supported.



**IsSupportJumboFrame ** <span data-label="purple">boolean </span>`Sample value: false`

Whether the instance type supports jumbo frames. Valid values:


* true: Supported.

* false: Not supported.



**LocalVolumes ** <span data-label="purple">object[] </span>`Sample value: --`

The local volume configuration information corresponding to the instance type.


**Count ** <span data-label="purple">integer </span>`Sample value: 4`

The number of local volumes mounted to the instance.



**Size ** <span data-label="purple">integer </span>`Sample value: 200`

The capacity of one local volume mounted on the instance. Unit: GiB



**VolumeType ** <span data-label="purple">string </span>`Sample value: LOCAL_SSD`

The local volume type. Valid values:


* LOCAL_SSD: local SSD

* LOCAL_HDD: local HDD




**Memory ** <span data-label="purple">object </span>`Sample value: --`

The memory information of the instance type.


**EncryptedSize ** <span data-label="purple">integer </span>`Sample value: 8192`

The encrypted memory size. Unit: MiB. Valid range: 0 to 256 \* 1024.


* When the` InstanceTypeFamily `value is ecs.ebmg2t (denoting a Security Enhanced EBM instance), encrypted memory is allocated, with a maximum capacity of 256 GiB. For all other instance types, the default allocated encrypted memory is 0 GiB.

* The Security Enhanced EBM instance is in Beta. If you need a trial, contact your account manager.



**Size ** <span data-label="purple">integer </span>`Sample value: 4096`

Memory size. Unit: MiB.




**Network ** <span data-label="purple">object </span>`Sample value: --`

The network information of the instance type.


**VrdmaCrossS2BandwidthMbps ** <span data-label="purple">integer </span>`Sample value: 50`

The rate limiting bandwidth of the vRdam cross\-S2 switch. Unit: Mbps.



**BaselineBandwidthMbps ** <span data-label="purple">integer </span>`Sample value: 2000`

The network baseline bandwidth capability (outbound/inbound). Unit: Mbps.



**MaximumBandwidthMbps ** <span data-label="purple">integer </span>`Sample value: 2000`

The peak network bandwidth (outbound/inbound). Unit: Mbps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the specified instance type does not support burst capability, the return value of <code>MaximumBandwidthMbps</code> is the same as the value of <code>BaselineBandwidthMbps</code>. For instance types with burst capability, see <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types</a>.</div>




**MaximumNetworkInterfaces ** <span data-label="purple">integer </span>`Sample value: 8`

The maximum number of elastic network interfaces that can be mounted.

The maximum number of elastic network interfaces that can be mounted varies based on the instance type. For more information, see [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).



**MaximumPrivateIpv4AddressesPerNetworkInterface ** <span data-label="purple">integer </span>`Sample value: 20`

The maximum number of IPv4 addresses for a single elastic network interface. For more information, see [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).



**MaximumQueuesPerNetworkInterface ** <span data-label="purple">integer </span>`Sample value: 16`

The maximum number of queues supported by a single elastic network interface, including those supported by the primary and secondary network interfaces. For more information, see [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).



**MaximumThroughputKpps ** <span data-label="purple">integer </span>`Sample value: 150`

The maximum throughput (outbound + inbound), in Kpps.




**Processor ** <span data-label="purple">object </span>`Sample value: --`

The CPU information of the instance type.


**BaseFrequency ** <span data-label="purple">float </span>`Sample value: 2.3`

The CPU base frequency. Unit: GHz.



**Cpus ** <span data-label="purple">integer </span>`Sample value: 8`

Number of CPUs.



**Model ** <span data-label="purple">string </span>`Sample value: Intel Xeon(Ice Lake) Platinum 8336C`

The CPU model.



**TurboFrequency ** <span data-label="purple">float </span>`Sample value: 3.0`

The CPU Turbo Boost frequency. Unit: GHz.




**Rdma ** <span data-label="purple">object </span>`Sample value: --`

The RDMA specification information.


**RdmaNetworkInterfaces ** <span data-label="purple">integer </span>`Sample value: 2`

The number of RDMA network interfaces.



**RdmaProductName ** <span data-label="purple">string </span>`Sample value: Mellanox BlueField3`

The model of the RDMA network interface.




**Volume ** <span data-label="purple">object </span>`Sample value: --`

The volume information of the instance type.


**MaximumCount ** <span data-label="purple">integer </span>`Sample value: 16`

The maximum number of volumes that can be mounted.

The maximum number of volumes that can be mounted varies based on the instance type. For more information, see [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). Valid values:


* 4: Maximum number of volumes supported by t2 burstable instances.

* 15: Maximum number of volumes supported by first\-generation instances except for g1ie, c1ie, and r1ie.

* 16: Maximum number of volumes supported by g1ie, c1ie, r1ie, and second\- and third\-generation instances.



**SupportedVolumeTypes ** <span data-label="purple">string[] </span>`Sample value: [ "ESSD_FlexPL", "ESSD_PL0"]`

The list of supported volume types.





**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query token returned by this API call. An empty value indicates that there is no next page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeInstanceTypes&Version=2020-04-01&InstanceTypeIds.1=ecs.g3i.large HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2021110417394001022514606307D7****",
    "Action": "DescribeInstanceTypes",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "InstanceTypes": [
      {
        "InstanceTypeFamily": "ecs.g3i",
        "Gpu": null,
        "Rdma": null,
        "BaselineCredit": 0,
        "InitialCredit": 0,
        "InstanceTypeId": "ecs.g3i.large",
        "IsSupportEsi": "true",
        "IsSupportAffinityGroup": false,
        "AffinityGroupSizes": [],
        "IsSupportJumboFrame": false,
        "Processor": {
          "Cpus": 2,
          "Model": "Intel Xeon(Ice Lake) Platinum 8336C",
          "BaseFrequency": 2.3,
          "TurboFrequency": 3
        },
        "Memory": {
          "Size": 8192,
          "EncryptedSize": 0
        },
        "Network": {
          "MaximumNetworkInterfaces": 3,
          "MaximumPrivateIpv4AddressesPerNetworkInterface": 6,
          "MaximumQueuesPerNetworkInterface": 2,
          "BaselineBandwidthMbps": 2000,
          "MaximumBandwidthMbps": 2000,
          "MaximumThroughputKpps": 500
        },
        "LocalVolumes": [],
        "Volume": {
          "SupportedVolumeTypes": [
            "ESSD_FlexPL",
            "ESSD_PL0"
          ],
          "MaximumCount": 16
        }
      }
    ],
    "NextToken": "bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The requested API does not exist. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |You have exceeded the rate limit for resource requests. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
