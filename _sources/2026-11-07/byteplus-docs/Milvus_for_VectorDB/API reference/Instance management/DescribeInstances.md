---
title: "DescribeInstances"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DescribeInstances"
---

Call DescribeInstances to get the instance list.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstances&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|7KKgAb">必选</span>` Example value: DescribeInstances`

Operation to execute: DescribeInstances.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|YwxbQo">必选</span> `Example: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId ** <span data-label="purple">string </span>`optional` `Example value: instance-123456`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Optional` `Example value: my-milvus-instance`

Instance name.



**ProjectName ** <span data-label="purple">string </span>`optional` `Example value: ai-platform`

Project name.



**PageNumber ** <span data-label="purple">Integer </span>`Optional` `Example value: 1`

Page number of the instance information list.



**PageSize ** <span data-label="purple">Integer </span>`Optional` `Example value: 10`

Records per page: 10\-100.



**TagFilters ** <span data-label="purple">object[] </span>`optional` `Example value: []`

An array of tag key\-value pairs used for filtering queries.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|4m40q7">必选</span> `Example value: -`

Tag key.



**Values ** <span data-label="purple">string[] </span><span data-api-tag="require|RTrnaF">必选</span>`Example value: -`

Tag value.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceInfos ** <span data-label="purple">object[] </span>`Example value: []`

Instance information.


**InstanceId ** <span data-label="purple">string </span>`Example value: milvus-12345678`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Example: milvus-prod-01`

Instance name.



**InstanceVersion ** <span data-label="purple">string </span>`Example value: V2_5`

Milvus version.



**ProjectName ** <span data-label="purple">string </span>`Example value: ai-platform`

Project name.



**Region ** <span data-label="purple">string </span>`Example value: ap-beijing`

Region.



**Status ** <span data-label="purple">string </span>`Example value: Running`

Instance status.

Init: Initializing.

WaitingPaid: Awaiting payment.

WaitCreate: Pending creation.

Creating: Creating.

Running: Running.

Restarting: Restarting.

Updating: Updating.

WaitScale: Pending scaling.

Scaling: Scaling.

Restoring: Restoring.

Upgrading: Upgrading.

Closing: Closing.

Disabled

Restoring

WaitRelease

Releasing

Released

Creation failed

Error

Warning



**Zones ** <span data-label="purple">string[] </span>`Example value: -`

Availability zone list.



**NetworkConfig ** <span data-label="purple">object </span>`Example: -`

Network configuration.


**VpcInfo ** <span data-label="purple">object </span>`Example value: -`

Private network information.


**VpcId ** <span data-label="purple">string </span>`Example value: vpc-12345678`

Private network ID.



**VpcName ** <span data-label="purple">string </span>`Example value: milvus-vpc`

private network name.




**SubnetInfo ** <span data-label="purple">object </span>`Example value: -`

Subnet information.


**SubnetId ** <span data-label="purple">string </span>`Example value: subnet-12345678`

Subnet ID.



**Subnet name ** <span data-label="purple">string </span>`Example value: milvus-subnet`

Subnet name.





**ChargeConfig ** <span data-label="purple">object </span>`example: -`

Billing configuration.


**ChargeType ** <span data-label="purple">string </span>`Example: -`

Billing type.


* PostPaid: Pay\-as\-you\-go.

* PrePaid: Subscription.



**ExpireDate ** <span data-label="purple">string </span>`Example value: 2025-12-31 12:00:00`

Expiration time.




**DeleteProtectEnabled ** <span data-label="purple">boolean </span>`Example value: true`

Whether deletion protection is enabled.



**CreateTime ** <span data-label="purple">string </span>`Example value: 2023-01-15T10:30:00Z`

Creation time.



**Tags ** <span data-label="purple">object[] </span>`Example: -`

List of tags.


**Key ** <span data-label="purple">string </span>`Example: -`

Tag key.



**Value ** <span data-label="purple">string </span>`Example: -`

Tag value.





**Size ** <span data-label="purple">integer </span>`Example value: 2`

Number of items on the current page.



**Total ** <span data-label="purple">integer </span>`Example value: 10`

Total number of instances.



**PageNumber ** <span data-label="purple">integer </span>`Example value: 1`

Page number of the instance information list.



**PageSize ** <span data-label="purple">integer </span>`Example value: 10`

The number of records per page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeInstances&Version=2023-01-01 HTTP/1.1
Host: milvus.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251027T125939Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251027/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "instance-123456",
  "InstanceName": "my-milvus-instance",
  "ProjectName": "ai-platform",
  "PageNumber": 1,
  "PageSize": 10,
  "TagFilters": [
    {
      "Key": "LQT",
      "Values": [
        "daQ"
      ]
    }
  ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202510272059421341810312017ED5C8",
    "Action": "DescribeInstances",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "InstanceInfos": [
      {
        "InstanceId": "milvus-12345678",
        "InstanceName": "milvus-prod-01",
        "InstanceVersion": "V2_5",
        "ProjectName": "ai-platform",
        "Region": "ap-beijing",
        "Status": "Running",
        "Zones": [
          "Z"
        ],
        "NetworkConfig": {
          "VpcInfo": {
            "VpcId": "vpc-12345678",
            "VpcName": "milvus-vpc"
          },
          "SubnetInfo": {
            "SubnetId": "subnet-12345678",
            "SubnetName": "milvus-subnet"
          },
          "InnerEndpointEnabled": true
        },
        "ChargeConfig": {
          "ChargeType": "C4sHT6",
          "Period": 12,
          "AutoRenew": true,
          "ExpireDate": "2025-12-31 12:00:00"
        },
        "DeleteProtectEnabled": true,
        "CreateTime": "2023-01-15T10:30:00Z",
        "Tags": [
          {
            "Key": "9CKexeIUE3w",
            "Value": "6ReTL"
          }
        ]
      }
    ],
    "Size": 2,
    "Total": 10,
    "PageNumber": 1,
    "PageSize": 10
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |InternalServerError |InternalServerError |Internal server exception. |
