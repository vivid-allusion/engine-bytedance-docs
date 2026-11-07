---
title: "ListAwardConfigsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardConfigs"
---

Call `ListAwardConfigsAPI` to obtain the configuration details of lucky draws.

<span id="Requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisite: A BytePlus account or an IAM user with **Live control** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListAwardConfigsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListAwardConfigsAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|All |Integer |Yes |1 |Specifies whether to query all real\-time lucky draw configurations in the live room. The default value is `0`. Valid values are as follows:<br><br><br>* `0`: Query only the sent lucky draw configurations<br><br>* `1`: Query all lucky draw configurations in the live room |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AwardConfigs |Array of [AwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs#awardconfigs) |`-` |List of real\-time lucky draw configuration information. |


<span id="awardconfigs"></span>
### AwardConfigs


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |Long |`36576` |Real\-time lucky draw ID. |
|ActivityId |Long |17218346\*\*\*\* |Live room ID. |
|Name |String |Lucky draw |Lucky draw name. |
|AwardType |Integer |1 |Draw method. The values are as follows:<br><br><br>* `1`: Automatic draw<br><br>* `2`: Manual draw |
|DeadLine |Long |`1` |The number of minutes remaining in the lucky draw countdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when the value of <code>AwardType</code> is <code>1</code>.</div><br> |
|BarragePwd |String |comment |Lucky draw barrage comment password. |
|Status |Integer |`4` |Lucky draw status. Valid values are as follows:<br><br><br>* `1`: Not sent<br><br>* `2`: In progress<br><br>* `4`: Completed<br><br>* `5`: Deleted<br><br>* `7`: Withdrawn<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To retrieve information about unsent lucky draws, set the <code>All</code> parameter to <code>1</code>.</div><br> |
|WinnerCount |Integer |1 |The number of winners for the current prize. |
|ParticipantCount |Integer |`5` |Number of participants. |
|SendTime |Integer |`1673199096` |The time the lucky draw was sent, as a Unix timestamp measured in seconds. |
|OpenAwardTime |Integer |`1673199158` |The time the lucky draw results were announced, as a Unix timestamp measured in seconds. |
|AwardNum |Integer |`1` |Total number of prizes. |
|RangeStatus |Integer |0 |Lucky draw rules. The values are as follows:<br><br><br>* `0`: All viewers have the same probability of winning.<br><br>* `1`: Viewers who have not won are given priority. |
|ShowPeopleNumber |Integer |0 |Whether to display the actual number of participants in the lucky draw on the viewing page. The values are as follows:<br><br><br>* `0`: Display<br><br>* `1`: Do not display |
|MsgIds |String |`155681` |The ID of the image and text message for the lucky draw sent through the console. |
|AwardCondition |Object of [AwardCondition](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs#awardcondition) |`-` |Conditions for participating in the lucky draw |
|ShowWinnerComment |Integer |`0` |Whether to display the lucky draw winner details.<br><br><br>* `0`: Do not display<br><br>* `1`: Display |
|AwardItemInfo |Array of [AwardItemInfo](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs#awarditeminfo) |`-` |Prize information. |


<span id="awardcondition"></span>
### AwardCondition


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Quiz |String |all |Sets the Q&A participation requirement for users to be eligible for the lucky draw. If this parameter is not set (default), the condition is disabled.<br><br><br>* `"all"`: The user must have answered **all** questions sent during the livestream before the lucky draw.<br><br>* `1`\-`999`: The user must have submitted **at least** this number of answers to be eligible. For example, a value of `3` requires the user to have answered a minimum of three questions. |
|RightQuiz |String |1 |The minimum number of questions the user must answer correctly. If this parameter is not set (default), the condition is disabled.<br><br><br>* `"all"`: The user must have answered **all** questions correctly sent during the livestream before the lucky draw.<br><br>* `1`\-`999`: The user must have correctly answered **at least** this number of questions to be eligible. For example, a value of `3` requires the user to have answered a minimum of three questions. |
|Questionnaire |String |1 |The minimum number of questionnaires the user must submit. If this parameter is not set (default), the condition is disabled.<br><br><br>* `"all"`: The user must have submitted **all** questionnaires sent during the livestream before the lucky draw.<br><br>* `1`\-`999`: The user must have submitted **at least** this number of questionnaires to be eligible. For example, a value of `3` requires the user to have submitted a minimum of three questionnaires. |
|CheckIn |String |all |The minimum number of check\-ins the user must complete. If this parameter is not set (default), the condition is disabled.<br><br><br>* `"all"`: The user must have completed **all** check\-ins sent during the livestream before the lucky draw.<br><br>* `1`\-`999`: The user must have completed **at least** this number of check\-ins to be eligible. For example, a value of `3` requires the user to have completed a minimum of three check\-ins. |
|Vote |String |1 |The minimum number of votes the user must submit. If this parameter is not set (default), the condition is disabled.<br><br><br>* `"all"`: The user must have submitted **all** votes sent during the livestream before the lucky draw.<br><br>* `1`\-`999`: The user must have submitted **at least** this number of votes to be eligible. For example, a value of `3` requires the user to have submitted a minimum of three votes. |


<span id="awarditeminfo"></span>
### AwardItemInfo


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AwardItemId |Long |`908` |Prize ID. |
|AwardItemName |String |Prize coupon |Prize name. |
|AwardItemCount |Long |`1000` |Number of prizes. |
|AwardItemType |Integer |`4` |Prize type. Valid values are as follows:<br><br><br>* `1`: Physical prize<br><br>* `2`: Virtual prize<br><br>* `3`: Custom prize<br><br>* `4`: Voucher prize |
|AwardItemIcon |String |`//p.org/04ae0f42a3a04e7387e5f6fe7a18c4fb~tplv-6ed59yyum2-image.image` |The URL of the prize icon, without the protocol. |
|AwardItemNum |String |48151841 |Batch number for points prizes. The length ranges from 1 to 256 characters. You can use this batch number to identify company points and distribute them to viewers. |
|AwardItemAmounts |Long |1 |Number of points each winning viewer receives. The value range is [0,99999]. |
|AwardLotteryTicketAddr |String |https://example.com |Claim URL for voucher prizes. The length ranges from 1 to 256 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and applies only when <code>AwardItemType</code> is set to 4.</div><br> |
|WinnerInfoType |String |[1,2,3] |Information types that winners of physical or virtual prizes need to provide. Values:<br><br><br>* `1`: Shipping address<br><br>* `2`: Phone number<br><br>* `3`: Recipient name |
|WinnerCount |Long |1 |The number of winners for the current prize. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAwardConfigsAPI&Version=2023-08-01&ActivityId=17218346****&All=1
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAwardConfigsAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "AwardConfigs": [
            {
                "Name": "Lucky draw",
                "AwardType": 1,
                "DeadLine": 1,
                "BarragePwd": "comment",
                "Status": 4,
                "ActivityId": 17218346****,
                "SendTime": 1673199096,
                "OpenAwardTime": 1673199158,
                "RangeStatus": 0,
                "ShowPeopleNumber": 0,
                "MsgIds": "155681",
                "AwardCondition": {
                    "Quiz": "all",
                    "RightQuiz": "1",
                    "Questionnaire": "1",
                    "CheckIn": "all",
                    "Vote": "1"
                },
                "Id": 36576,
                "WinnerCount": 1,
                "ParticipantCount": 5,
                "ShowWinnerComment": 0,
                "AwardItemInfo": [
                    {
                        "AwardItemId": 908,
                        "AwardItemName": "Prize coupon",
                        "AwardItemCount": 1000,
                        "AwardItemType": 4,
                        "WinnerCount": 1,
                        "AwardItemIcon": "//p.org/04ae0f42a3a04e7387e5f6fe7a18c4fb~tplv-6ed59yyum2-image.image",
                        "AwardLotteryTicketAddr": "https://example.com",
                        "WinnerInfoType": "[1,2,3]",
                        "AwardItemNum": "48151841",
                        "AwardItemAmounts": 1
                    }
                ],
                "AwardNum": 1,
                "AwardSendTime": 1726734970,
                "AwardSendType": 1
            }
        ]
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
