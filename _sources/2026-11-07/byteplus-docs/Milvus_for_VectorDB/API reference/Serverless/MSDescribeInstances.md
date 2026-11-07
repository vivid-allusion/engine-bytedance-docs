---
title: "MSDescribeInstances"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/MSDescribeInstances"
---

Call MSDescribeInstances to view the Serverless instance list.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=MSDescribeInstances&groupName=Serverless&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|4dSaPg">必选</span> `example: MSDescribeInstances`

Operation to execute: MSDescribeInstances.



**Version**<span data-label="purple"> string </span><span data-api-tag="require|odN0TJ">必选</span>` Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**PageNumber ** <span data-label="purple">Integer </span>`Optional` `Example value: 1`

Page number, default is 1.



**InstanceId ** <span data-label="purple">string </span>`Optional` `Example value: s-dev-12345678`

Instance ID.



**PageSize ** <span data-label="purple">Integer </span>`Optional` `Example: 10`

Number of items displayed per page, default is 10.



**InstanceName ** <span data-label="purple">string </span>`optional` `example: milvus-serverless-instance`

Instance name.



**ProjectName ** <span data-label="purple">String </span>`Optional` `Example: default`

Project



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Instances ** <span data-label="purple">object[] </span>`Example value: -`

Instance list.


**CreateTime ** <span data-label="purple">string </span>`Example value: -`

Creation time.



**InstanceId ** <span data-label="purple">string </span>`Example value: -`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Example value: -`

Instance name.



**MilvusVersion ** <span data-label="purple">string </span>`Example value: -`

Milvus version.



**ProjectName ** <span data-label="purple">string </span>`example value: -`

Project name.



**RegionId ** <span data-label="purple">string </span>`Example value: -`

Region ID.



**Status ** <span data-label="purple">string </span>`Example value: -`

Instance status.



**NetworkConfig ** <span data-label="purple">object </span>`Example: -`

Network configuration.


**VpcInfo ** <span data-label="purple">object </span>`Example value: -`

VPC information.


**VpcId ** <span data-label="purple">string </span>`Example value: -`

VPC ID.



**VpcName ** <span data-label="purple">string </span>`example: -`

VPC name.




**SubnetInfo ** <span data-label="purple">object </span>`Example value: -`

Subnet information.


**SubnetId ** <span data-label="purple">string </span>`Example value: -`

Subnet ID.



**SubnetName ** <span data-label="purple">string </span>`Example value: -`

Subnet name.




**InnerEndpointEnabled ** <span data-label="purple">boolean </span>`Example: -`

Enable internal network address.



**HttpsEnabled ** <span data-label="purple">boolean </span>`example: -`

Whether to turn on HTTPS.



**IpVersion ** <span data-label="purple">string </span>`Example value: -`

IP address version.




**ChargeConfig ** <span data-label="purple">object </span>`Example value: -`

Billing configuration.


**ChargeType ** <span data-label="purple">string </span>`Example value: -`

Charge type.



**Period ** <span data-label="purple">integer </span>`Example value: -`

Subscription duration.



**AutoRenew ** <span data-label="purple">boolean </span>`Example: -`

Whether to enable the automatic renewal function.



**ExpireDate ** <span data-label="purple">string </span>`Example value: -`

Expiration time.




**DeleteProtect ** <span data-label="purple">boolean </span>`Example value: -`

Turn on deletion protection or not.




**InstanceInfos ** <span data-label="purple">object[] </span>`Example value: -`

Instance list information.


**AccountId ** <span data-label="purple">string </span>`Example value: -`

Account ID.



**InstanceId ** <span data-label="purple">string </span>`Example value: -`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Example: -`

Instance name.



**InstanceVersion ** <span data-label="purple">string </span>`Example: -`

Instance version



**ProjectName ** <span data-label="purple">string </span>`example value: -`

Project name.



**Region ** <span data-label="purple">string </span>`Example value: -`

Affiliated region.



**Status ** <span data-label="purple">string </span>`Example value: -`

Instance status.



**NetworkConfig ** <span data-label="purple">object </span>`Example value: -`

Network configuration.


**VpcInfo ** <span data-label="purple">object </span>`Example value: -`

VPC information.


**VpcId ** <span data-label="purple">string </span>`example: -`

VPC ID.



**VpcName ** <span data-label="purple">string </span>`Example value: -`

VPC name.




**SubnetInfo ** <span data-label="purple">object </span>`Example value: -`

Subnet information.


**SubnetId ** <span data-label="purple">string </span>`Example value: -`

Subnet ID.



**SubnetName ** <span data-label="purple">string </span>`example: -`

Subnet name.




**InnerEndpointEnabled ** <span data-label="purple">boolean </span>`Example value: -`

Enable internal network address.



**HttpsEnabled ** <span data-label="purple">boolean </span>`Example value: -`

Whether HTTPS is enabled.



**IpVersion ** <span data-label="purple">string </span>`Example value: -`

IP address version.




**ChargeConfig ** <span data-label="purple">object </span>`example: -`

Billing configuration.


**ChargeType ** <span data-label="purple">string </span>`Example: -`

Billing type.



**Period ** <span data-label="purple">integer </span>`Example value: -`

Billing cycle.



**AutoRenew ** <span data-label="purple">boolean </span>`Example value: -`

Whether to enable the automatic renewal function.



**ExpireDate ** <span data-label="purple">string </span>`example: -`

Expiration time.




**DeleteProtectEnabled ** <span data-label="purple">boolean </span>`Example value: -`

Turn on deletion protection or not.



**CreateTime ** <span data-label="purple">string </span>`Example value: -`

Creation time.



**UpdateTime ** <span data-label="purple">string </span>`Example value: -`

Updated at.




**CurrentPage ** <span data-label="purple">long </span>`Example: -`

Current page.



**Size ** <span data-label="purple">integer </span>`Example value: -`

Number of instances on the current page.



**TotalPages ** <span data-label="purple">long </span>`example value: -`

Total pages.



**Total ** <span data-label="purple">long </span>`example: -`

Total number of instances.



**PageNumber ** <span data-label="purple">integer </span>`example: -`

Current page number.



**TotalSize ** <span data-label="purple">long </span>`example value: -`

Total count.



**PageSize ** <span data-label="purple">integer </span>`example: -`

Number of instances per page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=MSDescribeInstances&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260316T065912Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260316/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "202603161459160020141091614A1682",
    "Action": "MSDescribeInstances",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "Instances": [
      {
        "CreateTime": "zW4KH",
        "InstanceId": "JrIfTT3IEW",
        "InstanceName": "wEQrC",
        "MilvusVersion": "pXFQRaNTEdG",
        "ProjectName": "gC",
        "RegionId": "qmrFRsVVhlC",
        "Status": "tr8yI",
        "NetworkConfig": {
          "VpcInfo": {
            "VpcId": "XhCF90q",
            "VpcName": "9I1K"
          },
          "SubnetInfo": {
            "SubnetId": "WD4",
            "SubnetName": "UG"
          },
          "InnerEndpointEnabled": false,
          "HttpsEnabled": true,
          "IpVersion": "PATbSw"
        },
        "ChargeConfig": {
          "ChargeType": "bdOSTRe",
          "Period": 54,
          "AutoRenew": false,
          "ExpireDate": "7HYYj"
        },
        "DeleteProtect": false
      }
    ],
    "InstanceInfos": [
      {
        "AccountId": "ulrULea",
        "InstanceId": "t5lUT9b",
        "InstanceName": "X6LGW24w",
        "InstanceVersion": "rWcA",
        "ProjectName": "xb0kM2",
        "Region": "DzEZSdS",
        "Status": "ZlL9fqjEWM",
        "NetworkConfig": {
          "VpcInfo": {
            "VpcId": "kzxzE",
            "VpcName": "7LOMYEXl"
          },
          "SubnetInfo": {
            "SubnetId": "dkm4",
            "SubnetName": "Z6Xwx1"
          },
          "InnerEndpointEnabled": false,
          "HttpsEnabled": true,
          "IpVersion": "DlQS6zG"
        },
        "ChargeConfig": {
          "ChargeType": "viJ9JsI",
          "Period": 44,
          "AutoRenew": true,
          "ExpireDate": "LEMnHnyj"
        },
        "DeleteProtectEnabled": false,
        "CreateTime": "j3TTb",
        "UpdateTime": "Lnd0ETfm5bV"
      }
    ],
    "CurrentPage": 392,
    "Size": 809,
    "TotalPages": 607,
    "Total": 437,
    "PageNumber": 252,
    "TotalSize": 385,
    "PageSize": 865
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
