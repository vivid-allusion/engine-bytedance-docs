---
title: "AddCertificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-AddCertificate_zh-tw"
---

在 BytePlus CDN 中上傳一本伺服器憑證，用於為網域名稱配置 HTTPS。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=AddCertificate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `AddCertificate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Source |String |否 |表示憑證存放的位置。該參數的取值只能是 `cert_center`，表示 BytePlus 憑證中心。 |`cert_center` |
|Certificate |String |是 |表示憑證檔案的內容，建議包含完整的憑證鏈。內容中的換行需要使用 `\r\n` 替換。憑證檔案的副檔名是 .crt 或者 .pem。 |`-----BEGIN CERTIFICATE-----\r\n......\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\n.......\r\n-----END CERTIFICATE-----` |
|PrivateKey |String |是 |表示憑證私密金鑰檔案的內容。內容中的換行需要使用 `\r\n` 替換。憑證私密金鑰檔案的副檔名是 .key 或者 .pem。 |`-----BEGIN RSA PRIVATE KEY-----\r\n.....\r\n-----END RSA PRIVATE KEY-----` |
|Desc |String |否 |表示該憑證的備註。 |`Note` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|CertId |String |表示上傳後該憑證在 `Source` 中的 ID。 |`cert-17f1d965a11342eb80d9a0ecfef35713` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=AddCertificate&Version=2021-03-01
{
    "Source": "cert_center",
    "Certificate": "-----BEGIN CERTIFICATE-----\r\nMIGrhI\r\nmg==\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\nMIIE ==\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\nMIID \r\nMrY=\r\n-----END CERTIFICATE-----",
    "PrivateKey": "-----BEGIN RSA PRIVATE KEY-----\r\nMIIjQVx9Q==\r\n-----END RSA PRIVATE KEY-----"
}
```


<span id="範例回應"></span>
### 範例回應

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
