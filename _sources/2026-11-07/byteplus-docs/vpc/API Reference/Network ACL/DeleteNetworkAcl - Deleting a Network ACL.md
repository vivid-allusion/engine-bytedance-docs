---
title: "DeleteNetworkAcl - Deleting a Network ACL"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteNetworkAcl"
---

Call the DeleteNetworkAcl API to delete the Network Access Control List.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Network Access List is not associated with any subnets. You can call the [DescribeNetworkAcls](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls) API to check if it is associated. If it is associated, you can call the [DisassociateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/DisassociateNetworkAcl) API to disassociate.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteNetworkAcl&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|bwU6Q-">必选</span> `Example value: DeleteNetworkAcl`

The interface name. The current API name is `DeleteNetworkAcl`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|-VT-C3">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**NetworkAclId** <span data-label="purple">String</span> <span data-api-tag="require|iSDpeW">必选</span>`Example value: nacl-bp1fg655nh68xyz9****`

Network ACL ID.

You can call the [DescribeNetworkAcls](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls) API to query the Network Access Control List ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteNetworkAcl&Version=2020-04-01&NetworkAclId=acl-bp1fg655nh68xyz9**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteNetworkAcl",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidNetworkAcl.InUse |The specified Network ACL has dependent resource of a subnet. |The specified network ACL cannot be deleted because it is associated with subnets. |
|400 |InvalidNetworkAcl.InvalidStatus |The specified Network ACL is not in the correct status for the request. |The specified Network ACL is in a state that cannot respond to this request. |
|404 |InvalidNetworkAcl.NotFound |The specified Network ACL does not exist. |The specified Network Access Control List does not exist. |
