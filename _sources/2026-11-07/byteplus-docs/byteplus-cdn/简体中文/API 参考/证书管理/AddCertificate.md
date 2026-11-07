---
title: "AddCertificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-cn-addcertificate"
---

在 BytePlus CDN 中上传一本服务器证书，用于为域名配置 HTTPS。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=AddCertificate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `AddCertificate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Source |String |否 |表示证书存放的位置。该参数有以下取值：<br><br><br>* `cert_center`：表示 BytePlus 证书中心。<br><br>* `cdn_cert_hosting`：表示 BytePlus CDN 证书托管。要将证书托管在 CDN，请 [提交工单](https://console.byteplus.com/workorder/create?_vtm_=a78999.b69280.0_0.0_0.0.1016_7659971919328183861)。<br><br><br>该参数的默认值是 `cdn_cert_hosting`。 |`cert_center` |
|Certificate |String |是 |表示证书文件的内容，建议包含完整的证书链。内容中的换行需要使用 `\r\n` 替换。证书文件的扩展名是 .crt 或者 .pem。 |`-----BEGIN CERTIFICATE-----\r\n......\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\n.......\r\n-----END CERTIFICATE-----` |
|PrivateKey |String |是 |表示证书私钥文件的内容。内容中的换行需要使用 `\r\n` 替换。证书私钥文件的扩展名是 .key 或者 .pem。 |`-----BEGIN RSA PRIVATE KEY-----\r\n.....\r\n-----END RSA PRIVATE KEY-----` |
|Desc |String |否 |表示该证书的备注，长度不能超过 64 个字符。 |`Note` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|CertId |String |表示上传后该证书在 `Source` 中的 ID。 |`cert-17f1d965a11342eb80d9a0ecfef35713` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=AddCertificate&Version=2021-03-01
{
    "Source": "cert_center",
    "Certificate": "-----BEGIN CERTIFICATE-----\r\nMIGrhI\r\nmg==\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\nMIIE ==\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\nMIID \r\nMrY=\r\n-----END CERTIFICATE-----",
    "PrivateKey": "-----BEGIN RSA PRIVATE KEY-----\r\nMIIjQVx9Q==\r\n-----END RSA PRIVATE KEY-----"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240402082809CAFB8B06254524ECDFF3",
        "Action": "AddCertificate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertId": "cert-c6424725984f4c69b671e119aa0ffa69"
    }
}
```


&nbsp;
