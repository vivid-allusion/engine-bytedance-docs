---
title: "GetTaskAwardItemListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetTaskAwardItemListAPI-zh-CN"
---

获取已在直播间发送的观看时长抽奖奖品列表。

<span id="Requirements"></span>
## 要求


* 配额：每个账号每分钟最多查询 120 次。

* 前提条件：需拥有 BytePlus 账号，或具有 **Insights** \> **仅查看** 或 **编辑**权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* 接口地址：https://livesaas.byteplusapi.com/?Action=GetTaskAwardItemListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整参数列表请参见 [通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetTaskAwardItemListAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |1798615803\*\*\*\* |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 获取该 ID。 |
|PageNo |Integer |否 |1 |返回结果的页码。默认值：`1`。 |
|PageItemCount |Integer |否 |10 |每页返回的结果数量。默认值：`10`。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TaskAwardItemList |Array of[TaskAwardItemList](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI-zh-CN#taskawarditemlist) |无 |观看时长抽奖奖品信息列表。 |
|PageNo |Integer |1 |返回结果的页码。 |
|PageItemCount |Integer |10 |每页返回的结果数量。 |
|PageTotalCount |Integer |1 |查询结果总数。 |


<span id="taskawarditemlist"></span>
### TaskAwardItemList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TaskAwardItemId |String |8480 |观看时长抽奖奖品的奖品 ID。 |
|AwardItemType |Integer |4 |奖品类型。有效值如下：<br><br><br>* `1`：实物奖品<br><br>* `2`：虚拟奖品<br><br>* `3`：自定义奖品<br><br>* `4`：代金券奖品 |
|PeopleCount |Integer |1 |参与人数。 |
|AwardCount |Integer |1 |获奖人数。 |
|AwardItemName |String |实物奖品 |奖品名称。 |
|AwardLotteryTicketAddr |String |https://example.com |代金券奖品的领取 URL。长度范围为 1 到 256 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>AwardItemType</code> 设置为 4 时，该参数为必填且生效。</div><br> |
|AwardStartTime |Long |1689570360 |观看时长抽奖的开始时间。Unix 时间戳（秒）。 |
|AwardEndTime |Long |1689656640 |观看时长抽奖的结束时间。Unix 时间戳（秒）。 |
|AwardItemNum |String |48151841 |积分奖品的批次号。长度范围为 1 到 256 个字符。可通过该批次号识别企业积分，并发放给观众。 |
|AwardItemAmounts |Integer |1 |每位获奖观众获得的积分数量。取值范围为 [0,99999]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>AwardItemType</code> 设置为 3 时，该参数为必填且生效。</div><br> |
|TaskAwardIcon |String |//example\-image.image |奖品图标的 URL（不含协议头）。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetTaskAwardItemListAPI&Version=2020-06-01&ActivityId=1798615803****&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202301112319419CCB1169F45D1CD7A49F",
    "Action": "GetTaskAwardItemListAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "cn-north-1",
    "SystemTime": 1673450381
  },
  "Result": {
    "PageNo": 1,
    "PageItemCount": 10,
    "PageTotalCount": 1,
    "TaskAwardItemList": [
      {
        "TaskAwardItemId": "8480",
        "AwardItemType": 1,
        "PeopleCount": 1,
        "AwardCount": 0,
        "AwardItemName": "Prize A",
        "AwardLotteryTicketAddr": "",
        "AwardItemNum": "",
        "AwardItemAmounts": 0,
        "TaskAwardIcon": "//example.com/path/to/image.png",
        "AwardStartTime": 1689570360,
        "AwardEndTime": 1689656640
      }
    ]
  }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见 [常见错误码及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
