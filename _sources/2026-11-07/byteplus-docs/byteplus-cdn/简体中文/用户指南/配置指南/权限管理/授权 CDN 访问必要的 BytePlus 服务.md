---
title: "授权 CDN 访问必要的 BytePlus 服务"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-authorize-byteplus-cdn-to-access-byteplus-certificate-center-cn"
---

在 BytePlus CDN 中，如果您执行以下操作，您需要授权 CDN 访问对应的 BytePlus 服务：


* 指定 BytePlus 对象存储（TOS）中的一个存储桶作为一个源站：您需要授权 CDN 访问 TOS 服务。

* 上传证书或者关联一个 BytePlus 证书中心中的证书：您需要授权 CDN 访问证书中心服务。

* 创建边缘函数：您需要授权 CDN 访问边缘函数服务。


为了避免您以及子用户在执行以上操作时遇到权限问题，我们建议您事先授予 CDN 权限访问这些服务。

<span id="操作步骤"></span>
## 操作步骤

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">强烈推荐使用主账号操作以下步骤。当以下步骤完成后，如果主账号和子用户在 CDN 中操作证书、管理边缘函数、设置 TOS 存储桶为源站时，无需再次执行这些步骤，也不会遇到服务授权问题。</div>


<div data-tips="true" data-tips-type="warning">对于子账号，除非被授予了 IAMFullAccess 系统策略，子账号没有权限授予 CDN 访问其他 BytePlus 服务。因此，如果一个没有没有被授予 IAMFullAccess 策略的子账号操作以下步骤，授权会失败。同时，不建议授予子用户 IAMFullAccess 策略，因为该策略的权限范围太广。</div>



1. 打开 [该链接](https://console.byteplus.com/iam/service/attach_role/?ServiceName=CDN)。

2. 点击 **立即授权**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e28a1a13b28e8cbea1004dcb05fdfa1f.png) </span>
