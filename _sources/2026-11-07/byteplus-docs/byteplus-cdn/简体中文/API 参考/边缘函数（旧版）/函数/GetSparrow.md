---
title: "GetSparrow"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetSparrow"
---

该接口用于根据其ID获取函数的详细信息。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetSparrow&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetSparrow`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |输入您希望获取详细信息的函数的ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|AccountIdentity |Long |账户ID |`20****` |
|Creator |String |创建者 |`zhangsan` |
|Domain |String[] |绑定到函数的域名。 |`[test-sparrow.test.test]` |
|FunctionId |String |函数的ID。 |`3gyz993****` |
|Name |String |函数的名称。 |`hello-ve` |
|ProjectName |String |函数所属项目的名称。 |`default` |
|Remark |String |该函数的备注。 |`this is a test` |
|Status |Integer |函数状态。<br><br><br>* 100：运行中<br><br>* 400：未关联<br><br>* 500：配置中 |`100` |
|CreateTime |Long |创建时间。以UNIX时间戳格式显示。 |`1638326159` |
|UpdateTime |Long |更新时间。以UNIX时间戳格式显示。 |`1638326159` |
|UserIdentity |Long |用户ID |`0****` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=GetSparrow&Version=2021-03-01&FunctionId=bc36dc7c58e942f0b9f125d186df****
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "202404220913431B87E7D87928AD8F48BE",
        "Action": "GetSparrow",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Sparrow": {
            "AccountIdentity": 300000****,
            "UserIdentity": 0,
            "Domain": [],
            "Name": "test",
            "ClazzName": "Free",
            "BindingType": 0,
            "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
            "Status": 400,
            "IsPublish": false,
            "IsFullPublish": false,
            "CodeType": "js",
            "Creator": "CDN_test",
            "CreateTime": 1713776330,
            "UpdateTime": 1713776330,
            "Remark": "",
            "ProjectName": "default"
        }
    }
}
```


&nbsp;
