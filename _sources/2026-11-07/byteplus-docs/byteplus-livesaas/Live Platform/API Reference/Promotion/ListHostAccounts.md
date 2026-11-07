---
title: "ListHostAccounts"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts"
---

Gets information such as the ID, name, and avatar URL of host accounts under your account.

<span id="requirements"></span>
## Requirements


* Rate limit: 120 requests per minute per account

* Prerequisite: A BytePlus account or an IAM user with the Marketing toolkits \> View only or Edit permission. For more information, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://livesaas.byteplusapi.com/?Action=ListHostAccounts&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListHostAccounts` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |
|PageNo |Integer |No |`1` |The number of the page to return. Default value: `1`. The value must be greater than or equal to 1. |
|PageItemCount |Integer |No |`10` |The number of results to return on each page. Default value: `10`. Default value: [1,1000]. |
|HostAccountId |Integer |No |`2333` |The host account ID. |
|HostAccountName |String |No |`Host A` |The host account name. The value must be 1\-260 characters in length. Fuzzy search is supported.<br><br>The value is case\-insensitive. For example, if the parameter value is `A`, host accounts with names such as `Host A` and `host abc` are to be returned. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNo |Integer |`1` |The page number of the returned page. |
|PageItemCount |Integer |`10` |The number of results returned on each page. |
|TotalItemCount |Integer |`1` |The total number of returned host accounts. |
|HostAccounts |Array of [HostAccounts](https://docs.byteplus.com/en/docs/11/35113#hostaccounts) |`-` |The list of host account information. |
|GetFollowDataUrl |String |`https://example.com` |The query request URL, which is used to query whether a viewer is following the host. For more information, see [Integrating your system with BytePlus Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account#integrating-your-system-with-byteplus-live). |
|UpdateFollowDataUrl |String |`https://example.com` |The update request URL, which is used to update a viewer's following status for the host. For more information, see [Integrating your system with BytePlus Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account#integrating-your-system-with-byteplus-live). |


<span id="hostaccounts"></span>
### HostAccounts


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |Long |`2333` |The host account ID.<br><br>After getting the ID, you can call [UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) to update the information of the host account, [DeleteHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/deletehostaccount) to delete the host account, or [UpdateActivityHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount) to update the host account associated with a specific live room. |
|Name |String |`Host A` |The host account name. |
|AvatarUrl |String |`https://example.com/a.png` |The URL of the host account avatar. |
|HomeUrl |String |`https://example.com` |The homepage URL of the host account. |
|CreateTime |Integer |`1657525387` |The creation time of the host account in Unix timestamp format. Unit: seconds. |
|IsFollowEnable |Integer |`0` |Indicates whether viewers are allowed to follow the host on the viewing page. Valid values:<br><br><br>* `0`: Not allowed.<br><br>* `1`: Allowed. |
|ExternalPlatformId |String |`abc123` |The external platform ID, which can only contain uppercase and lowercase letters and numbers, and cannot exceed 128 characters in length. |
|ExtraInfo |String |`abc` |The extra information associated with the host account. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://livesaas.byteplusapi.com/?Action=ListHostAccounts&Version=2023-08-01&PageNo=1&PageItemCount=10&HostAccountId=2333&HostAccountName=Host A
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListHostAccounts",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1715326286
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "TotalItemCount": 1,
        "GetFollowDataUrl": "https://example.com",
        "UpdateFollowDataUrl": "https://example.com",
        "HostAccounts": [
            {
                "Id": 2333,
                "Name": "Host A",
                "AvatarUrl": "https://example.com/a.png",
                "HomeUrl": "https://example.com",
                "CreateTime": 1657525387,
                "IsFollowEnable": 0,
                "ExternalPlatformId": "abc123",
                "ExtraInfo": "abc"
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
