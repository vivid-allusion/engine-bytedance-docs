---
title: "GetAwardItemList"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetAwardItemList-zh-CN"
---

调用`GetAwardItemList` API 获取当前账号奖品库中的奖品列表，包括奖品名称、库存、图片及其他信息。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">使用 IAM 用户调用本 API 时，仅可获取该 IAM 用户有权限访问或编辑的奖品信息。关于如何配置 IAM 用户的用户范围和分类范围，详见 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">用户、组织与角色管理</a>。</div>


<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多 10 次请求

* 前提条件：需要拥有 BytePlus 账号，或具备**媒体库** \> **奖品库** \> **编辑**或**仅查看**权限的 IAM 用户。关于如何添加 IAM 用户，详见[用户、组织与角色管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetAwardItemList&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetAwardItemList` |API 操作。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本号。当前版本：`2023-08-01`。 |
|Name |String |否 |Prize A |奖品名称。支持模糊搜索，不区分大小写。<br><br>例如，若参数设置为**A**，则会返回**Prize A**、**Prize abc**等奖品。 |
|PageNumber |Integer |否 |1 |要返回的页码。默认值：`1`。取值需大于等于 1。 |
|PageSize |Integer |否 |200 |每页返回的结果数量。默认值：`200`。取值范围为 [1,1000]。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|AwardItemList |[AwardItemList](https://docs.byteplus.com/en/docs/11/113725#awarditemlist) 数组 |*  |奖品库中的奖品列表。 |
|TotalCount |Long |1 |查询结果总数。 |


<span id="awarditemlist"></span>
### AwardItemList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|AwardItemIcon |String |https://www.example.com/test.png |奖品图片的 URL，包含协议。 |
|AwardItemType |Integer |1 |奖品类型。有效取值：<br><br><br>* `1`：实物奖品<br><br>* `2`：虚拟奖品<br><br>* `3`：自定义奖品<br><br>* `4`：卡券奖品 |
|AwardItemName |String |Prize A |奖品名称。 |
|Id |Long |1715\*\*\*\*1256 |奖品 ID。获取奖品 ID 后，可调用[UpdateAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateawarditem) API 更新奖品信息，或调用[DeleteAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteawarditem) API 删除奖品。 |
|AwardLotteryTicketAddr |String |https://example.com |抽奖券奖品的领取 URL。 |
|AwardItemStock |Long |200 |奖品库存。取值为`-1`时表示库存不限。 |
|AwardItemNum |String |48151841 |积分奖品的批次号。可通过该批次号识别企业积分并发放给观众。 |
|AwardItemAmounts |Long |1 |每位中奖观众获得的积分数量。仅当`DeliveryMethod`为 2 时有效。 |
|DeliveryMethod |Integer |1 |自定义奖品的分类。仅当`AwardItemType`为 3 时有效。取值：<br><br><br>* `1`：优惠券<br><br>* `2`：积分 |
|WinnerInfoType |Integer 数组 |[1,2,3] |实物或虚拟奖品中奖者需填写的信息类型。取值：<br><br><br>* `1`：收货地址<br><br>* `2`：手机号<br><br>* `3`：收件人姓名 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetAwardItemList&Version=2023-08-01&Name=Prize A&PageNumber=1&PageSize=200
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetAwardItemList",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "cn-north-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "AwardItemList": [
            {
                "AwardItemIcon": "https://www.example.com/test.png",
                "AwardItemType": 1,
                "AwardItemName": "Prize A",
                "Id": 1715****1256,
                "AwardLotteryTicketAddr": "https://example.com",
                "AwardItemStock": 200,
                "AwardItemNum": "48151841",
                "AwardItemAmounts": 1,
                "DeliveryMethod": 1,
                "WinnerInfoType": [
                    1,
                    2,
                    3
                ]
            }
        ],
        "TotalCount": 1
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
