---
title: "AssociateNetworkAcl - Network ACL associated resources"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AssociateNetworkAcl"
---

Call the AssociateNetworkAcl API to associate a subnet with a Network Access Control List.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssociateNetworkAcl&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|QWYECg">必选</span> `Example value: AssociateNetworkAcl`

The interface name. The current API name is `AssociateNetworkAcl`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|dpFzng">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**NetworkAclId ** <span data-label="purple"> String  </span><span data-api-tag="require|WWTe7v">必选</span> `Example value: nacl-bp1fg655nh68xyz9****`

Network Access Control List ID.

You can call the [DescribeNetworkAcls](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls) API to query the Network Access Control List ID.



**Resource.N.ResourceId ** <span data-label="purple"> String  </span>`optional` `Example value: subnet-67acfmxazb4p****`

ID of the subnet to be associated.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.


* Parameter \- N: represents the serial number of the subnet ID, value range: 1 to 100.

* Separate multiple IDs with ampersands (&).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=AssociateNetworkAcl&Version=2020-04-01&NetworkAclId=nacl-bp1fg655nh68xyz9****&Resource.1.ResourceId=subnet-67acfmxazb4p****&Resource.2.ResourceId=subnet-g655nh68xyz9**** HTTP/1.1
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
        "Action": "AssociateNetworkAcl",
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
|400 |InvalidNetworkAcl.InvalidStatus |The specified Network ACL is not in the correct status for the request. |The specified network ACL in a state that cannot respond to this request. |
|400 |InvalidResource.Associated |The specified resource has been associated. |The specified resource is already associated with the network ACL. |
|400 |InvalidResource.Disorder |The specified resource index orders are malformed. |The serial number of the specified resource entry is invalid. |
|400 |InvalidResource.VpcMismatch |The specified resource is not under the same vpc as the Network ACL. |The specified resource does not belong to the same VPC as the network ACL. |
|400 |InvalidSubnet.InvalidStatus |The specified subnet is not in the correct status for the request. |The specified subnet is in a state that cannot process this request. |
|400 |LimitExceeded.ResourceId |You've reached the limit on the number of resources that you can operate one time. |The maximum number of resources that can be associated in a single operation has been reached. |
|404 |InvalidNetworkAcl.NotFound |The specified Network ACL does not exist. |The specified network ACL does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
