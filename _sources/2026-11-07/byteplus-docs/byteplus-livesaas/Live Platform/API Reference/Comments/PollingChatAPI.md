---
title: "PollingChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-pollingchatapi"
---

Call this API to get comments in a live room. By specifying a comment ID and a polling direction, you can periodically retrieve new comments or load historical chat messages.

<span id="bae63780"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="35ca73aa"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=PollingChatAPI&Version=2020-06-01`

* Method: GET


<span id="f3f5b32b"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="ca18801e"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`PollingChatAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218346****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|ChatId |Long |Yes |`0` |The ID of a comment, which serves as a cursor for pagination. The API returns comments sent before or after this ID, but does not include the comment with this ID.<br><br><br>* If the value is `0`, the API returns comments posted before the request time.<br><br>* If you set this to a `ChatId` value from a previous response, the API retrieves comments sent before or after that specific comment, depending on the `PollingType` value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also set this parameter to <code>1</code> and set <code>PollingType</code> to <code>0</code> to retrieve the earliest comment sent in the current live room.</div><br> |
|Count |Integer |No |`0` |The maximum number of comments to return.<br><br>Default value: `0`.<br><br>If the value is `0`, the API returns all comments that match the conditions based on `ChatId` and `PollingType`. |
|PollingType |Integer |No |`0` |Specifies whether to return comments sent before or after the comment specified by `ChatId`.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Returns comments sent after the specified `ChatId`.<br><br>* `1`: Returns comments sent before the specified `ChatId`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>ChatId</code> is <code>0</code>, this parameter is ignored, and the API returns comments posted before the request time.</div><br> |


<span id="34e67e49"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Array of [Chat](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi#d762709f) |`-` |List of comments. |


<span id="d762709f"></span>
### Chat


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ChatId |Integer |`1672920235409489` |The comment ID. |
|CreateTime |Long |`1714658888` |The time when the comment was sent in Unix timestamp format. Unit: seconds. |
|TextContent |String |`Hello` |The content of the comment. |
|User |Array of [User](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi#60fb2ff7) |`-` |Information about the user who sent the comment. |
|IsDelete |Boolean |`false` |Indicates whether the comment was deleted.<br><br><br>* `true`: Deleted.<br><br>* `false`: Not deleted. |
|LikeCount |Integer |`10` |The number of likes for the comment. |
|IsPresenter |Boolean |`true` |Indicates whether the comment was sent by the host.<br><br><br>* `true`: Sent by the host.<br><br>* `false`: Sent by others. |
|reviewStatus |Integer |`0` |The review status of the comment.<br><br><br>* `0`: Review not required.<br><br>* `1`: Under review.<br><br>* `2`: Approved.<br><br>* `3`: Rejected.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter value is always <code>2</code> if the value of <code>IsPresenter</code> is <code>true</code>.</div><br> |
|IsTipOff |Integer |`0` |Indicates whether the comment was reported.<br><br><br>* `0`: Not reported.<br><br>* `1`: Reported. |


<span id="60fb2ff7"></span>
#### User


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|UserId |Long |`17975829****` |The ID of the user.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The ID of the host is always <code>0</code>.</div><br> |
|Nickname |String |`Viewer A` |The nickname of the user. |


<span id="90d4a741"></span>
## Samples

<span id="c9d65ee4"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=PollingChatAPI&Version=2020-06-01&ActivityId=17218346****&ChatId=0&Count=0&PollingType=0
```


<span id="Response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "PollingChatAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714662740
    },
    "Result": {
        "Data": [
            {
                "ChatId": 1672920235409489,
                "CreateTime": 1714658888,
                "TextContent": "Hello",
                "User": {
                    "Nickname": "Viewer A",
                    "UserId": 17975829****
                },
                "IsDelete": false,
                "LikeCount": 10,
                "IsPresenter": false,
                "reviewStatus": 0,
                "IsTipOff": 0
            },
            {
                "ChatId": 1672920235409492,
                "CreateTime": 1714660078,
                "TextContent": "Hello",
                "User": {
                    "Nickname": "Host",
                    "UserId": 0
                },
                "IsDelete": false,
                "LikeCount": 0,
                "IsPresenter": true,
                "reviewStatus": 2,
                "IsTipOff": 0
            }
        ]
    }
}
```


<span id="f9940149"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
