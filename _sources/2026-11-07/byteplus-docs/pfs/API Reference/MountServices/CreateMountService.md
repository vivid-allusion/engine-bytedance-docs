---
title: "CreateMountService"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/CreateMountService"
---

Call CreateMountService to create a mount service.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|MountServiceName |String |Yes |mountservice |Mount service name. The naming convention is as follows:<br><br><br>* Cannot start with a number, dash (\-) or underscore (_).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and dashes (\-).<br><br>* The length should be between 1 and 128 characters.<br><br>* The mount service name under each account in each region is unique and cannot be repeated. |
|ZoneId |String |Yes |ap\-southeast\-1a |You need to create the Availability Zone ID for the mount service.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call <a href="https://docs.byteplus.com/en/docs/pfs/DescribeZones">DescribeZones</a> to query the availability zone information under a region.</div><br> |
|VpcId |String |Yes |vpc\-13f24t16guqdc3n6nu4k5\*\*\*\* |The private network ID of the mounted service needs to be consistent with the private network ID of the subsequent mounted instance.<br><br><div data-tips="true" data-tips-type="tip">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> interface to query the private network ID.</div><br> |
|SubnetId |String |Yes |subnet\-rr96lovl7f28v0x58tv\*\*\*\* |Subnet ID.<br><br><div data-tips="true" data-tips-type="tip">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> interface to query all subnet IDs in the specified availability zone.</div><br> |
|NodeType |String |Yes |ecs.g2i.large |Client side management node type.<br><br>You can call the [DescribeMountServiceNodeTypes](https://docs.byteplus.com/en/docs/pfs/DescribeMountServiceNodeTypes) interface to query which node types are supported under an Availability Zone. |
|Project |String |No |testproject |Mount the item to which the service belongs. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|MountServiceId |String |mount\-75a6\*\*\*\* |The mount service ID created. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=CreateMountService&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "MountServiceName": "mountservice",
    "ZoneId": "ap-southeast-1a",
    "VpcId": "vpc-13f24t16guqdc3n6nu4k5****",
    "SubnetId": "subnet-rr96lovl7f28v0x58tv****",
    "NodeType": "ecs.g2i.large",
    "Project": "testproject"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateMountService",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "MountServiceId": "mount-75a6****"
    }
}
```
