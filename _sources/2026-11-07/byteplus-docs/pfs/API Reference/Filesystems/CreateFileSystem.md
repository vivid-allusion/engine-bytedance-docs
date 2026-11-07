---
title: "CreateFileSystem"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/CreateFileSystem"
---

Call the CreateFileSystem interface to create a file system.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|FileSystemName |String |Yes |test |File system name. The naming convention is as follows:<br><br><br>* Cannot start with numbers, dashes (\-) and underscores (_).<br><br>* Can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>   The length should be between 1 and 128 characters. |
|ZoneId |String |Yes |ap\-southeast\-1a |Availability zone ID. |
|ChargeType |String |Yes |PayAsYouGo |Billing type. The value selection description is as follows:<br><br>`PayAsYouGo`: Billed by volume. |
|FileSystemType |String |Yes |VePFS |File system type, defaults to `VePFS`. |
|StoreType |String |Yes |Advance_100 |File system specification, value selection description is as follows:<br><br>Advance_100: 100MB/s/TiB |
|ProtocolType |String |Yes |VePFS |Protocol type, defaults to`VePFS` |
|Description |String |No |Just\-for\-test |File system description information. |
|Project |String |No |default |The project to which the file system belongs, defaults to`default`. |
|Capacity |Integer |No |100 |File system capacity in TiB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a description of capacity limitations for different specifications, please refer to <a href="https://docs.byteplus.com/en/docs/pfs/Product-specifications">Product Specifications</a>.</div><br> |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/92/25010#tag) |No |See the request example for details |Label information to be added.<br><br><div data-tips="true" data-tips-type="tip">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The label information of the file system needs to meet certain rules. For details, please refer to <a href="https://docs.byteplus.com/en/docs/pfs/Binding-or-adding-tags">Tag Setup Rules</a>.</div><br> |
|VpcId |String |No |vpc\-rs5811nceqyov0x58x4\*\*\*\* |Private network ID.<br><br><div data-tips="true" data-tips-type="tip">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> interface to query the private network ID.</div><br> |
|SubnetId |String |No |subnet\-1g15j13jtzgu88ibuxwqp\*\*\*\* |Subnet ID. The subnet must belong to the selected Availability Zone.<br><br><div data-tips="true" data-tips-type="tip">Tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A subnet is a block of IP addresses within a private network. All cloud resources in a private network must be deployed within a subnet. The subnet is a cloud quota private network IP address. You can call the <a href="https://docs.byteplus.com/en/docs/vpc/CreateSubnet">CreateSubnet</a> interface to create a subnet.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> interface to query all subnet list information in the specified availability zone, including subnet IDs.</div><br> |


<span id="tag"></span>
### Tag


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |tag_00 |Label key. |
|Type |String |Yes |Custom |The label type is described as follows:<br><br><br>* `Custom`: user\-defined labels.<br><br>* `System`: System label. |
|Value |String |Yes |tag_value00 |Label value. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|FileSystemId |String |vepfs\-apse1dfff3e96\*\*\*\* |File system ID. |
|OrderNO |String |Order705488740677732\*\*\*\* |Order ID. |
|Tags |Array of [TagResponse](https://docs.byteplus.com/en/docs/92/25010#tagresponse) |See the return example for details |The label information of the file system is returned when adding labels while creating the file system. |


<span id="tagresponse"></span>
### TagResponse


|Name |Type |Example |Description |
|---|---|---|---|
|Key |String |tag_00 |Label key. |
|Type |String |Custom |The label type is described as follows:<br><br><br>* `Custom`: user\-defined labels.<br><br>* `System`: System label. |
|Value |String |tag_value00 |Label value. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=CreateFileSystem&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "FileSystemName": "test",
    "ZoneId": "ap-southeast-1a",
    "ChargeType": "PayAsYouGo",
    "FileSystemType": "VePFS",
    "StoreType": "Advance_100",
    "ProtocolType": "VePFS",
    "Description": "Just-for-test",
    "Project": "default",
    "Capacity": 100,
    "Tags": [
        {
            "Key": "tag_00",
            "Type": "Custom",
            "Value": "tag_value00"
        }
    ],
    "VpcId": "vpc-rs5811nceqyov0x58x4****",
    "SubnetId": "subnet-1g15j13jtzgu88ibuxwqp****"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateFileSystem",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "FileSystemId": "vepfs-apse1dfff3e96****",
        "OrderNO": "Order705488740677732****",
        "Tags": [
            {
                "Key": "tag_00",
                "Type": "Custom",
                "Value": "tag_value00"
            }
        ]
    }
}
```
