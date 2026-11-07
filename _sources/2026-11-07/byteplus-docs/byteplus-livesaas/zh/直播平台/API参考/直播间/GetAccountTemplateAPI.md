---
title: "GetAccountTemplateAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccounttemplateapi-zh-CN"
---

调用此API以获取您BytePlus账户下的直播间模版列表。您可以查找已发布模版的ID，并使用该ID按照模版配置创建直播间。

<span id="requirement"></span>
## 需求

配额：每个账户每分钟最多120次查询

<span id="http-request"></span>
## HTTP请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetAccountTemplateAPI&Version=2020-06-01`

* 方法：GET


<span id="request-parameters"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见[通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |字符串 |是 |`GetAccountTemplateAPI` |API操作。 |
|Version |字符串 |是 |`2020-06-01` |此API操作的版本。当前版本：`2020-06-01`。 |
|PageNo |整数 |否 |`1` |返回页码。<br><br>默认值：`1`。 |
|PageItemCount |整数 |否 |`10` |每页返回结果数量。<br><br>取值范围：[1,500]。<br><br>默认值：`10`。 |
|Status |整数 |否 |`0` |模版状态。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：返回已创建、未发布和已发布模版。<br><br>* `1`：返回已创建和未发布模版。<br><br><br>“已创建”模版尚未发布，“未发布”模版曾经发布过。 |
|Keyword |字符串 |否 |`Template A` |用于按名称筛选模版的关键词。API仅返回名称包含该关键词的模版。<br><br>取值范围：[1,64] |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|TemplateList |Array of[GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi-zh-CN) |`-` |模版列表。 |
|PageNo |整数 |`1` |返回页码。 |
|PageItemCount |整数 |`10` |每页返回结果数量。 |
|TotalItemCount |整数 |`1` |返回模版总数。 |
|EnabledTemplateCount |整数 |`0` |已发布模版总数。 |


<span id="templatelist"></span>
### TemplateList


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|TemplateId |长整型 |`172436707693****` |模版ID。 |
|TemplateName |字符串 |`Template A` |模版名称。 |
|Status |整数 |`1` |模版状态。<br><br><br>* `1`：已创建。<br><br>* `2`：未发布。<br><br>* `3`：已发布。<br><br>* 已创建的模版尚未发布，未发布的模版曾经发布过。<br><br>* 只有已发布的模版才能用于创建直播间。 |
|CoverImage |字符串 |`//p1-live.byteimg.com/tos-cn-i-gjr78lqtd0/29133e74110444****42013881a6be4b~tplv-gjr78lqtd0-image.image` |返回模版封面图的URL，不含协议头。 |
|Description |字符串 |`用于游戏直播的模版。` |模版描述。 |
|ModifyTime |长整型 |`1706166059` |模版最后一次更新时间，Unix时间戳格式（秒）。 |
|IsSystemTemplate |整数 |`2` |表示该模版是系统模版还是自定义模版。系统模版不可修改。<br><br><br>* `1`：系统模版。<br><br>* `2`：自定义模版。 |
|IsDefaultTemplate |整数 |`0` |表示该模版是否为默认模版。<br><br><br>* `0`：非默认模版。<br><br>* `1`：默认模版。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetAccountTemplateAPI&Version=2020-06-01&PageNo=1&PageItemCount=10&Status=0&Keyword=Template A
```


<span id="sample-response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetAccountTemplateAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1706166145
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "TotalItemCount": 1,
        "TemplateList": [
            {
                "TemplateId": 172436707693****,
                "TemplateName": "Template A",
                "Status": 1,
                "CoverImage": "//p1-live.byteimg.com/tos-cn-i-gjr78lqtd0/29133e74110444****42013881a6be4b~tplv-gjr78lqtd0-image.image",
                "Description": "A template for game streaming.",
                "ModifyTime": 1706166059,
                "IsSystemTemplate": 2,
                "IsDefaultTemplate": 0
            }
        ],
        "EnabledTemplateCount": 0
    }
}
```


<span id="error-codes"></span>
## 错误码

下表列出了此API操作的专用错误码。通用错误码列表请参见[常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。


|名称 |消息 |解决方案 |
|---|---|---|
|100000 |内部错误。 |请联系技术支持。 |
|200001 |PageItemCount必须小于或等于500。 |请更改`PageItemCount`参数值。 |
|200001 |指定的参数Status无效。 |请更改`Status`参数值。 |
