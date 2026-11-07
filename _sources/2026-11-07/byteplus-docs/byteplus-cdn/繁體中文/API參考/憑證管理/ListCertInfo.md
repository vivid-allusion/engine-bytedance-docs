---
title: "ListCertInfo"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCertInfo_zh-tw"
---

獲取符合篩選條件的憑證資訊。該 API 獲取的憑證是儲存在 BytePlus 憑證中心，並且能與或者已經與您帳號下的網域關聯的憑證。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=ListCertInfo&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `ListCertInfo`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Source |String |是 |表示憑證儲存的位置。目前該參數值只能是 `cert_center`，指 BytePlus 憑證中心。 |`cert-center` |
|CertId |String |否 |表示一個憑證 ID，獲取該 ID 的憑證。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|ConfiguredDomain |String |否 |表示一個網域名稱清單，獲取已與清單中任何一個網域名稱綁定的憑證。 |`www.example.com,www.test.com` |
|FuzzyMatch |Boolean |否 |當您指定了 `Name` 時，`FuzzyMatch` 表示在使用 `Name` 篩選憑證時，CDN 使用的匹配方式。該參數有以下取值：<br><br><br>* `true`：表示模糊匹配。<br><br>* `false`：表示精確匹配。<br><br><br>如果您未指定 `Name`，`FuzzyMatch` 無效。<br><br>`FuzzyMatch` 的預設值是 `false`。 |`true` |
|Name |String |否 |表示一個網域名稱，用於獲取那些在 SAN 欄位中包含該網域名稱的憑證。該網域名稱可以是泛網域名稱。例如，指定 `*.example.com` 表示獲取 SAN 欄位中包含 `img.example.com` 或 `www.example.com` 等匹配該泛網域名稱的憑證。 |`*.example.com` |
|PageNum |Long |否 |對於符合篩選條件的憑證清單，該參數表示一個頁碼，該 API 實際顯示的憑證是該頁碼所指定的分頁上的那些憑證。<br><br>該 API 回傳的憑證是根據 `PageSize` 而分頁的。假設該 API 回傳的憑證數量是 100，您指定的 `PageSize` 是 `10`，那麼回傳的憑證是分布在 10 個頁上。如果您指定的 `PageNum` 是 `2`，表示獲取第 2 頁上的那些憑證。<br><br>如果您指定的分頁上沒有憑證，則回傳結果中 `CertInfo` 參數的值為 `null`。<br><br>`PageNum` 的預設值是 `1`。 |`1` |
|PageSize |Long |否 |表示每頁包含的憑證數量。<br><br>該參數的取值範圍是 1\-100，預設值是 `10`。 |`10` |
|Status |String |否 |表示一個狀態清單，獲取處於清單中任意一個狀態下的憑證。多個狀態之間使用逗號（,）分隔。該參數有以下取值：<br><br><br>* `running`：表示有效期大於 30 天的那些憑證。<br><br>* `expired`：表示已過期的那些憑證。<br><br>* `expiring_soon`：表示有效期小於等於 30 天但還未過期的那些憑證。 |`expired,running` |
|SortRule |Object |否 |表示一個排序規則，對該 API 回傳的憑證進行排序。預設規則是按回應中的 `ExpireTime` 參數對回傳的憑證進行升冪排序。 | |
|Asc |Boolean |否 |表示排序的方式。該參數有以下取值：<br><br><br>* `false`：表示對清單中的憑證進行降冪排列。<br><br>* `true`：表示對清單中的憑證進行升冪排列。<br><br><br>該參數的預設值是 `true`。 |`false` |
|OrderBy |String |否 |表示回傳的憑證按哪個欄位進行排序。如果您指定了 SortRule，`OrderBy` 是必填。目前 `OrderBy` 的值必須是 `ExpireTime`，表示按憑證的到期時間進行排序。 |`ExpireTime` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|PageNum |Long |表示您在請求參數中指定的 `PageNum`。 |`1` |
|PageSize |Long |表示您在請求參數中指定的 `PageSize`。 |`10` |
|Total |Long |表示符合篩選條件的憑證數量。該參數值不受 `PageSize` 和 `PageNum` 的影響。 |`2` |
|CertInfo |Object[] |表示該 API 回傳的憑證清單。<br><br>需要留意的是，清單中的憑證是請求參數 `PageNum` 所表示的分頁上的那些憑證，不一定是所有符合篩選條件的憑證。 | |
|Source |String |對於回傳的憑證清單中的一個憑證，該參數表示該憑證儲存的位置，有以下取值：<br><br><br>* `cert_center`：表示 BytePlus 憑證中心。 |`cert_center` |
|CertId |String |表示該憑證的 ID。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|CertName |String |表示該憑證的 `Common Name (CN)` 欄位中的內容。 |`*.example.com` |
|Status |String |表示該憑證的狀態。該參數有以下取值：<br><br><br>* `running`：表示該憑證的有效期大於 30 天。<br><br>* `expired`：表示該憑證已經過期。<br><br>* `expiring_soon`：表示該憑證的有效期小於等於 30 天，但還未過期。 |`running` |
|EffectiveTime |Long |表示該憑證的簽發時間。單位是 Unix 時間戳。 |`1655856000` |
|ExpireTime |Long |表示該憑證的到期時間。單位是 Unix 時間戳。 |`1687478399` |
|DnsName |String |表示該憑證的 `SAN` 欄位中包含的那些網域名稱。多個網域名稱之間使用逗號（,）分隔。 |`www.test.com,*.example.com` |
|Desc |String |表示該憑證的備註。 |`Test` |
|ConfiguredDomain |String |表示已與該憑證關聯的網域名稱清單。如果該憑證還未與任何網域名稱關聯，該參數值為 `null`。 |`www.example.com, www.test.com` |
|CertFingerprint |Object |表示該憑證的指紋資訊。 | |
|Sha1 |String |表示一個基於 SHA\-1 加密演算法的指紋，由 40 個十六進位字元組成。 |`4f6c4bd5402e8f848837bf1334740ece0671ae4d` |
|Sha256 |String |表示一個基於 SHA\-256 加密演算法的指紋，由 64 個十六進位字元組成。 |`24e49e0888f91a25f1503b452aa7cf0cf30da637810eaee5309b0be6c3931c9d` |
|ExpiringCount |Long |表示在符合篩選條件的憑證中，狀態是 `expiring_soon` 的憑證數量。但是，目前該參數還未生效，因此該參數值始終是 `0`。 |`0` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=ListCertInfo&Version=2021-03-01
{
    "Source": "cert_center",
    "Name": "www.example.com",
    "Status": "running,expired",
    "SortRule": {
        "Asc": false,
        "OrderBy": "ExpireTime"
    }
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20240315094304D1302166C42C534627B0",
        "Action": "ListCertInfo",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertInfo": [
            {
                "CertId": "cert-7b94354335aa424993ce48fa355f1e5e",
                "CertName": "www.example.com",
                "ConfiguredDomain": "www.example.com",
                "Desc": "Test",
                "DnsName": "www.example.com",
                "EffectiveTime": 1708992000,
                "ExpireTime": 1740700799,
                "Source": "cert_center",
                "Status": "running"
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
