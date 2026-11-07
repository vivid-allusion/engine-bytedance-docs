---
title: "CreateSparrow"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateSparrow"
---

该接口用于创建函数。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateSparrow&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `CreateSparrow`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Name |String |是 |函数名称。以下为命名规则：<br><br><br>* 可以使用大写字母、小写字母、数字和连字符（\-）。<br><br>* 名称不应长于128个字符。 |`test-sparrow` |
|ProjectName |String |否 |函数所属项目的名称，默认为`default`。 |`default` |
|Remark |String |否 |该函数的备注。输入要求如下：<br><br><br>* 允许任何字符。<br><br>* 长度不应超过128个字符。 |`This is a test sparrow` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|FunctionId |String |函数的ID。 |`3gyz993****` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
POST  https://cdn.byteplusapi.com?Action=CreateSparrow&Version=2021-03-01
{
  "Name": "test-sparrow"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
  "ResponseMetadata": {
    "RequestId": "202404220916070BE49FB085D18E85BA26",
    "Action": "CreateSparrow",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "FunctionId": "bc36dc7c58e942f0b9f125d186df****"
  }
}
```


&nbsp;
