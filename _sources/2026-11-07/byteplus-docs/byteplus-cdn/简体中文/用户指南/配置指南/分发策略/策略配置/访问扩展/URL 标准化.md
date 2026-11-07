---
title: "URL 标准化"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/url-normalization_zh-cn"
---

本文档介绍了 BytePlus CDN 提供的 URL 标准化功能。该功能可以降低由于用户请求 URL 不符合规范而导致请求失败的情况。

<span id="功能概述"></span>
## 功能概述

如果用户请求 URL 包含非标内容，由于 CDN 在回源请求中使用相同的 URL，源站可能无法处理该回源请求。类似的，当您在 CDN 中执行刷新或预热操作时，如果您提交的 URL 包含非标内容，刷新和预热的操作结果可能不符合预期。

该功能可以对请求 URL 中出现的以下非标内容进行标准化处理。


|**非标内容** |**标准化方式** |**示例：不规范 URL** |**示例：标准化后的 URL** |
|---|---|---|---|
|反斜杠（\） |替换成单个斜杠（/） |https://www.example.com/img\test |https://www.example.com/img/test |
|连续斜杠（//） |替换成单个斜杠（/） |https://www.example.com//img///test |https://www.example.com/img/test |
|/./ |替换成单个斜杠（/） |https://www.example.com/./img/test |https://www.example.com/img/test |
|/../ |* 如果 `/../` 前还有一个目录，则删除 `/../` 与该目录。<br><br>* 如果 `/../` 前没有目录，则保留原 URL。 |https://www.example.com/all/img/../test |https://www.example.com/all/test |
|||https://www.example.com/../test |https://www.example.com/../test |



* URL 标准化不会使用户请求 URL 重定向到标准化后的 URL。因此，客户端浏览器地址栏中的 URL 不会改变。

* 在收到用户请求时，URL 标准化配置会优先于其他配置生效。"URL 鉴权" 功能是基于标准化后的 URL 进行操作。


<span id="操作步骤"></span>
## **操作步骤**


1. 打开 **URL 标准化** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为开启。

3. 在 **设置对象** 中，勾选您需要启用的 URL 标准化选项。

4. 配置完成后，点击 **保存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8d1a9497303d07ff153c4ce30d749a6a.png) </span>
