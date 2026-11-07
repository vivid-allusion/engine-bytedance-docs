---
title: "DescribeCertConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCertConfig_zh-tw"
---

對於可與指定憑證關聯的網域名稱，獲取這些網域名稱的憑證配置。這些網域名稱在指定憑證的 SAN 欄位中並且已添加到 CDN 中。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeCertConfig&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeCertConfig`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|CertId |String |是 |表示您要查詢的憑證的 ID。<br><br>您可以調用 [ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCdnCertInfo_zh-tw) 獲取憑證的 ID。 |`cert-5dc4bfa90c1048778abf036b03ffabf2` |
|Status |String |否 |表示網域名稱的狀態，用於對該 API 回應的網域名稱進行篩選。您可以指定多個狀態，狀態之間使用逗號（,）分隔。<br><br>該參數有以下取值：<br><br><br>* `online`：表示狀態是 "運行中"。<br><br>* `offline`：表示狀態是 "已下線"。<br><br>* `configuring`：表示狀態是 "配置中"。<br><br><br>如果不指定該參數，表示不對網域名稱進行篩選。 |`online,configuring` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|CertNotConfig |Object[] |表示可與 `CertId` 關聯，但尚未關聯任何憑證的網域清單。 | |
|Domain |String |表示清單中的一個網域名稱。 |`img.example.com` |
|Status |String |表示該網域名稱的狀態，有以下取值：<br><br><br>* `online`：表示狀態是 "運行中"。<br><br>* `offline`：表示狀態是 "已下線"。<br><br>* `configuring`：表示狀態是 "配置中"。 |`offline` |
|DomainLock |Object |表示該網域名稱是否被鎖定。如果一個網域名稱被鎖定了，您無法修改其配置。 | |
|Remark |String |表示網域名稱被鎖定的原因。<br><br><br>* 如果 `DomainLock` 結構體中的 `Status` 是 `on`，該參數表示該網域名稱被鎖定的原因。<br><br>* 如果 `Status` 是 `off`，該參數的值是空（""）。 |`some reason` |
|Status |String |表示該網域名稱的鎖定狀態。該參數有以下取值：<br><br><br>* `on`：表示該網域名稱已被鎖定。<br><br>* `off`：表示該網域名稱未被鎖定。 |`off` |
|SpecifiedCertConfig |Object[] |表示已與 `CertId` 關聯的網域清單。 | |
|Domain |String |表示清單中的一個網域名稱。 |`abc.example.com` |
|Status |String |表示該網域名稱的狀態。該參數有以下取值：<br><br><br>* `online`：表示狀態是 "運行中"。<br><br>* `offline`：表示狀態是 "已下線"。<br><br>* `configuring`：表示狀態是 "配置中"。 |`configuring` |
|CerStatus |String |表示該網域名稱關聯的憑證的狀態。該參數有以下取值：<br><br><br>* `running`：表示憑證的有效期大於 30 天。<br><br>* `expired`：表示憑證已經過期。<br><br>* `expiring_soon`：表示憑證的有效期小於等於 30 天，但還未過期。 |`expiring_soon` |
|DomainLock |Object |表示該網域名稱是否被鎖定。如果一個網域名稱被鎖定了，您無法修改其配置。 | |
|Remark |String |表示網域名稱被鎖定的原因。<br><br><br>* 如果 `DomainLock` 結構體中的 `Status` 是 `on`，該參數表示該網域名稱被鎖定的原因。<br><br>* 如果 `Status` 是 `off`，該參數的值是空（""）。 |`some reason` |
|Status |String |表示該網域名稱的鎖定狀態。該參數有以下取值：<br><br><br>* `on`：表示該網域名稱已被鎖定。<br><br>* `off`：表示該網域名稱未被鎖定。 |`on` |
|OtherCertConfig |Object[] |表示可與 `CertId` 關聯，但已關聯其他憑證的網域清單。 | |
|Domain |String |表示清單中的一個網域名稱。 |`www.example.com` |
|Status |String |表示該網域名稱的狀態，有以下取值：<br><br><br>* `online`：表示狀態是 "運行中"。<br><br>* `offline`：表示狀態是 "已下線"。<br><br>* `configuring`：表示狀態是 "配置中"。 |`online` |
|CerStatus |String |表示該網域名稱關聯的憑證的狀態。該參數有以下取值：<br><br><br>* `running`：表示憑證的有效期大於 30 天。<br><br>* `expired`：表示憑證已經過期。<br><br>* `expiring_soon`：表示憑證的有效期小於等於 30 天，但還未過期。 |`running` |
|DomainLock |Object |表示該網域名稱是否被鎖定。如果一個網域名稱被鎖定了，您無法修改其配置。 | |
|Remark |String |表示該網域名稱被鎖定的原因。<br><br><br>* 如果 `DomainLock` 結構體中的 `Status` 是 `on`，該參數表示鎖定的原因。<br><br>* 如果 `Status` 是 `off`，該參數的值是空（""）。 |`some reason` |
|Status |String |表示該網域名稱的鎖定狀態。該參數有以下取值：<br><br><br>* `on`：表示該網域名稱已被鎖定。<br><br>* `off`：表示該網域名稱未被鎖定。 |`off` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCertConfig&Version=2021-03-01
{
    "CertId": "cert-5dc4bfa90c1048778abf036b03ffabf2",
    "Status": "online,configuring"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202403181420252BCF8FD4581E1A5AAA4E",
        "Action": "DescribeCertConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertNotConfig": [
            {
                "Domain": "abc.example.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            },
            {
                "Domain": "img.example.com.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            }
        ],
        "OtherCertConfig": [
            {
                "CerStatus": "running",
                "Domain": "doc.example.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            }
        ],
        "SpecifiedCertConfig": [
            {
                "CerStatus": "expiring_soon",
                "Domain": "www.example.com",
                "DomainLock": {
                    "Remark": "Domain locked against unauthorized changes. Acting administration on behalf of customer",
                    "Status": "on"
                },
                "Status": "online"
            }
        ]
    }
}
```


&nbsp;
