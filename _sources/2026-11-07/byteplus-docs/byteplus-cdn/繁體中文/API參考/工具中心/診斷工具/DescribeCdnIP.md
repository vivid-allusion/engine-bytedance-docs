---
title: "DescribeCdnIP"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_zh-tw"
---

查詢指定的一個或者多個 IP 位址是否是 CDN 伺服器的 IP 位址。CDN 伺服器涵蓋邊緣伺服器和區域伺服器。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">該 API 替換了 DescribeIPListInfo。</div>


<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeCdnIP&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeCdnIP`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|IPs |String[] |是 |表示待查詢的 IP 位址列表。列表中最多可以包含 50 個 IP 位址。 |`["xx.xxx.xxx.102", "xxx.xxx.234.67"]` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|IPs |Object[] |表示請求參數中的 IP 位址列表。 | |
|IP |String |表示 IP 位址列表中的一個 IP 位址。 |`xx.xxx.xxx.102` |
|CdnIp |Boolean |表示該 IP 位址是否是某個 CDN 邊緣伺服器的 IP 位址。該參數有以下取值：<br><br><br>* `true`：表示該 IP 位址是某個 CDN 邊緣伺服器的 IP 位址。<br><br>* `false`：表示該 IP 位址不是任何 CDN 邊緣伺服器的 IP 位址。 |`false` |
|ISP |String |表示該 IP 位址歸屬的網路運營商（ISP）。<br><br><br>* 如果 `CdnIp` 是 `false`，該參數值為空（""）。<br><br>* 如果 `CdnIp` 是 `true` 但是 CDN 未獲取該 IP 位址歸屬的網路運營商，該參數值是 `DEFAULT`。 |`DEFAULT` |
|Location |String |表示該 IP 位址歸屬的國家或地區。如果 `CdnIp` 是 `false`，該參數值為空（""）。 |`United States-Florida-Florida` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnIP&Version=2021-03-01
{
    "IPs": [
        "xxx.xxx.xx.139",
        "xxx.xx.xx.34"
    ]
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2024101011033668CF51ECED9C5477E3C6",
        "Action": "DescribeCdnIP",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "IPs": [
            {
                "CdnIp": true,
                "IP": "xxx.xxx.xx.139",
                "ISP": "DEFAULT",
                "Location": "Singapore-Singapore-Singapore"
            },
            {
                "CdnIp": false,
                "IP": "xxx.xx.xx.34",
                "ISP": "",
                "Location": ""
            }
        ]
    }
}
```


&nbsp;
