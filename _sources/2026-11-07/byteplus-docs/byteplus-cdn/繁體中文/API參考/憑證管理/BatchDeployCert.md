---
title: "BatchDeployCert"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/BatchDeployCert_zh-tw"
---

將指定憑證與一個或多個網域名稱關聯。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=BatchDeployCert&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `BatchDeployCert`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示一個需要與 `CertId` 關聯的網域名稱列表，列表中最多包含 50 個網域名稱。多個網域名稱之間使用逗號（,）分隔。<br><br>如果列表中的某個網域名稱不在該憑證的 SAN 欄位中，該網域名稱將無法與該憑證關聯。 |`www.example.com,img.example.com` |
|CertId |String |是 |表示待關聯的憑證的 ID。 |`cert-c195f679cecb4f34tj23dd8c54e6c0a2` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|DeployResult |Object[] |表示各網域名稱的關聯結果。 | |
|Domain |String |表示 `Domain` 中的一個網域名稱。 |`example.com` |
|Status |String |表示關聯是否成功。該參數的取值如下：<br><br><br>* `success`：表示關聯成功。<br><br>* `fail`：表示關聯失敗。失敗原因在 `ErrorMsg` 參數中描述。 |`success` |
|ErrorMsg |String |表示關聯失敗的原因。如果 `Status` 是 `success`，該參數值為空（""）。 |`some error` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=BatchDeployCert&Version=2021-03-01
{
    "Domain": "www.example.com,docs.example.com",
    "CertId": "cert-a4827a17f0964010a199e74f6e6b6a52"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2025091106370814AF152ABDC20800D531",
        "Action": "BatchDeployCert",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DeployResult": [
            {
                "Domain": "www.example.com",
                "ErrorMsg": "",
                "Status": "success"
            },
            {
                "Domain": "docs.example.com",
                "ErrorMsg": "",
                "Status": "success"
            }
        ]
    }
}
```


&nbsp;
