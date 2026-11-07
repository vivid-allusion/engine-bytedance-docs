---
title: "ListCdnDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnDomains_zh-tw"
---

取得 BytePlus CDN 中的網域名稱清單以及每個網域名稱的基礎資訊，包括業務類型、執行狀態、CNAME 位址、服務區域等。您可以指定篩選條件對網域名稱清單進行篩選。若需要取得詳細的網域名稱設定，請呼叫 [DescribeCdnConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_zh-tw)。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=ListCdnDomains&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `ListCdnDomains`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |否 |表示要查詢的網域名稱，支援模糊比對。 |`example` |
|ServiceType |String |否 |表示一個業務類型，用來對網域名稱進行篩選，取得該業務類型的網域名稱。該參數有以下取值：<br><br><br>* `download`：表示檔案下載。<br><br>* `web`：表示網頁。<br><br>* `video`：表示影音點播。 |`web` |
|ResourceTags |String[] |否 |表示一個標籤清單，用於對網域名稱進行篩選，取得清單中帶有任意標籤的網域名稱。清單中最多可以包含 10 個標籤，每個標籤的格式是 `key:value`。請參閱右邊該參數的範例。 |`["key1:val1","key2:val2"]` |
|Status |String |否 |表示一個網域名稱狀態，用來對網域名稱進行篩選，取得該狀態下的網域名稱。該參數有以下取值：<br><br><br>* `online`：表示狀態是 "在線"。<br><br>* `configuring`：表示狀態是 "設定中"。<br><br>* `offline`：表示狀態是 "離線"。 |`offline` |
|Project |String |否 |表示一個專案，取得歸屬該專案的網域名稱。 |`default` |
|OriginProtocol |String |否 |表示一個協定，取得來源伺服器請求使用該協定的網域名稱。該參數有以下取值：<br><br><br>* `http`：表示 HTTP 協定。<br><br>* `https`：表示 HTTPS 協定。<br><br>* `followclient`：表示使用者請求使用的協定。 |`http` |
|IPv6 |Boolean |否 |表示根據是否啟用了 IPv6 特性來篩選網域名稱。該參數有以下取值：<br><br><br>* `true`: 表示 IPv6 已啟用。<br><br>* `false`: 表示 IPv6 未啟用。 |`true` |
|HTTPS |Boolean |否 |表示根據是否啟用了 HTTPS 加密服務來篩選網域名稱。該參數有以下取值：<br><br><br>* `true`: 表示 HTTPS 加密服務已啟用。<br><br>* `false`: 表示 HTTPS 加密服務未啟用。 |`true` |
|PrimaryOrigin |String |否 |表示一個主來源伺服器，以取得主來源伺服器設定中包含該主來源伺服器的那些網域名稱。該參數值可以是一個 IP 位址，也可以是一個網域名稱。 |`helloworld.example.com` |
|PageNum |Long |否 |表示一個頁碼，用以取得該頁面上網域名稱清單。該參數的預設值為 `1`。<br><br>CDN 對符合篩選條件的網域名稱進行分頁。您可以根據回應參數 `Total` 和請求參數 `PageSize` 計算該 API 回傳的頁數。 |`1` |
|PageSize |Long |否 |表示每頁包含的網域名稱數量。該參數的取值範圍是 1\-100，預設值是 `10`。 |`10` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|PageNum |Long |表示請求參數中的 `PageNum`。 |`1` |
|PageSize |Long |表示請求參數中的 `PageSize`。 |`10` |
|Total |Long |表示符合篩選條件的網域名稱數量。該參數值不受請求參數 `PageSize` 和 `PageNum` 的影響。 |`100` |
|Data |Object[] |表示符合篩選條件的網域名稱清單。 | |
|Domain |String |表示清單中的一個網域名稱。 |`www.example.com` |
|ServiceType |String |表示該網域名稱的業務類型。該參數有以下取值：<br><br><br>* `download`：表示檔案下載。<br><br>* `web`：表示網頁。<br><br>* `video`：表示影音點播。 |`web` |
|Status |String |表示該網域名稱的狀態。該參數有以下取值：<br><br><br>* `online`：表示狀態是 "在線"。<br><br>* `configuring`：表示狀態是 "設定中"。<br><br>* `offline`：表示狀態是 "離線"。 |`online` |
|Cname |String |表示 CDN 分配給該網域名稱的 CNAME。 |`www.example.com.bplslb.com` |
|ServiceRegion |String |表示該網域名稱的服務區域。該參數有以下取值：<br><br><br>* `chinese_mainland`：表示中國大陸。<br><br>* `global`：表示全球。<br><br>* `outside_chinese_mainland`：表示全球（不含中國大陸）。 |`outside_chinese_mainland` |
|CreateTime |Long |表示該網域名稱新增到 CDN 中的時間，格式為 Unix 時間標記。 |`1625587200` |
|UpdateTime |Long |表示該網域名稱最近一次更新的時間，格式是 Unix 時間標記。更新操作包括啟用網域名稱、停用網域名稱、修改網域名稱設定等。 |`1601371409` |
|Project |String |表示該網域名稱所歸屬的專案。 |`default` |
|OriginProtocol |String |表示來源伺服器請求使用的協定。該參數有以下取值：<br><br><br>* `http`：表示 HTTP 協定。<br><br>* `https`：表示 HTTPS 協定。<br><br>* `followclient`：表示使用者請求使用的協定。 |`http` |
|IPv6 |Boolean |表示該網域名稱是否啟用了 IPv6 特性。該參數有以下取值：<br><br><br>* `true`: 表示 IPv6 已啟用。<br><br>* `false`: 表示 IPv6 未啟用。 |`true` |
|HTTPS |Boolean |表示該網域名稱是否啟用了 HTTPS 加密服務。該參數有以下取值：<br><br><br>* `true`: 表示 HTTPS 加密服務已啟用。<br><br>* `false`: 表示 HTTPS 加密服務未啟用。 |`true` |
|PrimaryOrigin |String[] |表示該網域名稱設定的主來源伺服器清單。 |`"xxx.xx.xxx.xx","helloworld1.example.com"` |
|BackupOrigin |String[] |表示該網域名稱設定的備用來源伺服器清單。如果該網域名稱沒有設定任何備用來源伺服器，該參數值是 `null`。 |`"xxx.xx.xxx.xx","helloworld2.example.com"` |
|ResourceTags |Object[] |表示該網域名稱帶的標籤清單。如果該網域名稱沒有帶任何標籤，該參數值是 `null`。 | |
|Key |String |表示標籤清單中一個標籤的 key。 |`userKey` |
|Value |String |表示該標籤的 value。 |`userValue` |
|CacheShared |String |表示該網域名稱在共用快取設定中的角色。該參數有以下取值：<br><br><br>* `target_host`：表示存在一個共용快取設定，在該設定中該網域名稱的角色是目標網域名稱。<br><br>* `cache_shared_on`：表示存在一個共用快取設定，在該設定中該網域名稱的角色是被設定的網域名稱。<br><br>* `""`：該參數值為空，表示該網域名稱不存在於任何共用快取設定中。 |`cache_shared_on` |
|CacheSharedTargetHost |String |如果`CacheShared` 是 `cache_shared_on`，表示與該網域名稱共用快取的目標網域名稱。如果`CacheShared` 是 `target_host` 或者是空值（""），該參數值是空（""）。 |`www.example.net` |
|Waf |Boolean |表示該網域名稱是否啟用了 WAF 防護。該參數有以下取值：<br><br><br>* `true`：表示已啟用了 WAF 防護。<br><br>* `false`：表示未啟用 WAF 防護。 |`false` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=ListCdnDomains&Version=2021-03-01
{
    "Domain": "example",
    "ResourceTags": [
        "key1:val1",
        "key2:val2"
    ]
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20250821112545F5890E6D640605A33280",
        "Action": "ListCdnDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "BackupOrigin": [
                    "203.0.113.9",
                    "img2.example.com"
                ],
                "CacheShared": "",
                "CacheSharedTargetHost": "",
                "Cname": "www.example.com.bplslb.com",
                "CreateTime": 1755585663,
                "Domain": "www.example.com",
                "HTTPS": true,
                "IPv6": true,
                "OriginProtocol": "https",
                "PrimaryOrigin": [
                    "203.0.113.8",
                    "img.example.com",
                    "bpcntest.tos-ap-southeast-3.bytepluses.com",
                    "mybucket.oss-ap-southeast-1.aliyuncs.com",
                    "mybucket.cos.ap-singapore.myqcloud.com",
                    "my-bucket.s3.ap-southeast-1.amazonaws.com",
                    "myazstorage.blob.core.windows.net"
                ],
                "Project": "default",
                "ResourceTags": [
                    {
                        "Key": "mykey",
                        "Value": "myvalue"
                    }
                ],
                "ServiceRegion": "outside_chinese_mainland",
                "ServiceType": "web",
                "Status": "online",
                "UpdateTime": 1755585663,
                "Waf": false
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
