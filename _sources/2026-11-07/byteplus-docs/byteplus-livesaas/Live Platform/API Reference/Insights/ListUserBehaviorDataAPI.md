---
title: "ListUserBehaviorDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listuserbehaviordataapi"
---

Gets viewer behavior data for a live room. You can query data from the past 90 days.

<span id="3ae19eb3"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="f60263b8"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=ListUserBehaviorDataAPI&Version=2020-06-01`

* Method: GET


<span id="e0042409"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="2e36fb97"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListUserBehaviorDataAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218346****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNo |Integer |No |`1` |The number of the page to return.<br><br>Default value: `1`.<br><br>For a scrolling search, the value of `PageNo` can range from 1 to 2^64. For non\-scrolling searches, the API can return a maximum of 10,000 results; therefore, the product of `PageNo` and `PageItemCount` must not exceed 10,000. For more information about the scrolling search, see the query parameter `ScrollId`. |
|PageItemCount |Integer |No |`10` |The number of results to return on each page.<br><br>Default value: `10`.<br><br>Value range: [1,500]. |
|ScrollId |String |No |`klTVnVZdFk3bWg4YVQwdwAAAAAASn****xybkZ1el` |The scroll ID.<br><br>A scrolling search is applicable for scenarios with more than 10,000 results to return. To perform a scrolling search, make sure that you meet the following requirements.<br><br><br>* Keep the parameter value of `ScrollId` empty for the first API call. For the second API call, set the parameter value to the value of `ScrollId` returned in the first API call. For the third API call, set the parameter value to the value of `ScrollId` returned in the second API call, and so on.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the value of <code>IsMerge</code> or <code>IsMergeUserId</code> is set to <code>1</code>, the value of <code>ScrollId</code> must always be empty for a scrolling search.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of <code>ScrollId</code> in the response will become invalid 20 minutes after the API call, and then you cannot use the value for the next scrolling search.   </div><br>   <br><br>* Set the parameter value of `PageNo` to `1` for the first API call, set the value to `2` for the second API call, and so on.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of <code>PageNo</code> must be sequentially incremented and cannot be duplicated.   </div><br>   <br><br>* Keep the values of `IsMerge` and `IsMergeUserId` unchanged. |
|Name |String |No |`Viewer A` |The nickname. Returns behavior data for viewers whose nicknames contain this value. |
|StartTime |Long |No |`1642070520` |The start time in Unix timestamp format. Behavior data for viewers who entered the live room at or after this time is to be returned. Unit: seconds. |
|EndTime |Long |No |`1642070920` |The end time in Unix timestamp format. Behavior data for viewers who left the live room at or before this time is to be returned. Unit: seconds. |
|IsMerge |Integer |No |`0` |Specifies whether to merge behavior data for viewers who enter and leave the live room multiple times using the same device, based on device IDs.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Does not merge data.<br><br>* `1`: Merges data.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If viewers can watch previews, live videos, and playbacks without logging in to the live room, we recommend that you merge data in this way to get more accurate data.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>IsMerge</code> and <code>IsMergeUserId</code> cannot be set to <code>1</code> at the same time.</div><br> |
|Source |Integer |No |`0` |Data from this source is to be returned.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `-1`: Data from all addresses is to be returned.<br><br>* `0`: Data from the default address is to be returned.<br><br>* `1`: Data from address A is to be returned.<br><br>* `2`: Data from address B is to be returned.<br><br>* `3`: Data from address C is to be returned.<br><br>* `4`: Data from address D is to be returned. |
|PlayStatus |Integer |No |`1` |Specifies the statistics dimension. Default value: `10`.<br><br>Valid values:<br><br><br>* `1`: Returns data for viewers who watched live videos.<br><br>* `2`: Returns data for viewers who watched previews.<br><br>* `3`: Returns data for viewers who watched playbacks.<br><br>* `10`: Returns data for viewers who visited the viewing page.<br><br>* `11`: Returns data for viewers who watched live videos, previews, and playbacks. |
|IsMergeUserId |Integer |No |`0` |Specifies whether to merge behavior data for viewers who enter and leave the live room multiple times, based on user ID.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Does not merge data.<br><br>* `1`: Merges data.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If viewers must log in to the live room before watching previews, live videos, and playbacks, we recommend that you merge data in this way to get more accurate data.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>IsMerge</code> and <code>IsMergeUserId</code> cannot be set to <code>1</code> at the same time.</div><br> |
|Extra |String |No |`Marketing Department` |An additional parameter synchronized to BytePlus Live, which can be used to associate with the viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live. |


<span id="924e5e72"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|TotalItemCount |Integer |`1` |The total number of returned results. |
|Data |Array of [UserBehaviorData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi#d456d258) |`-` |Detailed behavior data of viewers. |
|ScrollId |String |`IN1ZTTzdZN3J3AAAAAAA****WTFdZalFSaGt` |The scroll ID. |


<span id="d456d258"></span>
### UserBehaviorData


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|UserId |Long |`172741906088****` |The unique identifier in BytePlus Live of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer does not log in to the live room by entering the nickname or by other methods, the user ID of the viewer is 0.</div><br> |
|UserName |String |`Viewer A` |The nickname of the viewer. |
|Region |String |`Singapore` |The region of the viewer. |
|IP |String |`4.**.**.89` |The IP address of the viewer. If behavior data is merged by setting the value of `IsMerge` or `IsMergeUserId` to `1` in the request, the value of this parameter may contain multiple IP addresses separated by spaces. |
|JoinAt |Array of Integer |`1714653969` |The time when the viewer entered the live room in Unix timestamp format. Unit: seconds. |
|leaveAt |Array of Integer |`1714668359` |The time when the viewer left the live room in Unix timestamp format. Unit: seconds. |
|WatchTime |Integer |`239` |The watch time of the viewer. Unit: minutes. |
|UserTel |String |`1560000****` |The phone number of the viewer. |
|InviteCode |String |`2711****` |The invitation code used by the viewer. |
|AccessTime |String |`playing before` |Indicates when the viewer entered the live room relative to the live stream.<br><br>Valid values:<br><br><br>* `playing`: During the live stream.<br><br>* `playing before`: Before the live stream starts.<br><br>* `playing post`: After the live stream ends. |
|UserDevice |Array of String |`Windows 10` |The device type used by the viewer. |
|Extra |String |`Marketing Department` |An additional parameter synchronized to BytePlus Live, which can be used to associate with the viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live. |
|ExternalUserId |String |`403343425511****` |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
|SilenceStatus |Integer |`1` |Indicates whether the viewer is muted.<br><br><br>* `1`: Muted.<br><br>* Other values: Not muted. |
|CommentCounts |Integer |`5` |The number of comments sent by the viewer. |


<span id="735d1510"></span>
## Samples

<span id="d820d185"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListUserBehaviorDataAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageItemCount=10&ScrollId=klTVnVZdFk3bWg4YVQwdwAAAAAASn****xybkZ1el&Source=0&IsMerge=0&IsMergeUserId=0
```


<span id="5eba56c8"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "ListUserBehaviorDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714673762
    },
    "Result": {
        "TotalItemCount": 1,
        "Data": [
            {
                "UserName": "Viewer A",
                "Region": "Singapore",
                "IP": "4.**.**.89",
                "JoinAt": [
                    1714653969
                ],
                "leaveAt": [
                    1714668359
                ],
                "UserId": 172741906088****,
                "UserTel": "-",
                "InviteCode": "-",
                "WatchTime": 239,
                "CommentCounts": 5,
                "AccessTime": "playing before",
                "Extra": "",
                "UserDevice": [
                    "Windows 10"
                ],
                "ExternalUserId": "",
                "SilenceStatus": 1
            }
        ],
        "ScrollId": "IN1ZTTzdZN3J3AAAAAAA****WTFdZalFSaGt"
    }
}
 
```


<span id="UserBehaviorData"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
