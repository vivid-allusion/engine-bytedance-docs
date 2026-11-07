---
title: "UpdateSparrow"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateSparrow"
---

该接口用于根据其ID更新函数的名称或描述。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateSparrow&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateSparrow`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|FunctionId |String |是 |输入您希望修改名称的函数ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)获取FunctionId。 |`3gyz993****` |
|Name |String |是 |新的函数名称。名称必须满足以下要求：<br><br><br>* 只能包含字母、数字和连字符（\-）。<br><br>* 长度不得超过128个字符。 |`test-sparrow2` |
|Remark |String |否 |该函数的备注。输入要求如下：<br><br><br>* 允许任何字符。<br><br>* 长度不应超过80个字符。<br><br>* 如果不使用此字段，将不进行修改。当此字段值未填写时，描述将修改为空。 |`This is a test sparrow` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com/?Action=UpdateSparrow&Version=2021-03-01
{
  "FunctionId": "bc36dc7c58e942f0b9f125d186df54d9",
  "Name": "test-doc",
  "Remark": ""
}
```
