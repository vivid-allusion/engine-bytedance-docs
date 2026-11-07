---
title: "DescribeScheduledInstances - Queries ESI orders"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeScheduledInstances"
---

Call the DescribeScheduledInstances operation to query Elastic Scheduled Instance (ESI) orders.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeScheduledInstances&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|KFgU2O">必选</span> `Sample value: DescribeScheduledInstances`

The operation that you want to perform. Valid value: DescribeScheduledInstances.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|KNo51V">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**DeliveryType** <span data-label="purple">string</span> `Optional` `Sample value: Reserve`

Delivery type of Elastic Scheduled Instances\-Segmented. Value:


* Reserve (default): Scheduled delivery

* Immediate: Immediate delivery


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You need to pass in this parameter only when <code>ElasticScheduledInstanceType</code> is set to <code>Segmented</code>.</div>


* <div data-tips="true" data-tips-type="tip">This feature is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**ElasticScheduledInstanceType** <span data-label="purple">string</span> `Optional` `Sample value: Esi`

The ESI type. Valid values:


* Esi: Elastic Scheduled Instances (ESI)

* Segmented: Elastic Scheduled Instances\-Segmented


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**ImageId** <span data-label="purple">string</span> `Optional` `Sample value: image-3tefr6wgx63vj0******`

Image ID.



**InstanceTypeIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: InstanceTypeIds.1=ecs.g3i.2xlarge&InstanceTypeIds.2=ecs.g3i.2xlarge`

The instance types that you want to use to filter ESI orders. You can specify up to 100 instance types.


* Parameter \- N: This specifies the serial number of the instance type.

* Use & to separate multiple types.



**KeyPairName** <span data-label="purple">string</span> `Optional` `Sample value: kp-test-123`

Name of the key pair.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries per page.


* Maximum value: 100

* Default value: 10



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: default`

The project to which the resources belong. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**ScheduledInstanceIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: ScheduledInstanceIds.1=si-3tiefmkskq3vj0x0****&ScheduledInstanceIds.2=esi-ycqweb5q3oa8j6lr****`

The ESI order ID. Up to 100 ESI order IDs are supported.


* Parameter \-N: This specifies the serial number of the ESI.

* Multiple IDs are divided with ampersands (&).



**ScheduledInstanceName** <span data-label="purple">string</span> `Optional` `Sample value: ESI-Name`

The name of the ESI order. Valid values:


* Cannot start with a number, a hyphen (\-), or an underscore (_).

* Only Chinese characters, letters, numbers, underscores, and hyphens are allowed.

* The length limit is 1 to 128 characters.

* Special characters are currently not supported.



**Status** <span data-label="purple">string</span> `Optional` `Sample value: CREATING`

The status of the ESI order. Valid values:


* CREATING: The instance is being created.

* PENDING: To be delivered.

* DELIVERING: Being delivered.

* DELIVERED: Delivered.

* FAILED: Delivery failed.

* PART_FAILED: Delivery failed for some ESIs.

* INVALID: Expired.

* CANCELED: Cancelled.



**TagFilters.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Key=k1`

The tag key of the user tag.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with "&". Duplicate tag keys are not allowed.



**TagFilters.N.Values.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The tag value of the user tag.


* The first N specifies the serial number of the tag key. Value range: 1–10.

* The second N specifies the serial number of the tag value. Valid range: 1\-3. That is, you can query up to three tag values of the same tag key.

* Separate multiple key values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>



* <div data-tips="true" data-tips-type="tip">If you do not pass in the TagFilters.N.Key parameter, all tag values corresponding to the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



**ScheduledInstanceInfo** <span data-label="purple">object[]</span> `Sample value: --`

The information about the ESI orders that meet the conditions.


**AutoReleaseAt** <span data-label="purple">string</span> `Sample value: 2024-01-04T23:00:00+08:00`

The time when the instances are automatically released.



**Count** <span data-label="purple">integer</span> `Sample value: 3`

The number of instances.



**CreatedAt** <span data-label="purple">string</span> `Sample value: 2024-01-04T14:32:58+08:00`

The time when the ESI order is created.



**DeliveryCount** <span data-label="purple">integer</span> `Sample value: 3`

The number of delivered instances.



**DeliveryType** <span data-label="purple">string</span> `Sample value: Reserve`

Elastic Scheduled Instances\-Segmented delivery type.



**ElasticScheduledInstanceType** <span data-label="purple">string</span> `Sample value: Esi`

The type of the ESI instance.



**EndDeliveryAt** <span data-label="purple">string</span>` Sample value: 2024-01-04T14:50:00+08:00`

The end time for instance delivery.



**InstanceConfig** <span data-label="purple">object</span> `Sample value: --`

The instance configuration information in the ESI orders.


**HpcClusterId** <span data-label="purple">string</span> `Sample value: hpcCluster-ybo1y364wkf80o0m****`

The HPC cluster ID.



**Description** <span data-label="purple">string</span> `Sample value: ECS instance for testing`

The description of the instance.



**EipAddress** <span data-label="purple">object</span> `Sample value: --`

The information about the EIP associated with the instance.


**BandwidthMbps** <span data-label="purple">integer</span> `Sample value: 5`

The maximum bandwidth measured in Mbps for the EIP.


* Default value: 1

* Valid range:

   * When `ChargeType` is set to `PayByBandwidth`: 1–500.

   * When `ChargeType` is set to `PayByTraffic`: 1–200.



**BandwidthPackageId** <span data-label="purple">string</span> `Sample value: bwp-2zeo05qre24nhrqpy****`

ID of the Shared Bandwidth Package.



**ChargeType** <span data-label="purple">string</span> `Sample value: PayByBandwidth`

The metering method of Elastic IP address (EIP). Valid values:


* PayByBandwidth (default): Pay\-by\-bandwidth

* PayByTraffic: Pay\-by\-data\-transfer

* PrePaid: subscription



**ISP** <span data-label="purple">string</span> `Sample value: BGP`

The ISP type. Valid values:


* BGP (default): BGP (Multi\-ISP).

* If your account has applied for and enabled permission for the static single\-ISP, you can pass in the following values:

   * ChinaMobile: China Mobile static single\-ISP.

   * ChinaTelecom: China Telecom static single\-ISP.

   * ChinaUnicom: China Unicom static single\-ISP.

   * If your account has applied for and enabled permission for the BGP single\-ISP, you can pass in SingleLine_BGP.

   * If your account has applied for and enabled static BGP permission, you can pass in Static_BGP.



**ReleaseWithInstance** <span data-label="purple">boolean</span> `Sample value: true`

Whether the EIP is deleted along with the instance. This feature is only available for pay\-as\-you\-go EIPs. Valid values:


* true: The EIP is deleted along with the instance. When an instance is automatically reclaimed by the system (for example, 24 hours after unsubscription or upon expiration) or deleted via the [DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) or [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API, the EIP is released along with the instance.

* false: The EIP is not deleted when the instance is deleted.



**SecurityProtectionInstanceId** <span data-label="purple">string</span> `Sample value: 20`

The ID of the associated security package. This parameter is returned only when `SecurityProtectionTypes` is not empty.



**SecurityProtectionTypes** <span data-label="purple">string[]</span> `Sample value: AntiDDoS_Enhanced`

The security protection type of EIP.


* AntiDDoS_Enhanced: EIP of the Security Enhanced type, which can be added to an Anti\-DDoS Origin (Enterprise Edition) instance.

* Empty value: EIP of the basic protection type.




**HostName** <span data-label="purple">string</span> `Sample value: instance-host-name`

Instance hostname.



**ImageId** <span data-label="purple">string</span> `Sample value: image-yctfez5q0e5pkg0f****`

The image ID.



**InstanceName** <span data-label="purple">string</span> `Sample value: ECS-qJsO`

Instance name.



**InstanceTypeId** <span data-label="purple">string</span> `Sample value: ecs.c3i.xlarge`

Instance type.



**KeyPairName** <span data-label="purple">string</span> `Sample value: kp-test-123`

Name of the key pair.



**NetworkInterfacesRes** <span data-label="purple">object[]</span> `Sample value: --`

Information about the network interface mounted to the instance.


**SecurityGroupIds** <span data-label="purple">string[]</span> `Sample value: sg-12b0uab1j62gw17q7y38d****`

ID of the security group associated with the network interface.



**SubnetId** <span data-label="purple">string</span> `Sample value: subnet-2ff2xcgobksn459gp67cp****`

The subnet ID of the private network of the instance.




**ProjectName** <span data-label="purple">string</span> `Sample value: default`

The project to which the instances belong.



**Tags** <span data-label="purple">object[]</span> `Sample value: --`

The tag information of the instance.


**Key** <span data-label="purple">string</span> `Sample value: k1`

The tag key of the resource.



**Value** <span data-label="purple">string</span> `Sample value: v1`

The tag value of the resource.




**Volumes** <span data-label="purple">object[]</span> `Sample value: --`

Information about the volume mounted to the instance.


**Kind** <span data-label="purple">string</span> `Sample value: system`

The volume type. Valid values:


* system: system volume

* data: data volume



**Size** <span data-label="purple">integer</span> `Sample value: 2048`

The volume capacity. Unit: GiB.



**VolumeType** <span data-label="purple">string</span> `Sample value: ESSD_PL0`

The volume type. Valid values:


* ESSD_PL0: ESSD PL0

* ESSD_FlexPL: ESSD FlexPL




**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

The availability zone ID where the ESI order is located.




**InvalidAt** <span data-label="purple">string</span> `Sample value: --`

The time when the ESI order expires.



**ProjectName** <span data-label="purple">string</span> `Sample value: default`

The project to which the ESI order belongs.



**ReleaseCount** <span data-label="purple">integer</span> `Sample value: 0`

The number of released instances.



**ScheduledInstanceDescription** <span data-label="purple">string</span> `Sample value: ESI order for testing`

The description of the ESI order.



**ScheduledInstanceId** <span data-label="purple">string</span> `Sample value: esi-ycvye5a380l8j1ld****`

ESI order ID.



**ScheduledInstanceName** <span data-label="purple">string</span> `Sample value: ESI-Name`

The name of the ESI order.



**StartDeliveryAt** <span data-label="purple">string</span> `Sample value: 2024-01-04T14:40:00+08:00`

The start time for instance delivery.



**Status** <span data-label="purple">string</span> `Sample value: CREATING`

The ESI order status.



**Tags** <span data-label="purple">object[]</span> `Sample value: --`

The tag information of the ESI order.


**Key** <span data-label="purple">string</span> `Sample value: k1`

The tag key of the resource.



**Value** <span data-label="purple">string</span> `Sample value: v1`

The tag value of the resource.




**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2024-01-04T15:35:15+08:00`

The time when the ESI order is updated.



**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

The availability zone ID where the ESI order is located.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeScheduledInstances&Version=2020-04-01&ScheduledInstanceIds.1=esi-ycvye5a380l8j1ld****&ElasticScheduledInstanceType=Segmented&DeliveryType=Reserve HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240104180821CDEEFD683593D54D****",
    "Action": "DescribeScheduledInstances",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScheduledInstanceInfo": [
      {
        "CreatedAt": "2024-01-04T14:32:58+08:00",
        "UpdatedAt": "2024-01-04T15:35:15+08:00",
        "ScheduledInstanceId": "esi-ycvye5a380l8j1ld****",
        "ZoneId": "cn-beijing-a",
        "ScheduledInstanceDescription": "Flexible reservation form for testing",
        "Status": "DELIVERED",
        "ScheduledInstanceName": "ESI-Name",
        "StartDeliveryAt": "2024-01-04T14:40:00+08:00",
        "EndDeliveryAt": "2024-01-04T14:50:00+08:00",
        "Count": 3,
        "DeliveryCount": 3,
        "ReleaseCount": 0,
        "InvalidAt": "",
        "ElasticScheduledInstanceType": "Segmented",
        "AutoReleaseAt": "2024-01-04T23:00:00+08:00",
        "ProjectName": "default",
        "Tags": [],
        "InstanceConfig": {
          "ZoneId": "cn-beijing-a",
          "InstanceTypeId": "ecs.c3i.xlarge",
          "ImageId": "image-yctfez5q0e5pkg0f****",
          "InstanceName": "ECS-qJsO",
          "Description": "",
          "HpcClusterId": "",
          "Hostname": "instance-host-name",
          "KeyPairName": "kp-test-123",
          "ProjectName": "default",
          "Tags": [],
          "Volumes": [
            {
              "VolumeType": "ESSD_PL0",
              "Size": 40,
              "Kind": "system"
            }
          ],
          "NetworkInterfacesRes": [
            {
              "SubnetId": "subnet-2ff2xcgobksn459gp67cp****",
              "SecurityGroupIds": [
                "sg-12b0uab1j62gw17q7y38d****"
              ]
            }
          ],
          "EipAddress": {
            "AllocationId": "eip-2749d8a20h4hs7fap8taa****",
            "ISP": "BGP",
            "BandwidthMbps": 1,
            "ChargeType": "PayByTraffic",
            "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
            "ReleaseWithInstance": "true",
            "SecurityProtectionTypes": []
          }
        },
        "DeliveryType": "Reserve"
      }
    ],
    "NextToken": "bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The format of the key for the specified query tag is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified TagFilterValue is malformed. |The format of the specified tag value for query is invalid. |
|400 |LimitExceeded.MaximumInstanceTypeIds |You've reached the limit on the number of InstanceTypeIds that you can set. |The specified number of InstanceTypeIds exceeds the maximum limit. |
|400 |LimitExceeded.MaximumScheduledInstanceIds |The number of specified ScheduledInstanceIds exceeds the maximum limit. |The value specified for ScheduledInstanceIds exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterKeys |You've reached the limit on the number of TagFilterKeys that you can set. |The specified query tag key is out of range. |
|400 |LimitExceeded.MaximumTagFilterResults |You've reached the limit on the number of resources that you can describe by TagFilters. |The number of resources filtered by tag exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterValues |You've reached the limit on the number of TagFilterValues that you can set. |The specified query tag value exceeds the valid range. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The operation does not exist. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag key for filtering already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
