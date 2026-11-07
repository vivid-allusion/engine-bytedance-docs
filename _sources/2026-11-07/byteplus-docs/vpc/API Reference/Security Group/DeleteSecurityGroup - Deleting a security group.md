---
title: "DeleteSecurityGroup - Deleting a security group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteSecurityGroup"
---

Call the DeleteSecurityGroup API to delete the specified security group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Security groups associated with ENIs cannot be deleted.

   You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to check for ENI associations. If associated, you can disassociate them by calling the [ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaceAttributes) API.

* Security groups referenced as a source in other security group rules cannot be deleted.

   You can call the [DescribeSecurityGroupAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroupAttributes) API to check if the security group is referenced by other rules. If it is, you can remove these references by calling the [RevokeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupIngress) and [RevokeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupEgress) APIs.

* Default security groups and managed security groups cannot be deleted. [Learn more](https://docs.byteplus.com/en/docs/vpc/Security-group-overview)


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteSecurityGroup&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|s490DO">必选</span> `Example value: DeleteSecurityGroup`

The interface name. The current API name is `DeleteSecurityGroup`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|sZDbF-">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**SecurityGroupId ** <span data-label="purple"> String  </span><span data-api-tag="require|xpTFNY">必选</span> `Example value: sg-bp1fg655nh68xyz9****`

Security group ID.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query the security group ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteSecurityGroup&Version=2020-04-01&SecurityGroupId=sg-bp1fg655nh68xyz9**** HTTP/1.1
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
        "Action": "DeleteSecurityGroup",
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
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidSecurityGroup.InUse |The specified security group has dependent resource of a security rule. |The specified security group cannot be deleted as it is referenced by other rules. |
|400 |InvalidSecurityGroup.InUse |The specified security group has dependent resource of an ENI. |The specified security group cannot be deleted as it is bound to ENIs. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified security group is not in the correct status for the request. |The specified security group is in a state that cannot respond to the request. |
|400 |InvalidSecurityRule.InvalidStatus |The specified security rule is not in the correct status for the request. |The specified security group rule in a state that cannot respond to this request. |
|403 |Forbidden |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |No sufficient permissions to perform this operation on the specified security group. The specified security group is managed by the cloud product. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
