---
title: "ListUserBehaviorDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listuserbehaviordataapi-zh-CN"
---

获取直播间观众行为数据。可查询过去 90 天的数据。

<span id="3ae19eb3"></span>
## 要求

配额：每个账号每分钟最多 120 次查询

<span id="f60263b8"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=ListUserBehaviorDataAPI&Version=2020-06-01`

* 方法：GET


<span id="e0042409"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="2e36fb97"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`ListUserBehaviorDataAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218346****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|PageNo |Integer |否 |`1` |返回的页码。<br><br>默认值：`1`。<br><br>对于滚动查询，`PageNo` 的取值范围为 1 到 2^64。非滚动查询时，API 最多返回 10,000 条结果，因此 `PageNo` 与 `PageItemCount` 的乘积不得超过 10,000。有关滚动查询的更多信息，请参见查询参数 `ScrollId`。 |
|PageItemCount |Integer |否 |`10` |每页返回的结果数量。<br><br>默认值：`10`。<br><br>取值范围：[1,500]。 |
|ScrollId |String |否 |`klTVnVZdFk3bWg4YVQwdwAAAAAASn****xybkZ1el` |滚动查询 ID。<br><br>滚动查询适用于需返回超过 10,000 条结果的场景。进行滚动查询时，请确保满足以下要求。<br><br><br>* 首次调用 API 时，将 `ScrollId` 参数值保持为空。第二次调用 API 时，将参数值设置为第一次调用返回的 `ScrollId` 的值。第三次调用 API 时，将参数值设置为第二次调用返回的 `ScrollId` 的值，依此类推。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果 <code>IsMerge</code> 或 <code>IsMergeUserId</code> 的值设置为 <code>1</code>，则滚动查询时 <code>ScrollId</code> 的值必须始终为空。   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">返回调用结果中的 <code>ScrollId</code> 的值在 API 调用后 20 分钟失效，之后无法用于下一次滚动查询。   </div><br>   <br><br>* 首次调用 API 时，将 `PageNo` 参数值设置为 `1`，第二次调用时设置为 `2`，依此类推。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>PageNo</code> 的值必须按顺序递增，且不能重复。   </div><br>   <br><br>* 保持 `IsMerge` 和 `IsMergeUserId` 的参数值不变。 |
|Name |String |否 |`Viewer A` |昵称。返回昵称包含该值的观众行为数据。 |
|StartTime |Long |否 |`1642070520` |Unix 时间戳格式的开始时间。返回在该时间及之后进入直播间的观众行为数据。单位：秒。 |
|EndTime |Long |否 |`1642070920` |Unix 时间戳格式的结束时间。返回在该时间及之前离开直播间的观众行为数据。单位：秒。 |
|IsMerge |Integer |否 |`0` |指定是否根据设备 ID 合并同一设备多次进出直播间的观众行为数据。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：不合并数据。<br><br>* `1`：合并数据。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">如果观众无需登录直播间即可观看预告、直播和回放，建议你以此方式合并数据，以获得更准确的数据。</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>IsMerge</code> 和 <code>IsMergeUserId</code> 不能同时设置为 <code>1</code>。</div><br> |
|Source |Integer |否 |`0` |返回该来源的数据。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `-1`：返回所有地址的数据。<br><br>* `0`：返回默认地址的数据。<br><br>* `1`：返回地址 A 的数据。<br><br>* `2`：返回地址 B 的数据。<br><br>* `3`：将返回地址C的数据。<br><br>* `4`：将返回地址D的数据。 |
|PlayStatus |Integer |No |`1` |指定统计维度。默认值：`10`。<br><br>有效值：<br><br><br>* `1`：返回观看直播视频的观众数据。<br><br>* `2`：返回观看预告的观众数据。<br><br>* `3`：返回观看回放的观众数据。<br><br>* `10`：返回访问观看页的观众数据。<br><br>* `11`：返回观看直播视频、预告和回放的观众数据。 |
|IsMergeUserId |Integer |No |`0` |指定是否根据用户ID合并多次进出直播间观众的行为数据。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：不合并数据。<br><br>* `1`：合并数据。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">如果观众必须登录直播间后才能观看预告、直播和回放，建议你以此方式合并数据，以获得更准确的数据。</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>IsMerge</code> 和 <code>IsMergeUserId</code> 不能同时设置为 <code>1</code>。</div><br> |
|Extra |String |No |`Marketing Department` |同步到 BytePlus Live 的额外参数，可用于与观众关联。例如，可以将观众的部门从自有账号系统同步到 BytePlus Live。 |


<span id="924e5e72"></span>
## 返回调用结果参数


|Name |Data Type |Sample Value |描述 |
|---|---|---|---|
|TotalItemCount |Integer |`1` |返回结果总数。 |
|Data |Array of[UserBehaviorData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi-zh-CN#d456d258) |`-` |观众的详细行为数据。 |
|ScrollId |String |`IN1ZTTzdZN3J3AAAAAAA****WTFdZalFSaGt` |滚动ID。 |


<span id="d456d258"></span>
### UserBehaviorData


|Name |Data Type |Sample Value |描述 |
|---|---|---|---|
|UserId |Long |`172741906088****` |观众在 BytePlus Live 的唯一标识。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果观众未通过输入昵称或其他方式登录直播间，则该观众的用户 ID 为 0。</div><br> |
|UserName |String |`观众A` |观众昵称。 |
|Region |String |`新加坡` |观众所在地区。 |
|IP |String |`4.**.**.89` |观众的IP地址。若在请求中通过设置`IsMerge`或`IsMergeUserId`为`1`合并行为数据，则该参数值可能包含多个以空格分隔的IP地址。 |
|JoinAt |Array of Integer |`1714653969` |观众进入直播间的时间，Unix时间戳格式。单位：秒。 |
|leaveAt |Array of Integer |`1714668359` |观众离开直播间的时间，Unix时间戳格式。单位：秒。 |
|WatchTime |Integer |`239` |观众观看时长。单位：分钟。 |
|UserTel |String |`1560000****` |观众的手机号。 |
|InviteCode |String |`2711****` |观众使用的邀请码。 |
|AccessTime |String |`playing before` |表示观众进入直播间相对于直播流的时间。<br><br>有效值：<br><br><br>* `playing`：直播流期间。<br><br>* `playing before`：直播流开始前。<br><br>* `playing post`：直播流结束后。 |
|UserDevice |Array of String |`Windows 10` |观众使用的设备类型。 |
|Extra |String |`Marketing Department` |同步到 BytePlus Live 的额外参数，可用于与观众关联。例如，可以将观众的部门从自有账号系统同步到 BytePlus Live。 |
|ExternalUserId |String |`403343425511****` |观众在第三方平台的唯一标识。可通过该关联用户ID识别观众在组织内的身份，便于用户洞察和数据分析。<br><br>观众的关联用户ID会根据其登录直播间的方式而变化。<br><br><br>* 自定义账号：自定义登录时通过`UserId`参数传递的值。更多信息，请参见[自定义认证登录](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions-zh-CN)。<br><br>* 手机号：观众使用手机号注册 BytePlus Live 时生成的 `passport_id`。<br><br>* OAuth 2.0：你自有账号体系中对应用户 ID 的字段。<br><br>* 白名单：观众输入的白名单校验信息。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当观众通过上述方式登录直播间时，该参数才有值。</div><br> |
|SilenceStatus |整数 |`1` |表示观众是否被禁言。<br><br><br>* `1`：已禁言。<br><br>* 其他值：未禁言。 |
|CommentCounts |整数 |`5` |观众发送的评论数。 |


<span id="735d1510"></span>
## 示例

<span id="d820d185"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListUserBehaviorDataAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageItemCount=10&ScrollId=klTVnVZdFk3bWg4YVQwdwAAAAAASn****xybkZ1el&Source=0&IsMerge=0&IsMergeUserId=0
```


<span id="5eba56c8"></span>
### 返回示例

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
## 错误码

有关通用错误码列表，请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
