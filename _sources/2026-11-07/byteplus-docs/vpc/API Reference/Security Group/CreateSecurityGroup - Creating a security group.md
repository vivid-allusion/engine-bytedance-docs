---
title: "CreateSecurityGroup - Creating a security group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateSecurityGroup"
---

Call the CreateSecurityGroup API to create a security group.

## Instructions

* The default maximum number of security groups (including the default security group) that can be created in a single account within a single region is 300. If the default quota cannot meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota.

* When creating a VPC, the system automatically creates a default security group named "Default".

* CreateSecurityGroup is an asynchronous API. When a request ID is returned, the system is still creating in the background. You can call [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) to check the status of the security group. `Creating` means it is being created, and `Available` means configuration is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateSecurityGroup&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateSecurityGroup`

Interface name. The current API name is `CreateSecurityGroup`.

**Version ** String必选 `Example: 2020-04-01`

Interface version. The current API version is `2020-04-01`.

**VpcId ** String必选 `Example: vpc-bp1opxu1zkhn00gzv****`

The ID of the VPC the security group belongs to.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**SecurityGroupName ** String`optional` `Example: testSecurityGroupName`

Name of the security group.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or digit. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, it defaults to the security group ID.

**Description ** String`optional` `Example: testDescription`

Description of the security group.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* If left blank, this defaults to an empty string.

**Type ** String`optional` `Example: -`

Security group type. Valid values:

* cidr_only: CIDR\-Only security group.

   * Such security groups are no longer restricted by IP address quotas and are suitable for business scenarios such as automatic resource expansion and large\-scale IP address usage.

   * Rules in such security groups do not support references to other security groups or prefix lists.

* If not specified, it defaults to a common security group.

**ProjectName ** String`optional` `Example: default`

Name of the project to which the security group belongs. If left blank, it defaults to the default project.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N specifies the serial number of a tag key. Valid values: 1–50.

* Separate multiple tag keys with ampersands ( & ).

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the custom tag.

* N specifies the serial number of a tag value. Valid values: 1–50.

* Separate multiple tag values with ampersands (&).

* The length ranges from 0 to 256 characters. If left blank, it defaults to an empty value.

* May include multilingual characters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.

> **tip**

> To provide this parameter, provide `Tags.N.Key` first.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**SecurityGroupId ** String`Example: sg-bp1fg655nh68xyz9****`

ID of the newly created security group.

## Request example

```json
GET /?Action=CreateSecurityGroup&Version=2020-04-01&VpcId=vpc-bp1ou1zkhn00gzv****&SecurityGroupName=SG_1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSecurityGroup",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "SecurityGroupId": "sg-bp1fg655nh68xyz9****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidBelongTo.Malformed |The specified BelongTo is malformed. |The specified BelongTo is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified ClientToken is invalid. It cannot be more than 64 ASCII characters. |
|400 |InvalidSecurityGroup.NotAuthorized |You are not authorized to operate invisible security group. |Hidden security groups cannot be operated without permissions. |
|400 |InvalidSecurityGroup.NotServicemanaged |The invisible security group is not service managed. |Hidden security groups must be managed by a service. |
|400 |InvalidSecurityGroupType.Malformed |The type of specified security group is invalid. |The specified type value is invalid. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot process this request. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |The maximum tags that you can operate in a single request have been reached. |
|400 |QuotaExceeded.SecurityGroup |Security group number exceeded quota. |The maximum number of security groups that can be created has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface created by recipient can not be service managed. |No permission to perform actions on the specified Elastic Network Interface (ENI). ENIs created by the sharee cannot be managed by the service. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
