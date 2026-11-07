---
title: "DescribeInstanceDetail"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DescribeInstanceDetail"
---

Call DescribeInstanceDetail to get instance details.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstanceDetail&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string</span><span data-api-tag="require|9NoS7A">必选</span> ` Example value: DescribeInstanceDetail`

Operation to execute: DescribeInstanceDetail.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|EfD9vM">必选</span>` Example: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId**<span data-label="purple"> string</span><span data-api-tag="require|u1GDzI">必选</span>`  Example: milvus-xxx`

Instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**BaseInstance ** <span data-label="purple">object </span>`Example value: {}`

Basic instance configuration.


**InstanceId ** <span data-label="purple">string </span>`Example value: milvus-12345678`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Example: milvus-prod-01`

Instance name.



**InstanceVersion ** <span data-label="purple">string </span>`Example value: V2_5`

Instance version


* V2_5.

* V2_6.



**AccountId ** <span data-label="purple">string </span>`Example value: account-123`

Account ID.



**SubAccountId ** <span data-label="purple">string </span>`Example value: sub-account-456`

Sub\-account ID.



**Region ** <span data-label="purple">string </span>`Example value: ap-beijing`

Region.



**ProjectName ** <span data-label="purple">string </span>`Example value: ai-platform`

Project name.



**Status ** <span data-label="purple">string </span>`Example value: Running`

Instance status.


* Init: Initializing.

* WaitingPaid: Awaiting payment.

* WaitCreate: Pending creation.

* Creating: Creating.

* Running: Running.

* Restarting: Restarting.

* Updating: Updating.

* WaitScale: Pending scaling.

* Scaling: Scaling.

* Restoring: Restoring.

* Upgrading: Upgrading.

* Closing: Closing.

* Disabled

* Restoring

* WaitRelease

* Releasing

* Released

* Creation failed

* Error

* Warning




**NetworkConfig ** <span data-label="purple">object </span>`Example value: {}`

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





**ChargeConfig ** <span data-label="purple">object </span>`Example value: {}`

Billing configuration.


**ChargeType ** <span data-label="purple">string </span>`Example: -`

Billing type.


* PostPaid: Pay\-as\-you\-go.

* PrePaid: Subscription.



**ExpireDate ** <span data-label="purple">string </span>`Example value: 2025-12-31`

Expiration time.




**EndpointList ** <span data-label="purple">object[] </span>`Example value: []`

List of endpoints.


**Type ** <span data-label="purple">string </span>`example value: -`

Terminal type.


* MILVUS_PRIVATE: private network access point.

* MILVUS_PUBLIC: public network access point.



**Domain ** <span data-label="purple">string </span>`Example value: -`

Domain name.



**Ip ** <span data-label="purple">string </span>`example value: -`

IP address.



**PrivateDomainPublishEnabled ** <span data-label="purple">boolean </span>`Example value: -`

Whether to enable public network resolution for private domain names.



**AllowGroupList ** <span data-label="purple">object[] </span>`example value: -`

Allowlist group list.


**GroupName ** <span data-label="purple">string </span>`Example: -`

Whitelist group name.



**List ** <span data-label="purple">string[] </span>`Example value: -`

Whitelist list.




**Eip ** <span data-label="purple">string </span>`Example value: -`

Public IP.



**AllowList ** <span data-label="purple">string[] </span>`example: -`

Whitelist.



**EipId** <span data-label="purple">string</span> `Example value: -`

Public IP ID.




**SpecConfig ** <span data-label="purple">object[] </span>`Example value: []`

Specification configuration.


**ResourceSpecName ** <span data-label="purple">string </span>`Example value: -`

Specification name.



**SpecType ** <span data-label="purple">string </span>`Example value: -`

Specification type CU/GPU.



**DisplayName ** <span data-label="purple">string </span>`Example value: -`

Specification display name



**NodeType ** <span data-label="purple">string </span>`Example value: QUERY_NODE`

Node type.



**CpuNum ** <span data-label="purple">integer </span>`Example value: 4`

CPU core count.



**MemSize ** <span data-label="purple">integer </span>`Example value: 16`

Memory size.



**NodeNum ** <span data-label="purple">integer </span>`Example value: 2`

Number of nodes.




**DeleteProtectEnabled ** <span data-label="purple">boolean </span>`Example value: true`

Whether deletion protection is enabled.



**Zones ** <span data-label="purple">string[] </span>`Example value: []`

Availability zones.



**CreateTime ** <span data-label="purple">string </span>`Example value: 2023-01-15T10:30:00Z`

Creation time.



**Tags ** <span data-label="purple">object[] </span>`Example value: []`

List of tags.


**Key ** <span data-label="purple">string </span>`Example: environment`

Tag key.



**Value ** <span data-label="purple">string </span>`Example value: production`

Tag value.




**StorageUsage ** <span data-label="purple">string </span>`Example value: test`

Storage usage.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DescribeInstanceDetail&Version=2023-01-01 HTTP/1.1
Host: milvus.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251027T125910Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251027/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "jMV"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027205913113065195101B45469",
    "Action": "DescribeInstanceDetail",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "BaseInstance": {
      "Id": 12345,
      "InstanceId": "milvus-12345678",
      "InstanceName": "milvus-prod-01",
      "InstanceVersion": "V2_5",
      "AccountId": "account-123",
      "SubAccountId": "sub-account-456",
      "DeployClusterId": "cluster-789",
      "Namespace": "milvus-namespace",
      "Region": "ap-beijing",
      "ProjectName": "ai-platform",
      "TaskId": "task-987654",
      "Version": 1,
      "Status": "Running"
    },
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
      "ChargeType": "jcXDgxZ",
      "Period": 12,
      "AutoRenew": true,
      "ExpireDate": "2025-12-31"
    },
    "EndpointList": [
      {
        "Type": "uesATxa",
        "Domain": "837F",
        "Ip": "D60AKfRc",
        "PrivateDomainPublishEnabled": false,
        "AllowGroupList": [
          {
            "GroupName": "JzxfTU",
            "List": [
              "s"
            ]
          }
        ],
        "Eip": "bTWrt",
        "AllowList": [
          "NRvQ"
        ],
        "EipId": "k1oCu"
      }
    ],
    "SpecConfig": [
      {
        "NodeType": "QUERY_NODE",
        "CpuNum": 4,
        "MemSize": 16,
        "NodeNum": 2,
        "NodeCUType": "uTgdAge"
      }
    ],
    "DeleteProtectEnabled": true,
    "Zones": [
      "P"
    ],
    "EngineVersion": "2.0.0",
    "CreateTime": "2023-01-15T10:30:00Z",
    "Tags": [
      {
        "Key": "environment",
        "Value": "production"
      }
    ],
    "StorageUsage": "Tw",
    "HaEnabled": true
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |AccountNoPermission |accountId have no permission |This account does not have permission. |
|200 |InstanceIsReleased |InstanceIsReleased |The instance has been released. |
|200 |InstanceNotFound |InstanceNotFound |The specified instance does not exist. |
|200 |InternalServerError |InternalServerError |Internal server exception. |
|200 |BadRequestParameterEmpty |Parameter can not be empty. |The parameter cannot be empty. |
|200 |IllegalParameter |illegal parameter |Invalid parameter. |
