---
title: "API 错误码"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-error-code_zh-cn"
---

本文档描述了 BytePlus CDN 中常见的错误码。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在您判断一个 API 请求是否成功时，建议您使用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/api-response_zh-cn#%E5%88%A4%E6%96%AD-api-%E8%AF%B7%E6%B1%82%E6%98%AF%E5%90%A6%E6%88%90%E5%8A%9F">判断 API 请求是否成功</a> 中描述的方法。</div>


<span id="公共错误码"></span>
## 公共错误码

参见 [公共错误码](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。

<span id="权限异常"></span>
## 权限异常

以下错误码表示子用户没有权限使用 API 操作目标资源。


|Code |Message |说明 |
|---|---|---|
|NotFound.Domain |账户下无此域名：xxx,xxx |尝试访问的资源不属于该账号。 |
|AccessDenied.IAMUnauthorized |根据访问的资源，您会收到以下某个错误消息：<br><br><br>* 您没有权限操作域名:  *<domain\>* <br><br>* 您没有权限执行该操作<br><br>* 您没有权限操作项目:  *<project\>*  |子账号无权限访问指定的域名、项目或使用该 API。 |


<span id="参数异常"></span>
## 参数异常

以下错误码表示用户请求不满足 CDN 中的配置。


|Code |Message |参数说明 |
|---|---|---|
|InvalidParameter.<param\> |参数错误 |API 的参数不正确。错误类别在 `<param>` 中指示。 |
|InvalidParameter.Certificate |证书内容解析错误。 |在解析证书内容的时候遇到了错误。 |
|InvalidParameter.Certificate.KeyNotMatch |证书与私钥不匹配。 |您上传的证书公钥与私钥不匹配。 |
|InvalidParameter.Https.CertInfo.ChainMissing |域名配置失败，证书链不完整。 |无法配置域名，原因是证书文件中的证书链不完整。 |
|InternalError.<param\> |内部错误，请稍后重试或联系工程师进行进一步咨询。 |系统出现异常。问题类别在 `<param>` 中指示。请 [提交工单](https://console.byteplus.com/workorder/create)。 |
|InvalidParameter.BillingCode |参数错误：BillingCode 内容不合法。 |参数错误：`BillingCode` 值不合法。 |
|InvalidParameter.BillingRegion |参数错误：BillingRegion。 |参数错误：`BillingRegion` 值不合法。 |


<span id="域名校验"></span>
## 域名校验


|Code |Message |参数说明 |
|---|---|---|
|InvalidParameter.Domain.NeedVerified |请先验证域名的归属权，验证成功后可添加域名。 |域名未通过所有权校验。 |
|InvalidParameter.Domain.RetrieveUnsupported |域名暂不支持取回。 |您无法对该域名进行所有权校验。 |
|InvalidParameter.Domain.DnsNotMatch |解析校验不匹配，请确认重试。 |您配置的 TXT 记录不正确。 |


<span id="已废弃的错误码"></span>
## 已废弃的错误码

以下列表中的错误码已经废弃。这些错误码不会在 CDN 中出现了。


|Code |Message |
|---|---|
|CDN.ResourceNotFound |账户下无此域名：xxx,xxx |
|CDN.PermissionDenied |您没有权限执行该操作。 |
|CDN.PermissionDenied |您没有权限执行该操作。 |
|CDN.InvalidParameters |参数错误 |
|CDN.InvalidParam.Certificate |Certificate参数错误 |
|CDN.InvalidParam.PrivateKey |PrivateKey参数错误 |
|CDN.InvalidParam.Source |Source参数错误 |
|CDN.InvalidParam.CertificateChainError |证书链无法补齐 |
|CDN.InternalError |未知错误，请联系技术支持 |
|CDN.InvalidParam.CertificateExpired |证书已过期 |
|CDN.InvalidParam.BillingCode |BillingCode 参数错误 |
|CDN.InvalidParam.BillingRegion |BillingRegion 参数错误 |
|CDN.InvalidParam.ExportType |ExportType 参数错误 |
