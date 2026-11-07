---
title: "边缘KV快速入门"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-EdgeKV-overview-cn"
---

本教程基于简单的示例场景介绍如何在边缘函数中使用边缘 KV。

边缘 KV 服务是在 BytePlus 的全球边缘节点上的分布式键值存储服务。一个键值对通过边缘函数控制台、OpenAPI 或运行时 API 被写入边缘 KV 后，会自动被同步到所有边缘节点。函数通过运行时 API 可以快速读取位于同一边缘节点的键值对。

<span id="示例场景"></span>
## 示例场景

您的网站支持 A/B 测试功能，可以根据用户的地理位置返回不同版本的网页。版本切换的配置信息存储在边缘 KV 中。您希望可以从函数的代码中读取版本切换的配置信息。在本教程中，假设配置信息如下：

```json
{
  "us": "versionA",
  "eu": "versionB",
  "asia": "versionA"
}
```


<span id="操作步骤"></span>
## 操作步骤

您需要完成以下步骤实现示例场景。


1. 创建一个存储空间。

2. 在存储空间中创建一个键值对。

3. 在函数代码中读取键值对的值。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8182ff737c782af460a4f4b242a0f8eb.jpeg) </span>

<span id="步骤一：创建一个存储空间"></span>
### 步骤一：创建一个存储空间

参见以下步骤创建一个存储空间。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您只能使用控制台或 OpenAPI 创建存储空间。您无法使用运行时 API 创建存储空间。</div>



1. 打开 [边缘KV](https://console.byteplus.com/cdn/edge-function/list) 页面。

2. 在 **边缘KV** 页面，点击 **创建存储空间**。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f54c3597a034c7d4b3b052a7eeb3b121.jpeg) </span>

3. 在 **创建存储空间** 对话框中，设置以下参数，然后点击 **保存** 。

   
   |参数 |描述 |
   |---|---|
   |名称 |设置为 `abtest_config`。 |
   |描述 |设置为 `demo`。 |
   |项目 |设置为 `default`。 |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3ee9514a866fcf1a7c9f82c5022c5bc4.jpeg) </span>


<span id="步骤二：在存储空间中创建一个键值对"></span>
### 步骤二：在存储空间中创建一个键值对

参见以下步骤在存储空间中创建一个键值对。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以使用控制台、OpenAPI 或运行时 API 创建键值对。</div>



1. 打开 [边缘KV](https://console.byteplus.com/cdn/edge-function/list) 页面。

2. 找到您创建的 `abtest_config` 存储空间，点击该存储空间的名称。

3. 点击 **添加数据**。

4. 在弹出的 **添加数据** 对话框中，设置数据的相关参数，然后点击 **保存**。

   
   |参数 |描述 |
   |---|---|
   |键 |设置为 `config_key`。 |
   |值 |设置为示例场景中的 JSON 值 `{"us":"versionA","eu":"versionB","asia":"versionA"}`。 |
   |TTL |设置为 **永久储存**。 |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_20c3a2a3b1312f48c100612561b422af.jpeg) </span>


<span id="步骤三：在函数代码中读取键值对的值。"></span>
### 步骤三：在函数代码中读取键值对的值。

参见以下步骤在函数代码中读取键值对的值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以使用控制台、OpenAPI 或运行时 API 读取键值对的值。</div>


在函数代码中，您调用 [KV.get()](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-EdgeKV-RuntimeAPI-cn) 获取键值对的值。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">边缘函数的调试环境暂不支持运行 <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-EdgeKV-RuntimeAPI-cn">边缘 KV 的运行时 API</a>。边缘 KV 的运行时 API 只能在正式环境运行。</div>


```JavaScript
const config = await KV.get("abtest_config","config_key",{type:"string"});
```
