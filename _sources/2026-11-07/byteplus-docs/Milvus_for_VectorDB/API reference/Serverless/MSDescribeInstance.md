---
title: "MSDescribeInstance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/MSDescribeInstance"
---

Call MSDescribeInstance to query Serverless instance details.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=MSDescribeInstance&groupName=Serverless-%E5%85%AC%E5%BC%80&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ByA7Jw">必选</span> `Example value: MSDescribeInstance`

Operation to execute, value: MSDescribeInstance.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|xRgZBY">必选</span> ` Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|nq4v0Z">必选</span> `Example: s-dev-12345678`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Optional Example: milvus-serverless-instance`

Instance name.



**ProjectName ** <span data-label="purple">String </span>`Optional` `Example: default`

Project



**PageNumber ** <span data-label="purple">Integer </span>`Optional` `Example value: 1`

Page number, default is 1.



**PageSize ** <span data-label="purple">Integer </span>`Optional` `Example: 10`

Number of items displayed per page, default is 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple">string </span>`Example value: -`

Account ID.



**InstanceId ** <span data-label="purple">string </span>`Example value: -`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Example: -`

Instance name.



**InstanceVersion ** <span data-label="purple">string </span>`Example value: -`

Instance version



**Region ** <span data-label="purple">string </span>`Example value: -`

Affiliated region.



**ProjectName ** <span data-label="purple">string </span>`example value: -`

Project name.



**Status ** <span data-label="purple">string </span>`Example value: -`

Instance status.



**Username ** <span data-label="purple">string </span>`Example value: -`

Username.



**DatabaseName ** <span data-label="purple">string </span>`Example value: -`

Database name.



**CreateTime ** <span data-label="purple">string </span>`Example value: -`

Creation time.



**UpdateTime ** <span data-label="purple">string </span>`Example value: -`

Updated at.



**DeleteProtectEnabled ** <span data-label="purple">boolean </span>`Example value: -`

Turn on deletion protection or not.



**Tags ** <span data-label="purple">object[] </span>`Example: -`

List of tags.


**Key ** <span data-label="purple">string </span>`Example: -`

Tag key.



**Value ** <span data-label="purple">string </span>`Example: -`

Tag value.



**SystemTag ** <span data-label="purple">boolean </span>`Example value: -`

System tag.




**NetworkConfig ** <span data-label="purple">object </span>`example value: -`

Network configuration.


**VpcInfo ** <span data-label="purple">object </span>`Example value: -`

VPC information.


**VpcId ** <span data-label="purple">string </span>`Example value: -`

VPC ID.



**VpcName ** <span data-label="purple">string </span>`Example: -`

VPC name.




**SubnetInfo ** <span data-label="purple">object </span>`Example: -`

Subnet information.


**SubnetId ** <span data-label="purple">string </span>`Example: -`

Subnet ID.



**SubnetName ** <span data-label="purple">string </span>`Example value: -`

Subnet name.




**InnerEndpointEnabled ** <span data-label="purple">boolean </span>`example: -`

Whether to enable internal network access.



**HttpsEnabled ** <span data-label="purple">boolean </span>`example value: -`

Whether to turn on HTTPS.



**IpVersion ** <span data-label="purple">string </span>`Example value: -`

IP address version.




**ChargeConfig ** <span data-label="purple">object </span>`example: -`

Billing configuration.


**ChargeType ** <span data-label="purple">string </span>`Example: -`

Billing type.



**Period ** <span data-label="purple">integer </span>`Example value: -`

Billing cycle.



**AutoRenew** <span data-label="purple">boolean</span> `Example value: -`

Automatic renewal.



**ExpireDate ** <span data-label="purple">string </span>`Example value: -`

expiration date.




**EndpointList ** <span data-label="purple">object[] </span>`Example value: -`

List of access points.


**Type ** <span data-label="purple">string </span>`example value: -`

Type.



**Domain ** <span data-label="purple">string </span>`Example value: -`

Domain name.



**Ip ** <span data-label="purple">string </span>`example value: -`

IP address.



**PrivateDomainPublishEnabled ** <span data-label="purple">boolean </span>`Example value: -`

Whether to enable public network resolution for private domain names.



**AllowGroupList ** <span data-label="purple">object[] </span>`example value: -`

IP allowlist.


**GroupName ** <span data-label="purple">string </span>`Example: -`

IP allowlist name.



**List ** <span data-label="purple">string[] </span>`Example value: -`

IP allowlist.




**Eip ** <span data-label="purple">string </span>`Example value: -`

Public IP.



**EipId** <span data-label="purple">string</span> `Example value: -`

Public IP ID.



**AllowList ** <span data-label="purple">string[] </span>`example: -`

Whitelist list.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=MSDescribeInstance&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260316T070008Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260316/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "s-dev-12345678"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202603161500110060040232337C2E38",
    "Action": "MSDescribeInstance",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "AccountId": "FubYuNem",
    "InstanceId": "dkU1",
    "InstanceName": "WCIJca1Z3S",
    "InstanceVersion": "aDol",
    "Region": "uAhzd",
    "ProjectName": "bpybBzFb6Mo",
    "Status": "6S",
    "Username": "s0t7",
    "DatabaseName": "j8vG3",
    "CreateTime": "fxJMbXjva7m",
    "UpdateTime": "EQXWxw",
    "DeleteProtectEnabled": false,
    "Tags": [
      {
        "Key": "2je9",
        "Value": "GscxM8u",
        "SystemTag": false
      }
    ],
    "NetworkConfig": {
      "VpcInfo": {
        "VpcId": "82QhFma",
        "VpcName": "InKPw4"
      },
      "SubnetInfo": {
        "SubnetId": "BMxJ",
        "SubnetName": "X8v"
      },
      "InnerEndpointEnabled": true,
      "HttpsEnabled": false,
      "IpVersion": "B5JMQ"
    },
    "ChargeConfig": {
      "ChargeType": "sPZDEeb",
      "Period": 880,
      "AutoRenew": true,
      "ExpireDate": "Hg6me7j"
    },
    "EndpointList": [
      {
        "Type": "bNBgj8qK",
        "Domain": "0WBRLmSv",
        "Ip": "tV1T0r1ukj",
        "PrivateDomainPublishEnabled": true,
        "AllowGroupList": [
          {
            "GroupName": "wpEK5qfWM5d",
            "List": [
              "0GRT78"
            ]
          }
        ],
        "Eip": "lvQGfQ",
        "EipId": "xI0T74x3t",
        "AllowList": [
          "Rq"
        ]
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |AccountNoPermission |accountId have no permission |This account does not have permission. |
