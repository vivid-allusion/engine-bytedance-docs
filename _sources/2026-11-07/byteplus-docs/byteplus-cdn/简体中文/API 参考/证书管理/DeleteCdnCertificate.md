---
title: "DeleteCdnCertificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteCdnCertificate_zh-cn"
---

删除一个托管在 CDN 的证书。您只能删除未与任何域名关联的证书。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DeleteCdnCertificate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DeleteCdnCertificate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|CertId |String |是 |表示待删除证书的 ID。证书的 ID 以 `cert_hosting` 开头。<br><br>您可以调用 [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcertinfo-cn) 获取证书 ID 的列表。 |`cert_hosting-4041`<br><br> |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DeleteCdnCertificate&Version=2021-03-01
{
    "CertId": "cert_hosting-4041"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202207131500530102120352272280EC8F",
        "Action": "DeleteCdnCertificate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```
