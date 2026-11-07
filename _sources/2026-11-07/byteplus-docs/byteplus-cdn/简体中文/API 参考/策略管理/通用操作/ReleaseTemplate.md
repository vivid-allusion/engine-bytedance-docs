---
title: "ReleaseTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ReleaseTemplate_zh-cn"
---

发布一个策略的指定版本。


* 如果待发布版本的状态是 `draft`，该 API 操作对应控制台上的 "发布" 操作。

* 如果待发布版本的状态是 `stop`，该 API 操作对应控制台上的 "回滚" 操作。


<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=ReleaseTemplate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ReleaseTemplate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示要发布的版本所在的策略 ID。 |`tpl-s18ynd9` |
|Env |String |否 |表示发布环境。当前，该参数值只能是 `prod`，表示线上环境。该参数的默认值也是 `prod`。 |`prod` |
|Message |String |否 |表示发布操作的描述。 |`My Desc` |
|TemplateVersion |String |否 |表示待发布的版本号。该参数的默认值是 `draft`。 |`P-250411.16282` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=ReleaseTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "TemplateVersion": "P-250411.16282"
}
```


&nbsp;
