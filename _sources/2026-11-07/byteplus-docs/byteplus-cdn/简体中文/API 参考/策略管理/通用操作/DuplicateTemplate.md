---
title: "DuplicateTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-duplicatetemplate-cn"
---

通过复制一个已有策略来创建一个配置相同，类型相同的策略。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DuplicateTemplate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DuplicateTemplate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ReferredTemplateId |String |是 |表示一个待复制的策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) 获取您想要复制的策略的 ID。 |`tpl-sZRpwq` |
|Message |String |否 |表示创建的策略的描述，长度不能超过 120 个字符。 |`This is a dup policy.` |
|Title |String |否 |表示创建的策略的名称，长度不能超过 100 个字符。<br><br>如果该参数未指定，CDN 会生成一个随机名称。 |`Dup_Policy` |
|Project |String |否 |表示创建的策略所归属的项目。<br><br>该参数的默认值是 "default"，表示 Default 项目。 |`default` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TemplateId |String |表示创建的策略的 ID。 |`tpl-s2N4rW` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DuplicateTemplate&Version=2021-03-01
{
    "ReferredTemplateId": "tpl-sZRpwq",
    "Title": "Dup_Policy",
    "Message": "This is a dup policy."
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024030403552737EB957CFE0697DBB981",
        "Action": "DuplicateTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TemplateId": "tpl-s2N4rW"
    }
}
```


&nbsp;
