---
title: "GetActivityMenuAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-CN"
---

该 API 用于获取直播间中的菜单列表。返回调用结果包含每个菜单的名称、类型和显示顺序。

<span id="11f1c7f4"></span>
## 需求

配额：每个账号每分钟 120 次查询

<span id="efb823e7"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityMenuAPI&Version=2020-06-01`

* 方法：GET


<span id="4436b24c"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="Request"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityMenuAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |该 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`178398113630****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="37718e59"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|菜单 |[菜单](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-CN#d6851f47)数组 |`-` |菜单对象数组。 |


<span id="d6851f47"></span>
### 菜单


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|名称 |String |`Chat` |菜单名称。 |
|类型 |Integer |`3` |菜单类型。<br><br><br>* `1`：图文。<br><br>* `2`：商品卡片。<br><br>* `3`：聊天互动。<br><br>* `4`：互动工具。<br><br>* `5`：聚合在线流。<br><br>* `6`：问答。<br><br>* `7`：内嵌链接。 |
|位置 |Integer |`1` |菜单的显示顺序。该值从 `1` 开始。 |


<span id="abfcc133"></span>
## 示例

<span id="951902d9"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityMenuAPI&Version=2020-06-01&ActivityId=178398113630****
```


<span id="f7900aaf"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityMenuAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714653986
    },
    "Result": [
        {
            "Name": "Chat",
            "Type": 3,
            "Location": 1
        },
        {
            "Name": "Interactions",
            "Type": 4,
            "Location": 2
        }
    ]
}
```


<span id="9d6706a4"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
