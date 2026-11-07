---
title: "DeleteTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-deletetemplate-cn"
---

删除一个策略或者策略的某个版本。

**删除策略**

如果一个策略被删除，该策略的所有版本都会被删除。

要删除一个策略，该策略必须未绑定任何域名。您可以调用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplates-cn) 了解一个策略是否已与某个域名绑定。只有当该策略的 `BoundDomains` 是 `null` 时，您才可以删除该策略。

假设一个策略已绑定了一个或者多个域名。如果您需要将其与这些域名解绑，参见 [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn) 中的相关描述。

**删除策略的版本**

您只能删除未发布的策略版本，也就是说，您只能删除策略下 `Status` 为 `draft` 或者 `stop` 的版本。要获取策略下的所有版本以及每个版本的状态，参见 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn)。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DeleteTemplate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DeleteTemplate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要删除的策略的 ID。<br><br>您可以调用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplates-cn) 获取您想要删除的策略 ID。 |`tpl-s2N4rW` |
|TemplateVersion |String |否 |表示要删除的版本。该版本的状态不能是 `running`。<br><br>您可以调用 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn) 获取该策略下的所有的版本以及版本的状态。 |`P-250414.89520` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DeleteTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-sqdYQ2",
    "TemplateVersion": "P-250414.89520"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202508251227583CD38EED31C8FCA7FF07",
        "Action": "DeleteTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
