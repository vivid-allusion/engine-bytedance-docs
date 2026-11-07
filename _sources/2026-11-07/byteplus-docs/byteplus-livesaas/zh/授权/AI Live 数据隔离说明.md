---
title: "AI Live 数据隔离说明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/doc-118702"
---

AI Live 按账户级别隔离数据，以防止未经授权访问或修改其他用户的数据。

访问控制如下：


* **子账户**只能访问其自身创建或拥有的数据。

* **管理员账户**可以访问与该账户关联的所有数据，包括属于子账户的数据。

* **对于 AI 角色配额**，每个账户拥有独立配额，并且只消耗自身配额。不同账户的配额互不影响。例如，若总配额为 13，且两个子账户各分配 5 个配额，则管理员账户保留 3 个配额供自身使用。每个子账户可独立训练至其分配的 5 个配额，不受其他账户影响。目前，您可通过提供子账户邮箱地址及所需配额数量，联系 BytePlus 支持进行配额分配。


对于非 AI Live 直播间，您可以为用户分配角色，以分配和管理资源访问权限。详情请参见[添加角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN#08751041)。

<span id="433a996b"></span>
### 按功能划分的账户可见性

下表描述了每项功能中子账户和管理员账户的数据可见性。


|**功能** |**资源** |**子账户可见性** |**管理员账户可见性** |
|---|---|---|---|
|AI Live |AI 角色、语音、知识库、商品，以及来自 TikTok Shop、Shopify 和内部系统的集成店铺 |仅可访问自身数据。例如，子账户只能查看其创建的 AI 形象、语音、知识库、产品和集成店铺，无法查看其他子账户或管理员账户创建的 AI 形象、语音、知识库、产品和集成店铺。 |账户下的所有资源。 |
|AI Analysis |主播评分和直播审核任务 |仅限自身数据。例如，子账户只能查看其创建的主播评分和直播审核任务，无法查看其他子账户创建的任务。 |账户下的所有资源。 |


<span id="2851f01d"></span>
## 服务中心

AI Live 和 AI Analysis 的**服务中心**页面仅对管理员账户开放。子账户无法访问**服务中心**页面。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fb09b6b3d6a4e888569431499623528~tplv-goo7wpa0wc-image.image) </span>
