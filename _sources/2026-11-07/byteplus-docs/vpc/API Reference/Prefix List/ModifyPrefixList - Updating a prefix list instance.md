---
title: "ModifyPrefixList - Updating a prefix list instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyPrefixList"
---

Call the ModifyPrefixList API to modify the prefix list.

## Instructions

ModifyPrefixList is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to check the prefix list status. `Pending` means configuring, and `Available` means modification is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyPrefixList&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: ModifyPrefixList`

The interface name. The current API name is `ModifyPrefixList`.

**Version ** String 必选`Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**PrefixListId ** String必选 `Example: pl-bp1fg655nh68xyz9****`

The ID of the prefix list to be modified.

You can call the [DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to query the Prefix List ID.

**PrefixListName ** String`optional` `Example: PrefixList-1`

Name of the prefix list.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example value: PrefixList_Common`

Description of the prefix list.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**MaxEntries ** Integer`optional` `Example value: 100`

The maximum number of entries allowed for the prefix list.

* If the prefix list has no associated resources, the maximum number of entries cannot exceed 200.

* If the prefix list has associated resources, the maximum number of entries is not only limited to 200 but is also subject to the quota limits of the associated resources.

> **tip**

> Prefix list's maximum entry count consumes associated resource quota. Modifying the maximum number of entries may prevent resources that are intended to be associated with the prefix list from establishing an association. Please thoroughly evaluate the potential impact on your services and proceed with caution.

**AddPrefixListEntries.N.Cidr ** String`optional` `Example: 1.XX.XX.0/24`

The CIDR block to add as a new prefix list entry.

* Parameter \- N: represents the serial number of a prefix list entry. Valid range: 1 to `MaxEntries`, and N must be sequential and in ascending order.

* Separate multiple CIDRs with ampersands ( & ).

> **tip**

> If the CIDR block to be added already exists, only the value of `AddPrefixListEntries.N.Description` will be updated (i.e., only the description of that CIDR block will be modified).

**AddPrefixListEntries.N.Description ** String`optional` `Example: CIDR_A`

The description for the new prefix list entry to be added.

* Parameter \- N: represents the serial number of a prefix list entry. Valid range: 1 to `MaxEntries`, and N must be sequential and in ascending order.

* Separate multiple descriptions with ampersands (&).

* Must be 0 to 255 characters.

* If left blank, this parameter defaults to an empty string.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**RemovePrefixListEntries.N.Cidr ** String`optional` `Example: 192.168.0.0/16`

The prefix list entry to be deleted.

* Parameter \- N: represents the serial number of a prefix list entry. Valid range: 1 to `MaxEntries`, and N must be sequential and in ascending order.

* Separate multiple CIDR with ampersands (&).

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.

* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.

**DryRun ** Boolean `optional` `Example: false`

Whether to only precheck the request

Type the enumerated values strictly in the case form as follows. Do not set other values.

* true: Sends a dry\-run request; the prefix list will not be modified. Checks include: Whether required parameters are entered, request format, and service limits. If the check fails, the corresponding error is returned. If the check passes, the error code `DryRunOperation` is returned.

* false (default): Sends a normal request. After passing the check, an HTTP 2xx status code is returned and the Prefix List is modified.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`optional` `Example: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=ModifyPrefixList&Version=2020-04-01&PrefixListId=pl-bp1fg655nh68xyz9****&AddPrefixListEntries.1.Cidr=1.XX.XX.0/24&AddPrefixListEntries.2.Cidr=2.XX.XX.0/24 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyPrefixList",
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

|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidCidr.ProtocolMismatch |The specified cidr block mismatch the protocol type. |The specified CIDR block format does not match the protocol type. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidMaxEntries.Malformed |The maximum number of entries is malformed. |The format of the maximum number of entries is incorrect. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.CidrCountExceedMaxCount |The number of CIDR blocks exceeded the maximum number of entries allowed. |The number of CIDR blocks exceeds the maximum entry limit of the prefix list. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidPrefixList.InvalidStatus |The specified prefix list is not in the correct status for the request. |The specified prefix list is in a state that cannot respond to this request. |
|400 |InvalidPrefixListEntry.Conflict |The specified CIDR block conflicts with another one in the specified prefix list. |Duplicate CIDR blocks exist in the specified prefix list entries. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified security group is not in the correct status for the request. |The specified security group is in a state that cannot respond to this request. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |LimitExceeded.MaxEntries |You've reached the limit on the number of MaxEntries per prefix list that you can assign. |The maximum number of CIDR block entries supported by the prefix list has been reached. |
|400 |QuotaExceeded.RouteEntry |Route entry of a route table number exceeded quota. |The maximum number of route entries that you can create has been reached. |
|400 |QuotaExceeded.SecurityGroupRule |You've reached the limit on the number of egress security rules that you can create. |The quota for the maximum number of outbound rules that can be created for the security group has been reached. |
|400 |QuotaExceeded.SecurityGroupRule |You've reached the limit on the number of ingress security rules that you can create. |The quota for the maximum number of inbound rules that can be created for the security group has been reached. |
|400 |QuotaExceeded.Vpc |VPC number exceeded quota. |Reached the maximum VPCs that you can create. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified Prefix List does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in your route table. |The specified CIDR block conflicts with another rule's CIDR block in the associated route table. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
