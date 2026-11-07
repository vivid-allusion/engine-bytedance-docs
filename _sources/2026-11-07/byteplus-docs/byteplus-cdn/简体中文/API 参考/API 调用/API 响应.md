---
title: "API 响应"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-response_zh-cn"
---

本文档介绍了 BytePlus CDN API 的响应。

<span id="响应头"></span>
## 响应头

每个 API 的响应中包含的响应头的描述如下。

<span id="响应状态码"></span>
## 响应状态码

CDN 的响应状态码的介绍如下：


* 2xx：表示 CDN 已成功响应了 API 请求。但是成功响应未必保证 API 请求是成功的。参见 [判断 API 请求是否成功](https://docs.byteplus.com/en/docs/18/46494#%E5%88%A4%E6%96%AD-api-%E8%AF%B7%E6%B1%82%E6%98%AF%E5%90%A6%E6%88%90%E5%8A%9F)。

* 4xx：表示 CDN 无法返回客户端请求的内容。原因是客户端请求不合法。例如：

   * 请求的文件不存在。

   * 请求方法不正确。

   * 请求中缺少必要的参数。例如缺少 `Action` 参数。

   * 请求者没有操作目标资源的权限。

* 5xx：表示请求已经失败了。失败的原因是 CDN 发生了内部错误。例如 CDN 服务不可用。


<span id="判断-api-请求是否成功"></span>
## 判断 API 请求是否成功

在您判断 API 请求是否成功时，不建议您使用 CDN 的响应状态码。我们建议您使用以下判断标准：


* 如果一个 API 请求成功，响应正文的 `ResponseMetadata` 结构体中不包含 `Error` 字段。

* 其余情况都被认为是请求失败。您可以在 `ResponseMetadata` 结构体的 `Error` 字段中找到相应的错误消息。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您的 API 请求可能会遇到以下情况：</div>



* <div data-tips="true" data-tips-type="tip">CDN 的响应状态码是 2xx，但是 <code>ResponseMetadata</code> 结构体中包含 <code>Error</code> 字段。</div>



<div data-tips="true" data-tips-type="tip">在这种情况下，该 API 请求是失败的。原因就是客户端请求不满足 CDN 中的配置。例如：</div>



* <div data-tips="true" data-tips-type="tip">某个请求参数的值不合法。</div>


* <div data-tips="true" data-tips-type="tip">在您为域名配置证书时，证书文件没有包含完整的证书链。</div>



关于 CDN 中的常见错误，参见 [API 请求错误码](https://docs.byteplus.com/en/docs/byteplus-cdn/api-error-code_zh-cn)。

<span id="响应示例"></span>
## 响应示例

<span id="api-请求成功的响应示例"></span>
### API 请求成功的响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2021041510110201022510703416005FB0",
        "Action": "DescribeCdnData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore"
    },
    "Result": {...}
}
```


<span id="api-请求失败的响应示例"></span>
### API 请求失败的响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2021041510110201022510703416005FB0",
        "Action": "DescribeCdnData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore",
        "Error": {
            "Code": "ResourceNotFound",
            "Message": "resource is not found"
        }
    }
}
```
