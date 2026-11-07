---
title: "GetFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetFunction-cn"
---

获取指定函数的详细信息。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetFunction&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetFunction`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|AccountIdentity |Long |BytePlus 账户 ID。 |`20****` |
|UserIdentity |Long |该参数无实际意义。请忽略该参数。 | |
|Domain |String[] |绑定到函数的域名。 |`["example.com"]` |
|Name |String |函数的名称。 |`hello-ve` |
|ClazzName |String |该参数无实际意义。请忽略该参数。 | |
|BindingType |Integer |该参数无实际意义。请忽略该参数。 | |
|FunctionId |String |函数的 ID。 |`3gyz993****` |
|Status |Integer |函数状态。<br><br><br>* 100：运行中<br><br>* 400：未关联<br><br>* 500：配置中 |`100` |
|IsPublish |Boolean |该参数无实际意义。请忽略该参数。 | |
|IsFullPublish |Boolean |该参数无实际意义。请忽略该参数。 | |
|CodeType |String |该参数无实际意义。请忽略该参数。 | |
|Creator |String |创建函数的用户名。 |`example` |
|CreateTime |Long |创建时间。格式为 Unix 时间戳（秒）。 |`1638326159` |
|UpdateTime |Long |更新时间。格式为 Unix 时间戳（秒）。 |`1638326159` |
|Remark |String |函数的备注。 |`this is a test` |
|ProjectName |String |函数所属项目的名称。 |`default` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetFunction&Version=2021-03-01&FunctionId=bc36dc7c58e942f0b9f125d186df****
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "202404220913431B87E7D87928AD8F48BE",
        "Action": "GetFunction",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Function": {
            "AccountIdentity": 300000****,
            "UserIdentity": 0,
            "Domain": [
                "test.example.com"
            ],
            "Name": "test",
            "ClazzName": "Free",
            "BindingType": 0,
            "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
            "Status": 400,
            "IsPublish": true,
            "IsFullPublish": true,
            "CodeType": "js",
            "Creator": "test_user",
            "CreateTime": 1713776330,
            "UpdateTime": 1713776330,
            "Remark": "",
            "ProjectName": "default"
        }
    }
}
```


&nbsp;
