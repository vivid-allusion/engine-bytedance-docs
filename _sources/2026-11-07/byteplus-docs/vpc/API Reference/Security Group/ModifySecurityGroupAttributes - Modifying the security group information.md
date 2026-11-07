---
title: "ModifySecurityGroupAttributes - Modifying the security group information"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupAttributes"
---

Call the ModifySecurityGroupAttributes API to change the name and description of security group.

## Instructions

Following optional parameters retain their existing configurations if not explicitly specified.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifySecurityGroupAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: ModifySecurityGroupAttributes`

The interface name. The current API name is `ModifySecurityGroupAttributes`.

**Version ** String必选 `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**SecurityGroupId** String 必选`Example value: sg-bp67acfmxazb4p****`

Security group ID.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query the security group ID.

**SecurityGroupName ** String`Optional` `Example value: sg-1`

The name of the security group.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example value: sg_1`

Description of the security group.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId** String `optional` `Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=ModifySecurityGroupAttribute&Version=2020-04-01&SecurityGroupId=sg-bp67acfmxazb4p****&SecurityGroupName=sg-1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifySecurityGroupAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified security group is not in the correct status for the request. |The specified security group is in a state that cannot respond to the request. |
|403 |Forbidden |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |No sufficient permissions to perform this operation on the specified security group. The specified security group is managed by the cloud product. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
