---
title: "DescribeReservedInstances - Queries Reserved Instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeReservedInstances"
---

Call the DescribeReservedInstances operation to query information about Reserved Instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

When you call this operation, the number of Reserved Instances queried using `TagFilters.N.Key` and `TagFilters.N.Values.N` must not exceed 1,000. If the number of instances to be queried exceeds 1,000, call the [DesribeTags](https://docs.byteplus.com/en/docs/ecs/DescribeTags) operation.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeReservedInstances&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|tHBpPH">必选</span> `Sample value: DescribeReservedInstances`

The operation that you want to perform. Valid value: DescribeReservedInstances.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|9nIfrN">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**HpcClusterId** <span data-label="purple">string</span> `Optional` `Sample value: hpcCluster-1`

HPC Cluster ID.



**InstanceTypeFamilies.N** <span data-label="purple">string[]</span> `Optional` `Sample value: InstanceTypeFamilies.1=ecs.g3i`

The instance type family that you want to use to filter Reserved Instances. You can specify up to 100 instance type families.


* Parameter \- N: This specifies the serial number of the instance type family.

* Separate multiple instance type families with &.



**InstanceTypeIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: InstanceTypeIds.1=ecs.g3i.2xlarge`

The type that you want to use to filter Reserved Instances. You can specify up to 100 types.


* Parameter \- N: This specifies the serial number of the instance type.

* Use & to separate multiple types.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 20`

The number of rows per page when you set up a pagination query.


* Maximum value: 100

* Default value: 10



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: project_a`

The associated project. Each instance can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**ReservedInstanceIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: ReservedInstanceIds.1=ecsri-ycsimi9g465pkfxc****`

The ID of the Reserved Instance. You can specify up to 100 IDs.


* Parameter \-N: Specifies the serial number of the Reserved Instance.

* Multiple IDs are divided with ampersands (&).



**ReservedInstanceName** <span data-label="purple">string</span> `Optional` `Sample value: reserved-instance-test`

The name of the Reserved Instance. Fuzzy search is supported.



**Scope** <span data-label="purple">string</span> `Optional` `Sample value: ZonalRI`

RI type. Value:


* ZonalRI (default): zonal RI

* RegionalRI: regional RI. Regional RI is currently in Beta. If you need a trial, contact the account manager to apply.



**Status** <span data-label="purple">string</span> `Optional` `Sample value: CREATING`

The status of the Reserved Instance. Valid values:


* CREATING: The instance is being created.

* ACTIVE: In effect

* EXPIRED: Expired

* UPDATING: Being changed (The attributes of the Reserved Instance are being changed.)



**SupportModify** <span data-label="purple">string</span> `Optional` `Sample value: SizeSupport`

The change type supported by the Reserved Instance. Valid values:


* NotSupport: No changes are supported.

* SizeSupport: The instance type can be changed but the availability zone cannot be changed.



**TagFilters.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Key=k1`

The tag key of the user tag.


* Parameter \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with "&". Duplicate tag keys are not allowed.



**TagFilters.N.Values.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The tag value of the user tag.


* The first N: specifies the serial number of the tag key. Value range: 1–10.

* The second N: specifies the serial number of the tag key. Value range: 1–3. You can query up to three tag values of the same tag key.

* Separate multiple key values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, you need to pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in the TagFilters.N.Key parameter, all tag values corresponding to the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The ID of the availability zone specified in RI.

You can call [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken** <span data-label="purple">string</span> `Sample value: eWNsYTg0b2s1Y3Yyd3Jzb2do****`

The query credentials value returned by this call. If null is returned, this page is the last page.



**ReservedInstances** <span data-label="purple">object[]</span> `Sample value: --`

The information of the Reserved Instances that meet the conditions.


**CreatedAt** <span data-label="purple">string</span> `Sample value: 2023-06-28T18:29:38+08:00`

The time when the Reserved Instance is created.



**Description** <span data-label="purple">string</span> `Sample value: testDescription`

The description of the Reserved Instance.



**ExpiredAt** <span data-label="purple">string</span> `Sample value: 2023-07-28T18:29:38+08:00`

The time when the Reserved Instance expires.



**HpcClusterId** <span data-label="purple">string</span> `Sample value: hpcCluster-1`

HPC Cluster ID.



**InstanceCount** <span data-label="purple">integer</span> `Sample value: 10`

The number of matching pay\-as\-you\-go instances.



**InstanceTypeId** <span data-label="purple">string</span> `Sample value: ecs.g3i.xlarge`

The instance type matched by the instance.



**OfferingType** <span data-label="purple">string</span> `Sample value: All Upfront`

The payment type of the Reserved Instance. Valid values:

All Upfront: Full prepayment.



**ProjectName** <span data-label="purple">string</span> `Sample value: project_a`

The project to which the resource belongs.



**RegionId** <span data-label="purple">string</span> `Sample value: cn-beijing`

The ID of the region specified in RI.



**ReservedInstanceId** <span data-label="purple">string</span> `Sample value: ecsri-ycsimi9g465pkfxc****`

ID of RI.



**ReservedInstanceName** <span data-label="purple">string</span> `Sample value: reserved-instance-test`

The name of the Reserved Instance.



**Scope** <span data-label="purple">string</span> `Sample value: ZonalRI`

The type of the Reserved Instance.



**StartAt** <span data-label="purple">string</span> `Sample value: 2023-06-28T18:29:38+08:00`

The time when the Reserved Instance takes effect.



**Status** <span data-label="purple">string</span> `Sample value: ACTIVE`

The status of the Reserved Instance.



**SupportModify** <span data-label="purple">string</span> `Sample value: SizeSupport`

The change type supported by the Reserved Instance.



**Tags** <span data-label="purple">object[]</span> `Sample value: --`

The information of tags associated with resources.


**Key** <span data-label="purple">string</span> `Sample value: k1`

The tag key of the resource.



**Value** <span data-label="purple">string</span> `Sample value: v1`

Tag value of a resource.




**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

The ID of the availability zone where the Reserved Instance is located.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeReservedInstances&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202311201528596749BD5A57E146F0****",
    "Action": "DescribeReservedInstances",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "ReservedInstances": [
      {
        "CreatedAt": "2023-06-28T18:29:38+08:00",
        "ExpiredAt": "2023-07-28T18:29:38+08:00",
        "InstanceCount": 10,
        "InstanceTypeId": "ecs.g3i.xlarge",
        "ReservedInstanceId": "ecsri-ycsimi9g465pkfxc****",
        "ReservedInstanceName": "reserved-instance-test",
        "Description": "testDescription",
        "Status": "ACTIVE",
        "ZoneId": "cn-beijing-a",
        "SupportModify": "SizeSupport",
        "OfferingType": "AllUpfront",
        "Tags": [
          {
            "Key": "k1",
            "Value": "v1"
          }
        ],
        "HpcClusterId": "",
        "ProjectName": "default",
        "Scope": "ZonalRI",
        "RegionId": "cn-beijing-a",
        "StartAt": "2023-06-28T18:29:38+08:00"
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
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The format of the specified tag key for query is invalid.​ ​​ |
|400 |InvalidTagFilterValue.Malformed |The specified TagFilterValue is malformed. |The format of the specified tag value for query is invalid. |
|400 |LimitExceeded.MaximumInstanceTypeFamilies |You've reached the limit on the number of InstanceTypeFamilies that you can set. |The specified number of InstanceTypeFamilies exceeds the maximum limit. |
|400 |LimitExceeded.MaximumInstanceTypeIds |You've reached the limit on the number of InstanceTypeIds that you can set. |The specified number of InstanceTypeIds exceeds the maximum limit. |
|400 |LimitExceeded.MaximumMaxResults |The number of specified MaxResults exceeds the maximum limit. |The value specified for MaxResults exceeds the upper limit. |
|400 |LimitExceeded.MaximumReservedInstanceIds |The number of specified ReservedInstanceIds exceeds the maximum limit. |The value specified for ReservedInstanceIds exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterKeys |You've reached the limit on the number of TagFilterKeys that you can set. |The specified query tag key is out of range. |
|400 |LimitExceeded.MaximumTagFilterResults |You've reached the limit on the number of resources that you can describe by TagFilters. |The number of resources filtered by tag exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterValues |You've reached the limit on the number of TagFilterValues that you can set. |The specified query tag value exceeds the valid range. |
|400 |LimitExceeded.MinimumMaxResults |The number of specified MaxResults exceeds the minimum limit. |The value specified for MaxResults exceeds the lower limit. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
