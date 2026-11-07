---
title: "DeleteSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteSharedConfig_cn"
---

删除一个已有的全局配置。

<span id="前提条件"></span>
## 前提条件

在删除一个全局配置前，请确保其未与任何域名关联。要删除一个全局配置，参照以下步骤：


1. 调用 [DescribeDomainShared](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_cn) 获取该全局配置关联的域名。

2. 对于与该全局配置关联的**每个**域名，执行以下步骤：

   1. 调用 [DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-duplicatetemplate-cn) 复制与域名绑定的分发策略。

   2. 对于新创建的策略,调用 [UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updateservicetemplate-cn) 对该策略进行修改，确保相关的 CDN 功能配置中没有引用该全局配置。您可以参考 [全局配置](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_cn) 了解可以引用全局配置的那些 CDN 功能。

   3. 调用 [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-updatetemplatedomain-05d27-cn) 将新创建的分发策略与该域名绑定。

3. 调用 DeleteSharedConfig 删除该全局配置。


如果子账号在调用该 API 时收到了 `该配置存在关联域名，不允许删除` 的错误，并且子账号调用 [DescribeDomainShared](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_cn) 时并未发现任何关联的域名，那么有可能子账号没有权限访问该全局配置所关联的域名。在这个情况下，需要主账号来解除该全局配置与域名的关联，然后子账号就可以删除该全局配置了。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DeleteSharedConfig&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DeleteSharedConfig`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ConfigName |String |是 |表示一个全局配置的名称。<br><br>您可以调用 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn) 获取已有的全局配置名称。 |`my_list` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DeleteSharedConfig&Version=2021-03-01
{
    "ConfigName": "my_list"
}
```
