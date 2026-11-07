---
title: "DeletePrefixList - Deleting a prefix list instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeletePrefixList"
---

Call the DeletePrefixList API to delete the prefix list.

## Instructions

* The prefix list is not referenced by VPC security group rules. If referenced, first [Delete security group rule](https://docs.byteplus.com/en/docs/vpc/Managing_a_security_group_rule).

* The prefix list is not referenced by VPC route entries. If referenced, first [Delete route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).

* The prefix list is not referenced by TR static routing. If referenced, first [Delete static routing](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05).

* The prefix list is not referenced by TR route policy. If already referenced, first [Delete route policy entry](https://docs.byteplus.com/en/docs/transitrouter/Managing-the-routing-policy-entries).

* DeletePrefixList is an asynchronous API. When a request ID is returned, the system is still deleting in the background. You can call [DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to check the prefix list status. `Deleting` indicates it is being deleted, and a failed query indicates deletion is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeletePrefixList&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DeletePrefixList`

The interface name. The current API name is `DeletePrefixList`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.

**PrefixListId ** String必选 `Example: pl-bp1fg655nh68xyz9****`

The ID of the prefix list to be deleted.

You can call the [DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to query the Prefix List ID.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.

* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.

**DryRun ** Boolean`optional` `Example: false`

Whether to only precheck the request

Type the enumerated values strictly in the case form as follows. Do not set other values.

* true: Sends a dry\-run request; the prefix list will not be deleted. Checks include: Whether required parameters are entered, request format, and service limits. If the check fails, the corresponding error is returned. If the check passes, the error code `DryRunOperation` is returned.

* false (default): Sends a normal request. After passing the check, an HTTP 2xx status code is returned and the Prefix List is deleted.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```json
GET /?Action=DeletePrefixList&Version=2020-04-01&PrefixListId=pl-bp1fg655nh68xyz9**** HTTP/1.1 
Host: vpc.cn-beijing.byteplusapi.com.cn 
X-Date: 20250804T033538Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeletePrefixList",
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

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidPrefixList.InUse |The specified prefix list is in use, and can't be deleted. |The specified prefix list is in use and cannot be deleted. |
|400 |InvalidPrefixList.InvalidStatus |The specified prefix list is not in the correct status for the request. |The specified prefix list is in a state that cannot respond to this request. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified Prefix List does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
