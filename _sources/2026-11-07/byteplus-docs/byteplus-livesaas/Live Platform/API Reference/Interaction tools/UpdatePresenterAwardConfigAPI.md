---
title: "UpdatePresenterAwardConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateAwardConfig"
---

Call `UpdatePresenterAwardConfigAPI` to add, update, or delete a real\-time lucky draw for a live room.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When updating a lucky draw, you must pass values for all customized parameters to prevent them from being reset to their defaults.</div>


<span id="Requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisite: A BytePlus account or an IAM user with **Live control** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=UpdatePresenterAwardConfigAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdatePresenterAwardConfigAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="Body parameters"></span>
### Body parameters


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|AccountId |Long |Yes |3000\*\*\*\* |Your account ID, which can be found on the [My Account](https://console.byteplus.com/user/basics/) page. |
|Id |Long |Yes |`36576` |Real\-time lucky draw ID. The value varies as follows:<br><br><br>* To create a real\-time lucky draw, pass in `0`.<br><br>* To update or delete the lucky draw configuration, pass in the lucky draw ID. You can obtain the ID through the [ListAwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs) API. |
|Name |String |No |Lucky draw event |Lucky draw name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when creating or updating a real\-time lucky draw.</div><br> |
|AwardType |Integer |No |1 |Draw method. The values are as follows:<br><br><br>* `1`: Automatic draw<br><br>* `2`: Manual draw<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when creating or updating a lucky draw.</div><br> |
|DeadLine |Long |No |30 |The duration of the lucky draw countdown, in minutes. The default value is `0`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is only valid when the value of <code>AwardType</code> is <code>1</code>.</div><br> |
|BarragePwd |String |No |Danmaku password |Lucky draw bullet comment password. The default value is empty. |
|WinnerInfoType |String |No |1 |Personal information that the winner needs to provide. Supported values include:<br><br><br>* 1: Shipping address<br><br>* 2: Phone number<br><br>* 3: Recipient name |
|AwardNum |Integer |No |1000 |The number of prizes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when creating or updating a real\-time lucky draw.</div><br> |
|RangeStatus |Integer |No |0 |Lucky draw rules. The default value is `0`. The values are as follows:<br><br><br>* `0`: All viewers have the same probability of winning.<br><br>* `1`: Viewers who have not won are given priority. |
|ShowPeopleNumber |Integer |No |0 |Whether to display the actual number of participants in the lucky draw on the viewing page. The default value is `0`. The values are as follows:<br><br><br>* `0`: Display<br><br>* `1`: Do not display |
|Status |Integer |Yes |`1` |Specifies the operation to perform on the real\-time lucky draw. The values are as follows:<br><br><br>* `1`: Create or update a real\-time lucky draw<br><br>* `5`: Delete a real\-time lucky draw |
|AwardCondition |Object of [AwardCondition](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig#awardcondition) |No |*  |Conditions for participating in the lucky draw. |
|ShowWinnerComment |Integer |No |0 |Whether to display the details of the winners. The default value is `0`. The values are as follows:<br><br><br>* `0`: Do not display<br><br>* `1`: Display |
|AwardId |Long |No |1621615169 |Prize ID. Obtain the ID by calling [GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist?lang=en).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when creating or updating a real\-time lucky draw.</div><br> |


<span id="awardcondition"></span>
### AwardCondition


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Quiz |String |No |all |Sets the Q&A participation requirement for users to be eligible for the lucky draw. If this parameter is not set (default), the condition is disabled.<br><br><br>* `"all"`: The user must have answered **all** questions sent during the livestream before the lucky draw.<br><br>* `1`\-`999`: The user must have submitted **at least** this number of answers to be eligible. For example, a value of `3` requires the user to have answered a minimum of three questions. |
|RightQuiz |String |No |`1` |The minimum number of questions the user must answer correctly. |
|Questionnaire |String |No |1 |The minimum number of questionnaires the user must submit. |
|CheckIn |String |No |all |The minimum number of check\-ins the user must complete. |
|Vote |String |No |1 |The minimum number of votes the user must submit. |


<span id="awarditemconfigs"></span>
### Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Status |Boolean |`true` |Returns `true` if the configuration was updated successfully. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdatePresenterAwardConfigAPI&Version=2023-08-01
{
    "ActivityId": 172183461234****,
    "AccountId": 3000****,
    "Id": 0,
    "Status": 1,
    "Name": "Prize A",
    "AwardType": 1,
    "DeadLine": 1,
    "AwardId": 1001,
    "AwardNum": 100,
    "RangeStatus": 1,
    "WinnerInfoType": "1",
    "AwardCondition": {
        "CheckIn": "1"
    }
}
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdatePresenterAwardConfigAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
