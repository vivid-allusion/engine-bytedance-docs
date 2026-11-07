---
title: "UpdateAwardItem"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateAwardItem-zh-CN"
---

调用 `UpdateAwardItem` API，可向奖品库添加新的奖品，或更新已有奖品的名称、库存及其他信息。

<span id="Usage scenario"></span>
## 使用场景

通过本 API 的 `Id` 参数，可以向奖品库添加新奖品或更新已有奖品。


* **添加新奖品：** 在请求参数中不传 `Id`，或将 `Id` 设置为 0，即可创建新奖品。

* **更新已有奖品：** 将待更新奖品的奖品 ID 作为 `Id` 参数的值传入。可通过调用 `GetAwardItemList` API 获取奖品 ID。


<span id="Requirements"></span>
## 使用要求


* 限流：每个账号每秒最多 10 次请求

* 前提条件：需拥有 BytePlus 账号，或具有 **媒体库** \> **奖品库** \> **编辑** 权限的 IAM 用户。关于添加 IAM 用户的更多信息，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=UpdateAwardItem&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateAwardItem` |API 操作。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|AwardItem |[AwardItem](https://docs.byteplus.com/en/docs/11/113727#awarditem) 对象 |是 |*  |奖品库中的奖品列表。 |


<span id="awarditem"></span>
### AwardItem


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|AwardItemIcon |String |否 |https://www.example.com/test.png |奖品图片的 URL，需包含协议。 |
|AwardItemType |Integer |否 |1 |奖品类型。有效值包括：<br><br><br>* `1`：实物奖品<br><br>* `2`：虚拟奖品<br><br>* `3`：自定义奖品<br><br>* `4`：券类奖品<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">新增奖品时必须填写此参数。</div><br> |
|AwardItemName |String |否 |奖品 A |奖品名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">新增奖品时必须填写此参数。</div><br> |
|Id |Long |否 |1715\*\*\*\*1256 |奖品 ID。<br><br><br>* **添加新奖品：** 不传此参数，或将其值设置为 `0`。奖品库最多允许添加 10,000 个奖品。<br><br>* **更新奖品信息：** 传入待更新奖品的奖品 ID。可通过调用 [GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) API 获取 ID。 |
|AwardLotteryTicketAddr |String |否 |https://example.com |券类奖品的领取 URL。长度范围为 1 到 256 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此参数为必填项，仅当<code>AwardItemType</code>设置为4时生效。</div><br> |
|AwardItemStock |Long |否 |200 |奖品库存。取值范围为 [1, 100000]。取值 `-1` 表示库存无限。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">新增奖品时必须填写此参数。</div><br> |
|AwardItemNum |String |否 |48151841 |积分奖品的批次号。长度范围为 1 到 256 个字符。可通过此批次号识别企业积分，并分发给观众。 |
|AwardItemAmounts |Long |否 |1 |每位中奖观众获得的积分数量。取值范围为 [0,99999]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此参数为必填项，仅当<code>AwardItemType</code>设置为3且<code>DeliveryMethod</code>设置为2时生效。</div><br> |
|DeliveryMethod |Integer |否 |1 |自定义奖品的分类。取值：<br><br><br>* `1`：优惠券<br><br>* `2`：积分<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此参数为必填项，当<code>AwardItemType</code>设置为3时生效。</div><br> |
|WinnerInfoType |Array of Integer |否 |[1,2,3] |实物奖品或虚拟奖品中奖者需提供的信息类型。取值：<br><br><br>* `1`：收货地址<br><br>* `2`：手机号<br><br>* `3`：收件人姓名<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此参数为必填项，仅当<code>AwardItemType</code>设置为<code>1</code>或<code>2</code>时生效。</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>AwardItemType</code>设置为<code>2</code>时，此参数仅支持值<code>2</code>。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Status |Boolean |true |奖品是否成功添加或更新。如果操作成功，则返回`true`。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateAwardItem&Version=2023-08-01
{
    "AwardItem": {
        "AwardItemIcon": "https://www.example.com/test.png",
        "AwardItemType": 1,
        "AwardItemName": "Prize",
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
}
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateAwardItem",
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
## 错误码

常见错误码列表请参见 [常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
