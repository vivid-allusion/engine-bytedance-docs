---
title: "ListFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn"
---

获取函数列表。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListFunction&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListFunction`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|Page |Integer |否 |页码。 |
|Limit |Integer |否 |每页记录数。默认为 100。每次最多可获取 100 条记录。 |
|OrderBy |Integer |否 |该参数指定数据查询的顺序。它接受以下值：<br><br><br>* 1：降序排列数据。<br><br>* 2（默认）：升序排列数据。 |
|OrderType |String |否 |可用的排序类型有：<br><br><br>* create_time（默认）：根据创建时间对数据进行排序。<br><br>* update_time：根据最后更新时间对数据进行排序。 |
|Status |String |否 |函数的状态。<br><br><br>* 100：运行中<br><br>* 400：未关联<br><br>* 500：配置中 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Functions |Object[] |函数列表。 | |
|AccountIdentity |Long |BytePlus 账户 ID。 |`20****` |
|UserIdentity |Long |该参数无实际意义。请忽略该参数。 | |
|Domain |String[] |绑定到函数的域名。 |`["example.com"]` |
|Name |String |函数的名称。 |`hello-ve` |
|FunctionId |String |函数的 ID。 |`3gyz993****` |
|Status |Integer |函数状态。<br><br><br>* 100：运行中<br><br>* 400：未关联<br><br>* 500：配置中 |`100` |
|Creator |String |创建函数的用户名。 |`example` |
|CreateTime |Long |创建时间。格式为 Unix 时间戳（秒）。 |`1638326159` |
|UpdateTime |Long |更新时间。格式为 Unix 时间戳（秒）。 |`1638326159` |
|Remark |String |函数的备注。 |`this is a test` |
|ProjectName |String |函数所属项目的名称。 |`default` |
|TotalCount |Long |函数总数。 |`1` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListFunction&Version=2021-03-01
```


<span id="返回示例"></span>
### 返回示例

```json

{
  "ResponseMetadata": {
    "RequestId": "202404220913221B87E7D87928AD8F42F8",
    "Action": "ListFunction",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
        "Functions": [
            {
                "AccountIdentity": 300000****,
                "UserIdentity": 0,
                "Domain": [
                    "test1.example.com"
                ],
                "Name": "test1",
                "ClazzName": "Free",
                "BindingType": 200,
                "FunctionId": "54ac587666c148a6b9ffacbb0cb1****",
                "Status": 100,
                "IsPublish": true,
                "IsFullPublish": true,
                "CodeType": "",
                "Creator": "example_user",
                "CreateTime": 1711004239,
                "UpdateTime": 1713270175,
                "Remark": "",
                "ProjectName": "default"
            },
            {
                "AccountIdentity": 300000****,
                "UserIdentity": 0,
                "Domain": [
                    "test2.example.com"
                ],
                "Name": "test",
                "ClazzName": "Free",
                "BindingType": 0,
                "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
                "Status": 400,
                "IsPublish": false,
                "IsFullPublish": false,
                "CodeType": "",
                "Creator": "example_user",
                "CreateTime": 1713776330,
                "UpdateTime": 1713776330,
                "Remark": "",
                "ProjectName": "default"
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
