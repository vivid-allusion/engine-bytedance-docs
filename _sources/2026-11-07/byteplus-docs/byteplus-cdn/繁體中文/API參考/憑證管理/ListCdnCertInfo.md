---
title: "ListCdnCertInfo"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCdnCertInfo_zh-tw"
---

獲取符合篩選條件的憑證清單以及這些憑證所關聯的網域名稱清單。

如果是子用戶調用該 API，清單中的網域名稱是該子用戶有權限訪問的。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=ListCdnCertInfo&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `ListCdnCertInfo`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|CertId |String |否 |表示一個憑證的 ID，獲取該 ID 的憑證。<br><br>您可以使用 [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCertInfo_zh-tw) 獲取您想要指定的憑證的 ID。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|ConfiguredDomain |String |否 |表示一個網域名稱清單，用於獲取清單中每個網域名稱所關聯的憑證。多個網域名稱之間使用逗號（,）分隔。<br><br>清單中可以包含泛網域名稱。但是需要留意的是，對於泛網域名稱，只有當一個憑證所關聯網域名稱中包含該泛網域名稱，該憑證才算符合 `ConfiguredDomain` 這個篩選條件。例如，您指定的 `ConfiguredDomain` 是 `*.example.com`。如果一個憑證所關聯的網域名稱中有 `www.example.com`，但沒有 `*.example.com`，那麼該憑證不符合這個篩選條件。 |`www.example.com,*.test.com` |
|DnsName |String |否 |表示一個網域名稱清單，獲取 SAN 欄位中包含清單中任一網域名稱的憑證。多個網域名稱之間使用逗號（,）分隔。<br><br>清單中可以包含泛網域名稱。但是需要留意的是，對於泛網域名稱，只有當一個憑證的 SAN 欄位中包含該泛網域名稱，該憑證才算符合 `DnsName` 這個篩選條件。例如，您指定的 `DnsName` 是 `*.example.com`。如果一個憑證的 SAN 欄位中有 `www.example.com`，但沒有 `*.example.com`，那麼該憑證不符合這個篩選條件。 |`*.example.com,www.test.com` |
|PageNum |Long |否 |對於 API 回應的憑證清單，該參數表示一個頁碼。該 API 實際回應的憑證清單是該頁碼所指定的分頁上的那些憑證。<br><br>該 API 回應的憑證是根據 `PageSize` 而分頁的。假設該 API 回應的憑證數量是 100，您指定的 `PageSize` 是 `10`，那麼回應的憑證是分布在 10 個頁上。如果您指定的 `PageNum` 是 `2`，表示獲取第 2 頁上的那些憑證。<br><br>如果您指定的分頁上沒有憑證，則回應結果中 `CertInfo` 參數的值為 `null`。<br><br>`PageNum` 的預設值是 `1`。 |`1` |
|PageSize |Long |否 |表示每個分頁包含的憑證數量。<br><br>該參數的取值範圍是 1\-100，預設值是 `10`。 |`10` |
|Source |String |否 |表示憑證的儲存位置，獲取儲存在該位置的憑證。目前，該參數值只能是 `cert_center`，表示 BytePlus 憑證中心。 |`cert_center` |
|Status |String |否 |表示一個憑證狀態的清單，獲取處於清單中任一狀態下的憑證。該參數有以下取值：<br><br><br>* `running`：表示該憑證的有效期大於 30 天。<br><br>* `expired`：表示該憑證已經過期。<br><br>* `expiring_soon`：表示該憑證的有效期小於等於 30 天，但還未過期。<br><br><br>多個憑證狀態使用逗號（,）分隔。 |`running,expird` |
|Configured |Boolean |否 |表示在該 API 回應的 `CertInfo` 中，是否移除未與任何網域名稱關聯的憑證。該參數有以下取值：<br><br><br>* `true`：表示移除未與任何網域名稱關聯的憑證。<br><br>* `false`：表示保留未與任何網域名稱關聯的憑證。<br><br><br>該參數的預設值是 `true`。 |`true` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|PageNum |Long |表示請求參數中 `PageNum` 的值。 |`1` |
|PageSize |Long |表示請求參數中 `PageSize` 的值。 |`10` |
|Total |Long |表示符合篩選條件的憑證數量。該參數值不受 `PageNum` 和 `PageSize` 的影響。 |`8` |
|CertInfo |Object[] |表示符合篩選條件的憑證清單。如果沒有符合篩選條件的憑證，該參數值為 `null`。 | |
|Source |String |對於回應的憑證清單中的一個憑證，該參數表示該憑證的儲存位置。目前，該參數值是 `cert_center`，表示 BytePlus 憑證中心。 |`cert_center` |
|CertId |String |表示該憑證的 ID。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|CertName |String |表示該憑證的 `Common Name (CN)` 欄位中的內容。 |`*.example.com` |
|Status |String |表示該憑證的狀態。該參數有以下取值：<br><br><br>* `running`：表示該憑證的有效期大於 30 天。<br><br>* `expired`：表示該憑證已經過期。<br><br>* `expiring_soon`：表示該憑證的有效期小於等於 30 天，但還未過期。 |`running` |
|EffectiveTime |Long |表示該憑證的簽發時間。單位是 Unix 時間戳記。 |`1655856000` |
|ExpireTime |Long |表示該憑證的過期時間。單位是 Unix 時間戳記。 |`1687478399` |
|DnsName |String |表示該憑證的 SAN 欄位中的那些網域名稱，多個網域名稱之間使用逗號（,）分隔。 |`*.example.com,www.test.com` |
|ConfiguredDomain |String |表示已與該憑證關聯的網域名稱清單。多個網域名稱之間使用逗號（,）分隔。<br><br>如果請求參數 `Configured` 是 `false` 並且該憑證未關聯任何網域名稱，那麼該參數值為 `null`。 |`www.example.com,abc.example.com,img.example.com` |
|Desc |String |表示該憑證的備註。 |`Test` |
|CertFingerprint |Object |表示該憑證的指紋資訊。 | |
|Sha1 |String |表示一個基於 SHA\-1 加密演算法的指紋，由 40 個十六進位字元組成。 |`4f6c4bd5402e8f848837bf1334740ece0671ae4d` |
|Sha256 |String |表示一個基於 SHA\-256 加密演算法的指紋，由 64 個十六進位字元組成。 |`24e49e0888f91a25f1503b452aa7cf0cf30da637810eaee5309b0be6c3931c9d` |
|ExpiringCount |Long |表示在符合篩選條件的憑證中，狀態是 `expiring_soon` 的憑證數量。但是，目前該參數還未生效，因此該參數值始終是 `0`。 |`0` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=ListCdnCertInfo&Version=2021-03-01
{
    "CertId": "cert-602fc4eb6cbf4b9351b54bedf2bc5dc5",
    "ConfiguredDomain": "www.example.com,*.test.com",
    "DnsName": "*.example.com,www.test.com",
    "Status": "running,expiring_soon",
    "Configured": true
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2024031811030837EB957CFE06970AC404",
        "Action": "ListCdnCertInfo",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertInfo": [
            {
                "CertId": "cert-602fc4eb6cbf4b9351b54bedf2bc5dc5",
                "CertName": "*.example.com",
                "ConfiguredDomain": "*.example.com",
                "Desc": "Test",
                "DnsName": "*.example.com",
                "EffectiveTime": 1694415266,
                "ExpireTime": 1725951266,
                "Source": "cert_center",
                "Status": "running"
            }
        ],
        "ExpiringCount": 0,
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
