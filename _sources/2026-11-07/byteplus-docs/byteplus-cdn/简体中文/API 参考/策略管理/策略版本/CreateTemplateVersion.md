---
title: "CreateTemplateVersion"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateTemplateVersion_zh-cn"
---

为策略创建一个草稿版本。


* 默认情况下，该 API 会基于当前已发布的版本来创建草稿版本，对应控制台上的 "创建版本" 操作。创建的草稿版本与当前已发布的版本具有相同的配置。

* 您也可以指定一个现有版本来创建一个草稿版本，对应控制台上的 "复制版本" 操作。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您不能对一个已包含草稿版本的策略调用该 API。</div>


<div data-tips="true" data-tips-type="tip">要判断指定的策略是否包含草稿版本，您可以对指定的策略调用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn">DescribeTemplateReleaseVersions</a>。在 API 返回的版本列表中，查看 <code>Staus</code> 为 <code>draft</code> 的版本是否存在。</div>


<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=CreateTemplateVersion&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `CreateTemplateVersion`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示需要创建草稿版本的策略 ID。 |`tpl-s18ynd9` |
|Message |String |否 |表示该草稿版本的描述。 |`my desc` |
|ReferredVersion |String |否 |表示一个现有版本的 ID，该 API 基于该版本而创建草稿版本。<br><br>该参数的值不能是 `draft`，默认值是当前发布版本的 ID。<br><br>您可以调用 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn) 获取该策略下的所有版本。 |`P-250414.89520` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=CreateTemplateVersion&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "Message": "Hello World",
    "ReferredVersion": "P-250414.89520"
}
```


&nbsp;
