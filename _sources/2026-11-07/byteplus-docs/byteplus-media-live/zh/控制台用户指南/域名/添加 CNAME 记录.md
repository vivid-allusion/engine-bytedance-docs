---
title: "添加 CNAME 记录"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adding-a-cname-record-zh-CN"
---

在 BytePlus MediaLive 控制台添加域名后，BytePlus MediaLive 会自动为您的域名分配一个 BytePlus MediaLive 域名，您可以在域名列表的 **CNAME** 列中找到该域名。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/921578252bd64ce5b8cdba2a4952cb4d~tplv-goo7wpa0wc-image.image) </span>

将您的域名指向由 BytePlus MediaLive 分配的 CNAME 地址。配置生效后，您的直播流将获得加速。要使用 BytePlus MediaLive 服务，必须添加 CNAME 记录。

<span id="78110c72"></span>
### 前提条件


* 已添加域名。

* 域名尚未配置 CNAME 记录，在域名列表的 **CNAME** 列中会显示黄色感叹号（!）。


<span id="a9099180"></span>
### 操作步骤

本主题介绍配置 CNAME 记录的常用方法。本操作步骤为通用指南。如无法按照上述步骤配置 CNAME 记录，请联系域名服务商获取更多信息。


1. 登录您的域名服务商控制台。

2. 选择您需要管理的域名。

3. 在出现的页面中，配置以下参数以添加 CNAME 记录。

   * 主机记录：输入子域名前缀。例如，若域名为 example.live.com，则输入 `example`。

   * 记录类型：选择 **CNAME**。

   * 线路类型：选择默认线路类型。

   * 记录值：输入该域名的 CNAME 地址。您可以在 BytePlus MediaLive 控制台的域名列表中找到 CNAME 地址。

   * TTL：建议填写 600s。

4. 保存配置并等待其生效。此时，域名列表的 **CNAME** 列会显示绿色对勾（✓）。
