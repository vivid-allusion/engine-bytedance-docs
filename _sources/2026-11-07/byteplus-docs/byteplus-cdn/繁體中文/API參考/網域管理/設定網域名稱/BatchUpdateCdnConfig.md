---
title: "BatchUpdateCdnConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/BatchUpdateCdnConfig_zh-tw"
---

在 BytePlus CDN 對多個網域名稱的設定進行更新。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您無法更新 <code>Status</code> 是 <code>offline</code> 的網域名稱。要取得一個網域名稱的狀態，請呼叫 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_zh-tw">DescribeCdnConfig</a>。</div>


<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=BatchUpdateCdnConfig&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `BatchUpdateCdnConfig`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body

<span id="基礎設定"></span>
## 基礎設定

<span id="網域"></span>
### 網域


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domains |String[] |是 |表示待更新的網域名稱清單，最多包含 50 個網域名稱。 |`["abc.example.com","zzz.example.com"]` |


<span id="aggregate"></span>
### Aggregate


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Aggregate |Boolean |否 |該參數的作用如下：<br><br><br>* 決定是否在 API 的回應中展示每個網域名稱的設定更新結果。<br><br>* 當 CDN 無法更新 `Domains` 清單中某個網域名稱的設定時，CDN 的行為。<br><br><br>該參數有以下取值：<br><br><br>* `true`：表示 API 的回應中不展示每個網域名稱的設定更新結果。另外，如果 CDN 無法更新一個網域名稱的設定，該 API 會放棄更新所有網域名稱的設定，並且回應正文會包含 `Error` 結構體。該結構體中包含的是設定更新失敗的網域名稱的錯誤資訊。參見範例 1。<br><br>* `false`：表示 API 的回應中展示每個網域名稱的設定更新結果。回應正文會包含 `DeployResult` 結構體。該結構體包含的是每個網域名稱的設定更新結果。參見範例 2。另外，如果 CDN 無法更新一個網域名稱的設定，CDN 會繼續更新其他網域名稱的設定。<br><br><br>該參數的預設值是 `true`。 |`false` |


<span id="ipv6"></span>
### IPv6


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|IPv6 |Object |否 |表示 IPv6 設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |


<span id="來源伺服器設定"></span>
### 來源伺服器設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Origin |Object[] |否 |表示來源伺服器設定。 | |
|OriginAction |Object |是 |表示來源伺服器設定，應用於所有使用者請求。 | |
|OriginLines |Object[] |是 |表示一個來源伺服器列表。列表中最多可以包含 50 個來源伺服器。 | |
|Address |String |是 |表示清單中一個來源伺服器的位址。該參數有以下說明：<br><br><br>* 如果 `InstanceType` 是 `ip`，您指定的是來源伺服器的 IP 位址。IP 位址可以是 IPv4 或 IPv6 位址。<br><br>* 如果 `InstanceType` 是 `domain`，您指定的是來源伺服器的網域名稱。該網域名稱不能是泛網域，也不能與該策略要繫結的網域名稱相同。<br><br>* 如果 `InstanceType` 是 `tos`，您指定的是儲存桶網域名稱。可以是雲端廠商分配的桶網域名稱，也可以是您在雲端廠商處為儲存桶設定的自訂網域名稱。桶網域名稱不能包含 `https://` ，長度不能超過 100 個字元。儲存桶可以來自 BytePlus TOS、阿里雲 OSS、騰訊雲 COS、AWS S3 或任何使用與 S3 相容的驗證方式的第三方物件儲存服務。<br><br><br>说明<br><br><br>* 如果儲存桶來自您帳戶下的 TOS 服務，在呼叫該 API 前，您需要在 CDN 控制台中開啟該網域名稱的設定頁面。在該頁面中，點擊 授權 CDN 存取您帳戶下的 TOS 服務。<br><br>* 在 Azure Blob Storage 中，物件儲存桶稱為 container。 |`www.example.com` |
|InstanceType |String |是 |表示來源伺服器的類型。該參數有以下取值：<br><br><br>* `ip`：表示 IP 位址。<br><br>* `domain`：表示網域名稱。<br><br>* `tos`：表示物件儲存桶。<br><br><br>注意<br><br>在 CDN 向物件儲存來源伺服器傳送來源伺服器請求時，來源伺服器請求使用的方法與使用者請求相同。預設情況下，使用者請求可以使用的請求方法有 DELETE、GET、HEAD、POST、PUT、PATCH、OPTIONS、CONNECT。如果您不希望來源伺服器請求使用某些請求方法，例如您不希望來源伺服器請求使用 DELETE 方法，可能導致誤刪來源伺服器上的檔案，建議您採取以下步驟：<br><br><br>1. 在儲存桶所在的物件儲存服務中設定權限，組織不符合預期的操作。<br><br>2. 在 CDN 的 `MethodDeniedRule` 特性中，指定 CDN 不支援的請求方法。 |`ip` |
|OriginType |String |是 |表示該來源伺服器的類別。該參數有以下取值：<br><br><br>* `primary`：表示主來源伺服器。<br><br>* `backup`：表示備用來源伺服器。<br><br><br>來源伺服器列表中至少需要包含一個主來源伺服器。備用來源伺服器是可選的。 |`primary` |
|HttpPort |String |否 |表示 CDN 使用 HTTP 協定存取該來源伺服器時所存取的連接埠，取值範圍是 1\-65535，預設值是 `80`。如果來源伺服器沒有開放該連接埠，您無需指定該參數。<br><br>該參數僅當 `InstanceType` 為 `ip` 或 `domain` 時才有效。 |`80` |
|HttpsPort |String |否 |表示 CDN 使用 HTTPS 協定存取該來源伺服器時所存取的連接埠，取值範圍是 1\-65535，預設值是 `443`。如果來源伺服器沒有開放該連接埠，您無需指定該參數。<br><br>該參數僅當 `InstanceType` 為 `ip` 或 `domain` 時才有效。 |`443` |
|OriginHost |String |否 |表示來源伺服器請求存取的站點網域名稱，適用於來源伺服器上有多個站點的情況。<br><br><br>* 該參數的預設值與全域 `OriginHost` 相同，但優先順序高於全域 `OriginHost` 參數。<br><br>* 該參數值的長度不能超過 1,024 個字元。<br><br>* 如果您在呼叫該 API 時，既沒有修改 `Address`，也沒有指定 `OriginHost`， `OriginHost` 不會被預設值覆寫，而是保持目前值。 |`img.example.com` |
|PrivateBucketAccess |Boolean |否 |表示儲存桶是否為私有桶。此參數僅在 `InstanceType` 為 `tos` 時有效。此參數的可選值如下：<br><br><br>* `true`：表示該儲存桶為私有桶。<br><br>* `false`：表示該儲存桶不是私有桶。<br><br><br>此參數的預設值為 `false`。 |`false` |
|PrivateBucketAuth |Object |否 |表示存取儲存桶的驗證設定。<br><br>说明<br><br>若儲存桶為本帳號下的 TOS 儲存桶，且您希望使用跨服務授權方式存取 TOS 儲存桶，則無需指定此參數。跨服務授權存取方式無需指定 AccessKey。 | |
|Switch |Boolean |是 |表示存取儲存桶是否需要憑證。該參數有以下取值：<br><br><br>* `true`：表示需要憑證。<br><br>* `false`：表示無需憑證。 |`false` |
|AuthType |String |否 |表示儲存桶使用的是哪個物件儲存服務所提供的驗證方式。此參數的可選值如下：<br><br><br>* `tos`：表示 BytePlus TOS，您使用 AccessKey 存取 TOS 儲存桶。<br><br>* `cos`：表示騰訊雲 COS。<br><br>* `oss`：表示阿里雲 OSS。<br><br>* `azure`：表示 Microsoft Azure。<br><br>* `aws_common`：表示 AWS S3 及相容 S3 的驗證方式。 |`cos` |
|TosAuthInformation |Object |否 |表示儲存桶的存取憑證（AccessKey）。 | |
|AccessKeyId |String |否 |表示存取憑證中的 AccessKey ID，在騰訊雲中稱為 SecretId，長度為 5\-100 個字元。 |`xxxxxxxx` |
|AccessKeySecret |String |否 |表示存取憑證中的 AccessKey Secret，在騰訊雲中稱為 SecretKey，長度為 5\-100 個字元。 |`xxxxxx` |
|AccountKey |String |否 |表示您 Azure 儲存帳戶的共用金鑰（Key）。該參數僅當 `AuthType` 為 `azure` 時有效。 |`xxxxxx` |
|Region |String |否 |表示儲存桶所在地域的資訊，也就是儲存桶的 region code。Region code 參與簽名的計算。<br><br>如果 `AuthType` 是 `aws_common` 並且 `PrivateBucketAccess` 是 `true`，您必須指定該參數。 |`us-east-1` |
|Weight |String |否 |表示該來源伺服器的權重，取值範圍是 1\-100，預設值是 `1`。權重越大，該來源伺服器在 CDN 傳送來源伺服器請求時被選擇到的機率也越大。<br><br>該參數僅當 `InstanceType` 為 `ip` 或 `domain` 時才有效。 |`100` |
|BucketName |String |否 |表示您 Azure 儲存帳戶的名稱。該參數僅當 `AuthType` 為 `azure` 時有效。 |`mystorageaccount` |


<span id="條件來源伺服器"></span>
### 條件來源伺服器


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ConditionalOrigin |Object |否 |表示 "條件源站" 特性的設定。 | |
|OriginRules |Object[] |否 |表示一個規則清單。清單中的每條規則中定義了一組比對條件以及 CDN 對滿足比對條件的請求所執行的操作。<br><br>清單中最多可以包含 20 條規則。<br><br>當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|Actions |Object |否 |表示一條規則中定義的操作設定。 | |
|OriginLines |Object[] |否 |表示一個源站清單。目前，清單中只能包含一個源站。 | |
|Address |String |否 |表示一個源站的位址。<br><br><br>* 當 `InstanceType` 是 `ip` 時，`Address` 表示一個 IPv4 或 IPv6 位址。<br><br>* 當 `InstanceType` 是 `domain` 時，`Address` 表示一個網域名稱。該網域名稱不能是泛網域名稱。<br><br>* 如果 `InstanceType` 是 `storage`，您指定的是儲存桶網域名稱，可以是雲端廠商分配的桶網域名稱，也可以是您在雲端廠商處為儲存桶設定的自訂網域名稱。桶網域名稱不能包含 `https://`，長度不能超過 100 個字元。儲存桶可以來自火山引擎 TOS、阿里雲 OSS、騰訊雲 COS、AWS S3 或任何使用鑑權方式與 S3 相容的第三方物件儲存服務，如七牛雲、華為雲等。 |`203.0.113.8` |
|HttpPort |String |否 |表示 CDN 使用 HTTP 協定存取該源站時所使用的連接埠，取值範圍是 1\-65535，預設值是 `80`。如果源站伺服器沒有開放該連接埠，您無需指定該參數。 |`80` |
|HttpsPort |String |否 |表示 CDN 使用 HTTPS 協定存取該源站時所使用的連接埠，取值範圍是 1\-65535，預設值是 `443`。如果源站伺服器沒有開放該連接埠，您無需指定該參數。 |`443` |
|InstanceType |String |否 |表示源站的類型。該參數有以下取值：<br><br><br>* `ip`：表示 IP 位址。<br><br>* `domain`：表示網域名稱。<br><br>* `storage`：表示物件儲存桶。<br><br><br>注意<br><br>在 CDN 向物件儲存源站傳送回源請求時，回源請求使用的方法與使用者請求相同。預設情況下，使用者請求可以使用的請求方法有 DELETE、GET、HEAD、POST、PUT、PATCH、OPTIONS、CONNECT。如果您不希望回源請求使用某些請求方法，例如您不希望回源請求使用 DELETE 方法，可能導致誤刪源站上的檔案，建議您採取以下步驟：<br><br><br>1. 在儲存桶所在的物件儲存服務中設定權限，組織不符合預期的操作。<br><br>2. 在 CDN 的 `MethodDeniedRule` 特性中，指定 CDN 不支援的請求方法。 |`ip` |
|OriginHost |String |否 |表示回源請求存取的站點網域名稱，適用於源站伺服器上有多個站點的情況。<br><br><br>* 該參數的預設值與全域 `OriginHost` 相同，但優先順序高於全域 `OriginHost` 參數。<br><br>* 該參數值的長度不能超過 1,024 個字元。<br><br>* 如果您在呼叫該 API 時，既沒有修改 `Address`，也沒有指定 `OriginHost`，`OriginHost` 不會被預設值覆寫，而是保持目前值。 |`img.example.com` |
|BucketSource |String |否 |表示儲存桶使用的是哪個物件儲存服務所提供的驗證方式。此參數的可選值如下：<br><br><br>* `tos`：表示 BytePlus TOS。<br><br>* `cos`：表示騰訊雲 COS。<br><br>* `oss`：表示阿里雲 OSS。<br><br>* `azure`：表示 Microsoft Azure。<br><br>* `aws_common`：表示 AWS S3 及相容 S3 的驗證方式。 |`aws_common` |
|PrivateBucketAccess |Boolean |否 |表示儲存桶是否為私有桶。此參數僅在 `InstanceType` 為 `storage` 時有效。此參數的可選值如下：<br><br><br>* `true`：表示該儲存桶為私有桶。<br><br>* `false`：表示該儲存桶不是私有桶。<br><br><br>此參數的預設值為 `false`。 |`true` |
|TosAuthInformation |Object |否 |表示存取儲存桶的驗證設定。<br><br>说明<br><br>若儲存桶為本帳號下的 TOS 儲存桶，且您希望使用跨服務授權方式存取 TOS 儲存桶，則無需指定此參數。跨服務授權存取方式無需指定 AccessKey。 | |
|AccessKeyId |String |否 |表示存取憑證中的 AccessKey ID，在騰訊雲中稱為 SecretId。 |`xxxxxxxxx` |
|AccessKeySecret |String |否 |表示存取憑證中的 AccessKey Secret，在騰訊雲中稱為 SecretKey。 |`xxxxxx` |
|Region |String |否 |表示儲存桶所在地域的資訊，也就是儲存桶的 region code。Region code 參與簽名的計算。<br><br>如果 `BucketSource` 是 `aws_common` 並且 `PrivateBucketAccess` 是 `true`，您必須指定該參數。 |`ap-southeast-1` |
|AccountName |String |否 |表示您 Azure 儲存帳戶的共用金鑰（Key）。該參數僅當 `BucketSource` 為 `azure` 時有效。 |`xxxxxxxxxxxxxxxxxxxx` |
|Condition |Object |否 |表示該規則中比對條件的設定。 | |
|ConditionGroups |Object[] |否 |表示一個比對條件清單。清單中可以包含最多 50 個比對條件。 | |
|Condition |Object |否 |表示一個比對條件的設定。 | |
|Object |String |否 |表示一個比對物件。該參數有以下取值：<br><br><br>* `path`：表示請求 URL 中的完整路徑。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `full_querystring`：表示請求 URL 中的所有查詢參數。<br><br>* `client_ip`：表示用戶端的 IP 位址。<br><br>* `query_name`：表示請求 URL 中的某個查詢參數。<br><br>* `customize`：表示使用者請求中的某個標頭。 |`path` |
|Operator |String |否 |表示比對類型。對於每個 `Object`，可指定的 `Operator` 如下所示：<br><br><br>* `path`：可指定 `equal`、`not_equal`、`regex_match`、`regex_not_match`。<br><br>* `directory`：可指定 `equal`、`not_equal`。<br><br>* `filetype`：可指定 `equal`、`not_equal`。<br><br>* `full_querystring`：可指定 `regex_match`、`regex_not_match`。<br><br>* `client_ip`：可指定 `equal`、`not_equal`、`belong`、`not_belong`。<br><br>* `query_name`：可指定 `equal`、`not_equal`、`regex_match`、`regex_not_match`、`exist`、`not_exist`、`empty`、`not_empty`。<br><br>* `customize`：可指定 `equal`、`not_equal`、`empty`、`not_empty`。<br><br><br>在以上取值中，`belong` 和 `not_belong` 的說明如下：<br><br><br>* `belong`：表示如果用戶端 IP 位址歸屬地在 `Value` 所表示國家和地區清單中，該請求就滿足這個比對條件。<br><br>* `not_belong`：表示如果用戶端 IP 位址歸屬地不在 `Value` 所表示國家和地區清單中，該請求才滿足這個比對條件。 |`equal` |
|Value |String[] |否 |表示一個或多個比對值，多個比對值之間以分號（;）分隔。但是當 `Object` 是 `customize` 時，多個標頭值之間以豎線（\\|）分隔。關於設定值的輸入要求，參見 [主控台說明文件](https://docs.byteplus.com/en/docs/byteplus-cdn/conditional-origin-server_zh-tw)。<br><br>说明<br><br>當 `Object` 是 `client_ip` 並且 `Operator` 是 `belong` 或 `not_belong` 時，比對值是一個或多個國家或地區的代號。您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw)，以獲取 CDN 支援的所有國家和地區的代號。在呼叫 `DescribeCdnRegionAndIsp` 時，請指定請求參數 `Area` 為 `Global`。 |`/www/img/my*image.png;/doc` |
|Name |String |否 |* 當 `Object` 為 `query_name` 時，該參數表示指定的查詢參數的名稱。<br><br>* 當 `Object` 為 `customize` 時，該參數表示指定的請求標頭的名稱。<br><br>* 當 `Object` 為其他值時，該參數無需指定。 |`myparam` |
|Type |String |否 |* 當 `Object` 為 `query_name` 時，該參數值必須是 `querystring`。<br><br>* 當 `Object` 為 `customize` 時，該參數值必須是 `request_header`。<br><br>* 當 `Object` 為其他值時，該參數無需指定。 |`request_header` |
|Connective |String |否 |表示這些比對條件之間的關係。該參數有以下取值：<br><br><br>* `or`：表示關係是 "或"。<br><br>* `and`：表示關係是 "與"。<br><br><br>該參數的預設值是 `or`。 |`and` |
|IsGroup |Boolean |否 |該參數值必須是 `true`。 |`true` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="來源伺服器請求協定"></span>
### 來源伺服器請求協定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginProtocol |String |是 |表示來源伺服器請求使用的協定。該參數有以下取值：<br><br><br>* `http`：表示來源伺服器請求使用 HTTP 協定。<br><br>* `https`：表示來源伺服器請求使用 HTTPS 協定。<br><br>* `followclient`：表示來源伺服器請求協定與使用者請求使用的協定相同。 |`http` |


<span id="ipv6-來源伺服器請求"></span>
### IPv6 來源伺服器請求


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginIPv6 |String |否 |表示「IPv6 來源伺服器請求」的設定。該參數有以下取值：<br><br><br>* `ipv6_first` ：表示 CDN 始終嘗試獲取來源伺服器網域名稱的 IPv6 位址。如果無法獲取該 IP 位址，CDN 才會嘗試獲取來源伺服器網域名稱的 IPv4 位址。<br><br>* `ipv4_first` ：表示 CDN 始終嘗試獲取來源伺服器網域名稱的 IPv4 位址。如果無法獲取該 IP 位址，CDN 才會嘗試獲取來源伺服器網域名稱的 IPv6 位址。<br><br>* `followclient` ：表示 CDN 嘗試獲取與使用者請求相同類型的 IP 位址。<br><br><br>該參數的預設值是 followclient 。<br><br>由於海外部分 CDN 區域伺服器不支援向 IPv6 位址傳送來源伺服器請求，該功能僅適用於位於中國大陸的區域伺服器。 |`followclient` |


<span id="來源伺服器-host"></span>
### 來源伺服器 Host


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginHost |String |否 |如果來源伺服器上有多个站點，該參數表示來源伺服器請求存取的站點網域名稱。該參數對所有來源伺服器設定生效，但是優先順序低於來源伺服器設定中 `OriginHost` 參數。<br><br>該參數的預設值與 `Domain` 相同。<br><br>如果來源伺服器是一個物件儲存桶，您無需指定該參數。其預設值與來源伺服器設定中的 `Address` 相同。 |`img.example.com` |


<span id="來源伺服器憑證校驗"></span>
### 來源伺服器憑證校驗


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginCertCheck |Object |否 |表示 "來源伺服器憑證校驗" 特性的設定。要使用此特性，請 [提交工單](https://console.byteplus.com/workorder/create)。<br><br>該特性啟用後，CDN 會校驗來源伺服器憑證的合法性，包括憑證是否已被吊銷、憑證是否由可信 CA 簽發、憑證與來源伺服器網域名稱是否匹配等。CDN 內建了常見可信 CA 的根憑證。如果來源伺服器憑證未通過校驗，CDN 進行 [來源伺服器請求重試](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-fetch-retry_zh-tw)。如果來源伺服器重試時來源伺服器憑證依然未通過校驗，CDN 判定無法從該來源伺服器獲取檔案，並對使用者請求回應 504 狀態碼。 | |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |
|CertInfoList |Object[] |否 |表示一個 CA 憑證列表，列表中的 CA 憑證託管在 CDN，且不能是國密憑證。CDN 使用該列表中的 CA 憑證對來自來源伺服器的伺服器憑證進行校驗。<br><br>目前，該列表中只能包含一本 CA 憑證。 | |
|CertId |String |否 |表示列表中一本 CA 憑證的 ID，以 `cert_hosting` 開頭。<br><br>您可以呼叫 [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCertInfo_zh-tw) 查詢託管在 CDN 的 CA 憑證列表以獲取您要指定的憑證的 ID。 |`cert_hosting-104663` |


<span id="https-設定"></span>
## HTTPS 設定

<span id="憑證設定"></span>
### 憑證設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|HTTPS |Object |否 |表示 HTTPS 加密服務的設定。 | |
|Switch |Boolean |是 |表示是否啟用 HTTPS 加密服務。該參數有以下取值：<br><br><br>* `true`：表示啟用 HTTPS 加密服務。<br><br>* `false`：表示禁用 HTTPS 加密服務。<br><br><br>如果 `Switch` 是 `true`，您必須指定 `CertInfo`。<br><br>您指定的憑證可以託管在 BytePlus 憑證中心，也可以託管在 CDN。 |`true` |
|CertInfo |Object |否 |表示要與網域名稱關聯的憑證。<br><br><br>* 如果該憑證已託管在 BytePlus 憑證中心或者 CDN，您必須在 `CertId` 中指定該憑證的 ID。<br><br>* 否則，您可以呼叫 [AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-AddCertificate_zh-tw) 上傳您的憑證或者在憑證中心主控台購買憑證，然後呼叫 `UpdateCdnConfig` 關聯該憑證。 | |
|CertId |String |否 |表示要關聯的憑證 ID。<br><br>您可以呼叫 [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCertInfo_zh-tw) 獲取您想要關聯的憑證 ID。 |`cert-eb5d99026753499a8a34d2a4f0a08d92` |
|DisableHttp |Boolean |否 |表示是否允許請求 URL 中 Scheme 是 `HTTP` 的請求。該參數有以下取值：<br><br><br>* `true`：表示允許 Scheme 是 `HTTP` 的請求。<br><br>* `false`：表示不允許 Scheme 是 `HTTP` 的請求。<br><br><br>該參數的預設值是 `false`。 |`false` |
|ForcedRedirect |Object |否 |表示 "HTTP 強制跳轉到 HTTPS" 特性的設定。<br><br>说明<br><br>CDN 提供了兩種通訊協定重定向的特性。<br><br><br>* HTTP 重定向到 HTTPS，也就是 `ForcedRedirect` 特性。<br><br>* HTTPS 重定向到 HTTP，也就是 `HttpForcedRedirect` 特性。<br><br><br>這兩個通訊協定重定向特性是互斥的。也就是說，如果您啟用了其中任意一個特性，就不能啟用另一個。 | |
|EnableForcedRedirect |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。啟用後，CDN 會將收到的 HTTP 請求重定向到 HTTPS 請求。<br><br>* `false`：表示停用該特性。停用後，CDN 不會將 HTTP 請求重定向到 HTTPS 請求。<br><br><br>要啟用該特性，您的網域名稱必須已啟用 HTTPS。 |`true` |
|StatusCode |String |是 |表示當收到 HTTPS 請求時 CDN 的重定向回應狀態碼。該參數有以下取值：<br><br><br>* `301`：表示返回的狀態碼是 301。<br><br>* `302`：表示返回的狀態碼是 302。<br><br><br>該參數的預設值是 `301`。 |`301` |
|HTTP2 |Boolean |否 |表示是否為使用者請求啟用 HTTP/2 支援。該參數有以下取值：<br><br><br>* `true`：表示啟用 HTTP/2。<br><br>* `false`：表示停用 HTTP/2。<br><br><br>要啟用該特性，您的網域名稱必須已經啟用了 HTTPS 加密服務。<br><br>該參數的預設值是 `false`。 |`true` |
|Hsts |Object |否 |表示 HSTS 特性的設定。 | |
|Subdomain |String |否 |表示 HSTS 設定是否也應用於網域名稱的子網域名稱。該參數有以下取值：<br><br><br>* `include`：表示 HSTS 設定應用於子網域名稱網站。<br><br>* `exclude`：表示 HSTS 設定不應用於子網域名稱網站。<br><br><br>該參數的預設值是 `exclude`。 |`include` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |
|Ttl |Long |否 |表示 `Strict-Transport-Security` 回應標頭在瀏覽器中的快取過期時間，單位是秒。如果 `Switch` 是 `true`，該參數為必填。該參數的取值範圍是 0 \- 31,536,000。31,536,000 秒表示 365 天。如果該參數值為 `0`，其效果等同於停用 HSTS 設定。 |`300` |
|OCSP |Boolean |否 |表示是否啟用 "OCSP 裝訂" 特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。<br><br><br>要啟用該特性，您的網域名稱必須啟用了 HTTPS。該參數的預設值是 `false`。 |`true` |
|TlsVersion |String[] |否 |表示 "TLS 版本" 特性的設定。該參數指定使用者請求可以使用的 TLS 版本，有以下取值：<br><br><br>* `tlsv1.0`：表示 TLS 1.0。<br><br>* `tlsv1.1`：表示 TLS 1.1。<br><br>* `tlsv1.2`：表示 TLS 1.2。<br><br>* `tlsv1.3`：表示 TLS 1.3。<br><br><br>該參數的預設值是 `["tlsv1.1", "tlsv1.2", "tlsv1.3"]` |`["tlsv1.1","tlsv1.2"]` |
|Keyless |Object |否 |KeylessServer | |
|CertInfoList |Object[] |否 |Keyless服务器证书校验\-CA证书 | |
|CertId |String |否 |证书ID | |
|CertName |String |否 |证书名 | |
|Certificate |Object |否 |证书信息 | |
|Certificate |String |否 |证书内容 | |
|EncryptionCert |String |否 |加密公私钥 | |
|EncryptionKey |String |否 |无 | |
|PrivateKey |String |否 |密钥 | |
|Desc |String |否 |证书描述信息 | |
|EffectiveTime |Long |否 |证书生效起始时间 | |
|EncryType |String |否 |证书类型 国际/国密 | |
|ExpireTime |Long |否 |证书过期时间 | |
|Source |String |否 |证书来源 | |
|CheckType |String |否 |Keyless服务器证书校验 | |
|ClientCertInfoList |Object[] |否 |Keyless服务器证书校验\-客户端证书 | |
|CertId |String |否 |证书ID | |
|CertName |String |否 |证书名 | |
|Certificate |Object |否 |证书信息 | |
|Certificate |String |否 |证书内容 | |
|EncryptionCert |String |否 |加密公私钥 | |
|EncryptionKey |String |否 |无 | |
|PrivateKey |String |否 |密钥 | |
|Desc |String |否 |证书描述信息 | |
|EffectiveTime |Long |否 |证书生效起始时间 | |
|EncryType |String |否 |证书类型 国际/国密 | |
|ExpireTime |Long |否 |证书过期时间 | |
|Source |String |否 |证书来源 | |
|KeylessServer |String |否 |Keyless服务器地址 | |
|Switch |Boolean |否 |Keyless开关 | |


<span id="強制跳轉設定"></span>
### 強制跳轉設定

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若要設定 HTTP 重新導向至 HTTPS，請參閱 <code>HTTPS</code> 模組中的 <code>ForcedRedirect</code> 子模組。<code>HttpForcedRedirect</code> 與 <code>ForcedRedirect</code> 是互斥的。換句話說，如果您設定了其中任一個模組，就無法設定另一個。</div>



|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|HttpForcedRedirect |Object |否 |表示 "HTTPS 強制跳轉到 HTTP" 特性的設定。 | |
|EnableForcedRedirect |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。啟用後，CDN 會將收到的 HTTPS 請求重定向到 HTTP 請求。<br><br>* `false`：表示停用該特性。CDN 不會將 HTTPS 請求重定向到 HTTP 請求。<br><br><br>要啟用該特性，您的網域名稱必須已啟用 HTTPS。 |`true` |
|StatusCode |String |是 |表示當收到 HTTPS 請求時，CDN 返回的重定向狀態碼。該參數有以下取值：**301**、**302**、**303**、**307**、**308**。<br><br>該參數的預設值是 `301`。<br><br>需要留意的是：<br><br><br>* 對於 301 和 302，如果原請求使用的方法不是GET，那麼客戶端向新的URL傳送請求時，新請求使用的方法可能變成 GET。<br><br>* 對於 303，新請求使用的方法是 GET。<br><br>* 對於 307 和 308，新請求使用的方法與原請求相同，不會被改變。 |`302` |


<span id="quic-設定"></span>
### QUIC 設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Quic |Object |否 |表示 QUIC 設定。 | |
|Switch |Boolean |是 |表示是否為使用者請求啟用 QUIC。該參數有以下取值：<br><br><br>* `true`：表示啟用 QUIC。<br><br>* `false`：表示停用 QUIC。<br><br><br>要啟用該特性，您的網域名稱必須已啟用 HTTPS。 |`true` |


<span id="存取限制"></span>
## 存取限制

<span id="websocket"></span>
### WebSocket


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Websocket |Object |否 |表示 WebSocket 設定。<br><br>注意<br><br>如果以下任一特性已啟用，您不能啟用 WebSocket。<br><br><br>* SSE<br><br>* HTTP/2<br><br>* HTTP/3 (QUIC) | |
|Switch |Boolean |否 |表示是否為使用者請求啟用 WebSocket 支援。該參數有以下取值：<br><br><br>* `true`：表示啟用 WebSocket。該特性啟用後，CDN 可以回應來自客戶端的 Websocket 請求。<br><br>* `false`：表示停用 WebSocket。<br><br><br>該參數的預設值是 `false`。 |`true` |
|Timeout |Long |否 |表示 Websocket 連線的逾時時間，單位是秒，取值範圍是 1\-300。<br><br>該參數的預設值是 60 秒。 |`60` |


<span id="proxy-protocol"></span>
### PROXY Protocol


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ProxyProtocol |Object |否 |表示 PROXY Protocol 的設定。 | |
|Switch |Boolean |否 |表示是否為使用者請求啟用 PROXY Protocol 支援。該參數有以下取值：<br><br><br>* `true` ：表示啟用 PROXY Protocol。該特性啟用後，CDN 就可以對收到的 PROXY 協定標頭進行解析，以獲取用戶端的真實 IP 位址。<br><br>* `false` ：表示停用 PROXY Protocol。<br><br><br>該參數的預設值是 `false` 。 |`true` |


<span id="server-sent-events-sse"></span>
### Server\-sent Events (SSE)


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ServerSentEvent |Object |否 |表示 SSE 的設定。<br><br>注意<br><br>SSE 和 WebSocket 不能同時開啟。 | |
|Switch |Boolean |否 |表示是否為使用者請求啟用 SSE 支援。該參數有以下取值：<br><br><br>* `true`：表示啟用 SSE。該特性啟用後，對於收到的用戶端 SSE 請求，CDN 扮演 SSE 代理的角色，將用戶端請求透傳到來源伺服器，並將來源伺服器 SSE 格式資料流推播至用戶端。<br><br>* `false`：表示停用 SSE。<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="url-標準化"></span>
### URL 標準化


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|UrlNormalize |Object |否 |表示 "URL 標準化" 特性的設定。 | |
|NormalizeObject |String[] |否 |表示一個 URL 標準化選項列表。當 `Switch` 為 `true` 時，該參數為必填。列表中可以包含以下選項：<br><br><br>* `dot_segments`：表示將請求 URL 中的以下內容進行替換：<br><br>   * `/./`：替換為單個斜線（/）。<br><br>   * `/../`：如果 `/../` 前還有一個級別的目錄，則刪除 `/../` 與該目錄。如果 `/../` 前沒有目錄，則保留原 URL。<br><br>* `back_slashes`：表示將請求 URL 中的反斜線（\）替換為單個斜線（/）。<br><br>* `successive_slashes`：表示將請求 URL 中雙斜線（//）替換為單個斜線（/）。 |`["dot_segments","back_slashes","successive_slashes"]` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="地區存取限制"></span>
### 地區存取限制


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|AreaAccessRule |Object |否 |表示 "地域存取控制" 特性的設定。 | |
|Area |String[] |否 |表示一個國家和地區的列表，對該列表應用地域存取限制。當 `Switch` 是 `true` 時，該參數為必填。國家和地區的名稱使用簡寫來表示。您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 並指定 `Area` 為 `Global` 以獲取國家和地區的簡寫。 |`["CHE","AZE"]` |
|RuleType |String |否 |表示 `Area` 的類型。當 `Switch` 是 `true` 時，該參數為必填。該參數有以下取值：<br><br><br>* `deny`: 表示 `Area` 是一個黑名單。CDN 將阻止來自這些國家和地區的請求。<br><br>* `allow`: 表示 `Area` 是一個白名單。CDN 僅允許來自這些國家和地區的請求。 |`allow` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |


<span id="禁用-http-方法"></span>
### 禁用 HTTP 方法


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|MethodDeniedRule |Object |否 |表示 "停用 HTTP Method" 特性的設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|Methods |String |否 |表示被停用的一個或多個 HTTP 請求方法。當 `Switch` 是 `true` 時，該參數為必填。多個方法使用逗號（,）分隔。該參數有以下取值：<br><br><br>* `get`：表示停用 GET 請求方法。<br><br>* `post`：表示停用 POST 請求方法。<br><br>* `delete`：表示停用 DELETE 請求方法。<br><br>* `put`：表示停用 PUT 請求方法。<br><br>* `head`：表示停用 HEAD 請求方法。<br><br>* `patch`：表示 PATCH 請求方法。<br><br>* `connect`：表示 CONNECT 請求方法。<br><br>* `options`：表示 OPTIONS 請求方法。 |`delete,put` |


<span id="ip-存取限制"></span>
### IP 存取限制


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|IpAccessRule |Object |否 |表示 "IP 黑白名單" 特性的設定。<br><br>該特性提供了兩種設定方式：<br><br><br>* 常規設定：指定 `RuleType` 和 `Ip` 對目前網域名稱進行設定。<br><br>* 全域設定：指定 `SharedConfig` 使用一個全域設定。<br><br><br>您只能選擇一種設定方式。 | |
|Ip |String[] |是 |表示黑名單或白名單中的 IP 位址。當 `Switch` 是 `true` 時，該參數為必填。您可以指定一個或者多個 IP 位址和 IP 位址網段。IP 位址和網段可以是 IPv4 或 IPv6 格式。您最多可輸入 1,000 個位址。<br><br>如果您指定了 `SharedConfig`，就不能指定該參數。 |`["xx.xxx.xx.xx","x.x.x.x"]` |
|RuleType |String |是 |表示 IP 名單的類型。當 `Switch` 是 `true` 時，該參數為必填。該參數有以下取值：<br><br><br>* `allow`：表示白名單。<br><br>* `deny`：表示黑名單。<br><br><br>如果您指定了 `SharedConfig`，就不能指定該參數。 |`deny` |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|SharedConfig |Object |否 |表示一個全域設定。<br><br>如果您指定了該參數，就不能指定 `RuleType` 和 `Ip`。 | |
|ConfigName |String |否 |表示一個全域設定的名稱。該全域設定的 `ConfigType` 必須是 `deny_ip_access_rule` 或者 `allow_ip_access_rule`。<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名單。<br><br>* `allow_ip_access_rule`：表示 IP 白名單。<br><br><br>您可以呼叫 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListSharedConfig_zh-tw) 獲取全域設定的列表。 |`my_whitelist` |
|DenyStatusCode |Long |否 |拦截状态码 | |
|IpSource |Object |否 |IP判断来源 | |
|SourceList |String[] |否 |无 | |
|Type |String |否 |无 | |


<span id="referer-存取限制"></span>
### Referer 存取限制


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|RefererAccessRule |Object |否 |表示 "Referer 黑白名單" 特性的設定。關於不同設定對請求匹配結果的影響，參見 [Referer 防盜連結](https://docs.byteplus.com/en/docs/byteplus-cdn/referer-restrictions_zh-tw#%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 | |
|AllowEmpty |Boolean |是 |表示當使用者請求不包含 Referer 標頭時，CDN 處理請求的方式。該參數有以下取值：<br><br><br>* `true`：表示如果請求不包含 Referer 標頭，則該請求被認為匹配您設定的 Referer 列表。<br><br>* `false`：表示如果請求不包含 Referer 標頭，則該請求被認為不匹配您設定的 Referer 列表。<br><br><br>該參數的預設值是 `false`。 |`true` |
|Referers |String[] |是 |表示一個 Referer 列表，該參數的輸入要求與 `ReferersType` 下 `CommonType` 型別的 `Referers` 的輸入要求相同。建議您使用 `ReferersType` 來指定 Referer 列表。<br><br>另外，如果您指定了 `SharedConfig`，就不能指定該參數。 |`["www.test.com","xxx.xx.x.x","xx.xx.xx.x/24"]` |
|ReferersType |Object |是 |表示一個 `ReferersType` 物件。其包含一個 `CommonType` 物件和一個 `RegularType` 物件，分別表示一個常規 Referer 列表和一個用於匹配 Referer 的正規表示式列表。您可以同時定義這兩個物件。<br><br>如果您指定了 `SharedConfig`，就不能指定該參數。 | |
|CommonType |Object |是 |表示一個 `CommonType` 物件，其包含一個常規 Referer 列表。 | |
|IgnoreCase |Boolean |否 |表示 `CommonType` 下的 `Referers` 列表是否是大小寫敏感的。該參數有以下取值：<br><br><br>* `true`: 表示大小寫不敏感。<br><br>* `false`: 表示大小寫敏感。<br><br><br>該參數的預設值是 `true`。 |`true` |
|Referers |String[] |是 |表示一個常規 Referer 列表。在該列表中，您可以指定一個或者多個 IP 位址，CIDR 網段，網域名稱和泛網域名稱。網域名稱可以是二級網域名稱。IP 位址只能是 IPv4 格式的位址。您最多可輸入 1,000 個 IP 位址。輸入的網域名稱不能包含 `http://` 或 `https://`。該參數值的長度不能超過 30,000 個字元。 |`["www.test.com","xxx.xxx.xx.xxx","1xx.xx.xx.x/24"]` |
|IgnoreScheme |Boolean |否 |表示 CDN 是否對 Referer 中的 scheme 進行校驗，也就是校驗 Referer 是否包含 `http://` 或者 `https://`。該參數有以下取值：<br><br><br>* `true`: 表示 CDN 不校驗 Referer 是否包含 scheme。在這種情況下，無論 Referer 是否包含 scheme，CDN 都會將 Referer 與您設定的名單進行匹配校驗。<br><br>* `false`: 表示 CDN 會先校驗 Referer 是否包含 scheme。只有 Referer 包含 scheme，CDN 才會將 Referer 與您設定的名單進行匹配校驗。否則，CDN 判定請求與您設定的名單不匹配。<br><br><br>該參數的預設值是 `false`。<br><br>另外，該設定對 `RegularType` 下的正規表示式列表不生效，因為 CDN 依賴正規表示式來判斷 Referer 是否匹配正規名單。 |`false` |
|ContMainDomain |Boolean |否 |泛域名匹配包含主域名 | |
|RegularType |Object |是 |表示一個 `RegularType` 物件，其包含一個正規表示式列表用來匹配請求中的 Referer 標頭。 | |
|Referers |String[] |是 |表示一個用於匹配 Referer 的正規表示式列表。該參數值的長度不能超過 30,000 個字元。 |`^http://a.com` |
|RuleType |String |是 |表示 Referer 名單的類型。當 `Switch` 是 `true` 時，該參數為必填。該參數有以下取值：<br><br><br>* `allow`：表示白名單。<br><br>* `deny`：表示黑名單。 |`deny` |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|SharedConfig |Object |否 |表示一個全域設定。<br><br>如果您指定了該參數，就不能指定 `Referers`，也不能指定 `ReferersType`。 | |
|ConfigName |String |否 |表示一個全域設定的名稱。該全域設定的 `ConfigType` 必須是 `deny_referer_access_rule` 或者 `allow_referer_access_rule`。<br><br><br>* `deny_referer_access_rule`：表示 Referer 黑名單。<br><br>* `allow_referer_access_rule`：表示 Referer 白名單。<br><br><br>您可以呼叫 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListSharedConfig_zh-tw) 獲取全域設定的列表。 |`my_allowlist` |


<span id="ua-存取限制"></span>
### UA 存取限制


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|UaAccessRule |Object |否 |表示 "UA 黑白名單" 特性的設定。 | |
|AllowEmpty |Boolean |是 |表示當使用者請求不包含 User\-Agent 標頭時，CDN 處理請求的方式。該參數有以下取值：<br><br><br>* `true`：表示如果請求不包含 User\-Agent 標頭，則該請求被認為匹配您設定的 User\-Agent 列表。<br><br>* `false`：表示如果請求不包含 User\-Agent 標頭，則該請求被認為不匹配您設定的 User\-Agent 列表。<br><br><br>該參數的預設值是 `false`。 |`true` |
|IgnoreCase |Boolean |是 |表示 UA 字串是否是大小寫敏感的。該參數有以下取值：<br><br><br>* `true`: 表示 UA 字串是大小寫不敏感的。<br><br>* `false`: 表示 UA 字串是大小寫敏感的。<br><br><br>該參數的預設值是 `false`。 |`true` |
|RuleType |String |是 |表示 UA 名單的類型。當 `Switch` 是 `true` 時，該參數為必填。該參數有以下取值：<br><br><br>* `allow`：表示白名單。<br><br>* `deny`：表示黑名單。 |`deny` |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|UserAgent |String[] |是 |表示一個 UA 的列表。當 `Switch` 是 `true` 時，該參數為必填。該列表最多包含 1,000 個 UA。該參數的說明如下：<br><br><br>* 該參數值的長度不能超過 30,000 個字元。<br><br>* 如果 `RuleType` 是 `allow`，表示僅允許包含列表中的 UA 的請求存取網域名稱。<br><br>* 如果 `RuleType` 是 `deny`，表示如果存取請求包含列表中的 UA，則不允許存取網域名稱。<br><br><br>UA 能包含的字元有以下限制：<br><br><br>* UA 中可以使用 `*` 表示一個或者多個字元。`*` 僅可以出現在 UA 的開頭和末尾。<br><br>* UA 不能只包含 `*`或者空格。<br><br>* UA 如果包含符號，符號必須是被 HTML 編碼的。 |`["*curl*","*Mozilla*"]` |


<span id="origin-存取限制"></span>
### Origin 存取限制


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginAccessRule |Object |否 |表示 "Origin 黑白名單" 特性的設定。 | |
|AllowEmpty |Boolean |是 |表示當使用者請求不包含 Origin 標頭時，CDN 處理請求的方式。該參數有以下取值：<br><br><br>* `true`：表示如果請求不包含 Origin 標頭，則該請求被認為匹配您設定的 Origin 列表。<br><br>* `false`：表示如果請求不包含 Origin 標頭，則該請求被認為不匹配您設定的 Origin 列表。<br><br><br>該參數的預設值是 `false`。 |`true` |
|IgnoreCase |Boolean |是 |表示 Origin 列表是否是大小寫敏感的。該參數有以下取值：<br><br><br>* `true`: 表示 Origin 列表是大小寫不敏感的。<br><br>* `false`: 表示 Origin 列表是大小寫敏感的。<br><br><br>該參數的預設值是 `true`。 |`true` |
|Origins |String[] |是 |表示一個 Origin 清單。清單中可以包含最多 100 個 Origins，總長度不能超過 3,000 個字元。Origin 可以是 IP 位址，CIDR 網段，網域名稱或泛網域名稱。網域名稱可以是二級網域名稱。IP 位址可以是 IPv4 或 IPv6 格式的位址。 |`["www.test.com"]` |
|RuleType |String |是 |表示 Origin 清單的類型。該參數有以下取值：<br><br><br>* `allow`：表示白名單。<br><br>* `deny`：表示黑名單。 |`deny` |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |


<span id="自訂攔截規則"></span>
### 自訂攔截規則


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|RequestBlockRule |Object |否 |表示 "自訂攔截" 特性的設定。 | |
|BlockRule |Object[] |是 |表示一個規則清單。清單中最多可以包含 10 條規則。當 `Switch` 是 `true` 時，該參數為必填。<br><br>清單中的第一條規則具有最高的優先順序。<br><br>當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。 | |
|BlockAction |Object |是 |表示一條規則中 CDN 行為的設定。 | |
|Action |String |是 |表示 CDN 如何處理符合 `Condition` 的請求。該參數有以下取值：<br><br><br>* `refuse`：表示 CDN 拒絕請求並回應一個 4xx 的錯誤碼。錯誤碼在 `StatusCode` 中指定。<br><br>* `redirect`：表示 CDN 將請求重新導向到 `RedirectUrl` 中指定的 URL。 |`refuse` |
|StatusCode |String |是 |表示對於符合 `Condition` 的使用者請求，CDN 的回應狀態碼。<br><br><br>* 當 `Action` 是 `refuse` 時，該參數表示一個 400\-499 範圍內的錯誤碼。<br><br>* 當 `Action` 是 `redirect` 時，該參數有以下取值：<br><br>   * `301`：表示回應狀態碼是 301。<br><br>   * `302`：表示回應狀態碼是 302。 |`403` |
|ErrorPage |String |否 |* 當 `Action` 是 `refuse` 時，該參數是可選的，說明如下：<br><br>   * 如果指定該參數，該參數表示 "全域設定" 特性中的一個自訂回應頁面的名稱。也就是說，當 CDN 拒絕請求時，返回該自訂頁面。<br><br>   * 如果不指定該參數，表示 CDN 使用 `StatusCode` 中指定錯誤碼的標準回應正文。<br><br>* 當 `Action` 是 `redirect` 時，該參數無效，可以不指定。 |`GlobalConfigName` |
|RedirectUrl |String |否 |* 當 `Action` 是 `redirect` 時，該參數必填，表示重新導向 URL。URL 必須以 `http://` 或 `https://` 開頭，長度不能超過 1,024 個字元。<br><br>* 當 `Action` 是 `refuse` 時，該參數無效，可以不指定。 |`http://www.example.com` |
|Condition |Object |是 |表示該規則中符合條件的定義。 | |
|ConditionRule |Object[] |是 |表示一個符合條件清單，用於比對請求 URL 中的路徑和查詢參數、以及請求來自的用戶端 IP 位址。清單中最多可以包含 5 個符合條件。每個符合條件包含比對類型、對比類型和比對值。 | |
|Object |String |是 |表示一個比對類型。<br><br><br>* 當 `Type` 是 `url` 時，該參數有以下取值：<br><br>   * `path`：表示請求 URL 中的路徑。<br><br>   * `directory`：表示路徑中的一個目錄。<br><br>   * `filetype`：表示路徑末尾的副檔名。<br><br>   * `regex`：表示請求 URL 中的路徑，透過正規表示式比對。<br><br>* 當 `Type` 是 `querystring` 時，該參數有以下取值：<br><br>   * `query_name`：表示請求 URL 中的一個查詢參數。<br><br>   * `full_querystring`：表示請求 URL 中的查詢字串。<br><br>* 當 `Type` 是 `client_ip` 時，該參數有以下取值：<br><br>   * `client_ip`：表示用戶端的 IP 位址。<br><br>* 當 `Type` 是 `request_header` 時，該參數有以下取值：<br><br>   * `ua`：表示請求中 User\-Agent 標頭。<br><br>   * `customize`：表示請求中的自訂標頭。 |`filetype` |
|Operator |String |是 |表示一個對比類型。<br><br><br>* 當 `Object` 是 `path`、`directory`、`filetype` 時，該參數有以下取值：<br><br>   * `equal`：表示如果比對 `Value` 中的任何值，該請求就滿足這個比對條件。<br><br>   * `not_equal`：表示如果不比對 `Value` 中的所有值，該請求才滿足這個比對條件。<br><br>* 當 `Object` 是 `query_name` 時，該參數有以下取值：<br><br>   * `exist`：表示存在。比對邏輯與 `equal` 相同。<br><br>   * `not_exist`：表示不存在。比對邏輯與 `not_equal` 相同。<br><br>   * `belong_shared_config`：表示如果比對 `Value` 表示的全域設定中所包含的任何值，該請求就滿足這個比對條件。<br><br>   * `not_belong_shared_config`：表示如果不比對 `Value` 表示的全域設定中的所有值，該請求才滿足這個比對條件。<br><br>   * `empty`：表示值為空。<br><br>   * `not_empty`：表示值不為空。<br><br>   * `equal`：參見以上描述。<br><br>   * `not_equal`：參見以上描述。<br><br>* 當 `Object` 是 `regex`、`full_querystring`、`client_ip` 或 `ua` 時，該參數有以下取值：<br><br>   * `match`：描述與 `equal` 相同。<br><br>   * `not_match`：描述與 `not_equal` 相同。<br><br>* 當 `Object` 是 `ua` 或 `customize` 時，該參數還有以下**額外**取值：<br><br>   * `empty`：參見以上描述。<br><br>   * `not_empty`：參見以上描述。 |`not_equal` |
|Type |String |是 |表示一個比對物件的類型。該參數有以下取值：<br><br><br>* `url`：表示請求 URL。<br><br>* `querystring`：表示請求 URL 中的查詢字串。<br><br>* `request_header`：表示請求中的標頭。 |`url` |
|Value |String |是 |表示一個或者多個比對值。<br><br><br>* 如果 `Type` 是 `request_header`，多個比對值之間使用豎線（\\|）分隔。<br><br>* 如果 `Type` 不是 `request_header`，多個比對值之間使用分號（;）分隔。<br><br><br>&nbsp;<br><br>該參數的輸入要求如下：<br><br><br>* 當 `Object` 是 `path`、`directory` 或 `filetype` 時，所有比對值的總長度不能超過 1,024 個字元，不能包含以下字元：<br><br>   * 雙斜線（//）、空格、貨幣符號（$）、問號（?）、句點（.）<br><br>* 當 `Object` 是 `path` 時，該參數有以下**額外**要求：<br><br>   * 每個比對值必須以斜線（/）開頭。您可以在比對值中使用一個或者多個星號（\*），每個星號表示一個或者多個字元。例如：`/www/img/my*image.png`。<br><br>* 當 `Object` 是 `directory` 時，該參數有以下**額外**要求：<br><br>   * 每個比對值必須以斜線（/）開頭和結尾。例如：`/www/img/`。<br><br>* 當 `Object` 是 `filetype` 時，該參數有以下**額外**要求：<br><br>   * 每個比對值無需以句點（.）開頭。例如：`png;txt`。<br><br>* 當 `Object` 是 `query_name` 時，<br><br>   * 如果 `Operator` 是 `equal` 或者 `not_equal`，您只能指定一個比對值，表示 `Name` 所表示的查詢參數的值。該值的長度不能超過 256 個字元，可以包含數字、字母、百分比符號（%）、底線（_）、中線（\-）。<br><br>   * 如果 `Operator` 是 `belong_shared_config`、`not_belong_shared_config` 時，您只能指定一個比對值。該比對值是一個全域設定的名稱。<br><br>   * 如果 `Operator` 是 `exist`、`not_exist`、`empty`、`not_empty`，該參數無效，可以不指定。<br><br>* 當 `Object` 是 `full_querystring` 或者 `regex` 時，每個比對值都是一個正規表示式。多個比對值之間使用分號（;）分隔。所有比對值的總長度不能超過 1,024 個字元。<br><br>* 當 `Object` 是 `client_ip` 時，`Value` 中最多可以包含 50 個比對值，總長度不能超過 30,000 個字元。每個比對值是一個 IP 位址。IP 位址可以是 IPv4 位址、IPv4 CIDR 位址、IPv6 位址、IPv6 CIDR 位址。<br><br>* 當 `Object` 是 `custom` 或者 `ua` 時，`Value` 中最多可以包含 50 個比對值，總長度不能超過 1,024 個字元。比對值可以以 \* 開頭和結尾。\* 表示任意連續字元。<br><br>   * 如果 `Object` 是 `custom`，每個比對值是 `Name` 所表示的標頭的值。<br><br>   * 如果 `Object` 是 `ua`，每個比對值是一個 User\-Agent 標頭值。<br><br>   * 如果 `Operator` 是 `empty`、`not_empty`，該參數無效，可以不指定。 |`png;txt` |
|Name |String |否 |當 `Object` 是 `query_name` 或者 `customize` 時，該參數有效。<br><br><br>* 如果 `Object` 是 `query_name`，該參數表示一個查詢參數的名稱。<br><br>* 如果 `Object` 是 `customize`，該參數表示一個自訂請求標頭的名稱。<br><br><br>`Name` 的長度不能超過 256 個字元，可以包含數字、字母、百分比符號（%）、底線（_）、中線（\-）。 |`color` |
|Connective |String |是 |表示多條 `ConditionRule` 之間的關係。該參數有以下取值：<br><br><br>* `AND`：表示 "與"。<br><br>* `OR`：表示 "或"。<br><br><br>該參數的預設值是 `OR`。 |`AND` |
|RuleName |String |是 |表示規則的名稱，長度不超過 20 個字元，可以包含字母、數字、底線（_）、中線（\-）、漢字。一個漢字佔 3 個字元。 |`MyRule` |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |


<span id="url-驗證"></span>
### URL 驗證


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|SignedUrlAuth |Object |否 |表示 "URL 驗證" 特性的設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|SignedUrlAuthRules |Object[] |否 |表示一個規則清單。每條規則包含符合條件設定和驗證設定。目前，清單中只能包含一條規則。當 `Switch` 是 `true` 時，該參數為必填。 | |
|Condition |Object |是 |表示符合條件的設定。CDN 對符合條件的使用者請求進行驗證。 | |
|ConditionRule |Object[] |是 |表示一個符合條件清單。<br><br><br>* 當 `URLAuthType` 是 `typea`、`typed`、`typee` 時，您最多可以建立 10 個條件。<br><br>* 當 `URLAuthType` 是 `typeb`、`typec` 時，您只能建立 1 個條件。 | |
|Object |String |是 |表示符合條件中的比對類型。該參數有以下取值：<br><br><br>* `filetype`：表示 URL 路徑末尾的副檔名。<br><br>* `directory`：表示 URL 路徑中的一個目錄。<br><br>* `path`：表示完整的 URL 路徑。<br><br>* `regex`: 表示完整的 URL 路徑，透過正規表示式比對。<br><br><br>需要留意的是，當 `URLAuthType` 是 `typeb`、`typec` 時，您只能指定該參數值為 `filetype` 或 `directory`。 |`directory` |
|Operator |String |是 |表示符合條件中的比對方式。該參數有以下取值：<br><br><br>* `match`：表示如果 `object` 比對 `Value`，該請求就滿足了這個比對條件。<br><br>* `not_match`：表示如果 `object` 不比對 `Value`，該請求就滿足了這個比對條件。<br><br><br>該參數的預設值是`match`。<br><br>需要留意的是，當 `URLAuthType` 是 `typeb`、`typec` 時，您只能指定該參數值為 `match`。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示符合條件中的比對值。多個比對值之間以分號（;）分隔，總長度不能超過 1,024 個字元，不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、貨幣符號（$）、問號（?）<br><br><br>另外，<br><br><br>* 如果 `Object` 是 `filetype`，則每個比對值是一個檔案副檔名，不能以句點（.）開頭。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，則每個比對值是一個目錄路徑，必須以斜線（/）開頭和結尾。例如：`/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，則每個比對值是一個 URL 路徑，必須以斜線（/）開頭。比對值可以包含星號（\*）用來表示一個或者多個任意字元。例如：`/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果 `Object` 是 `regex`，則每個比對值是一個正規表示式，用於比對 URL 路徑。例如：`^/a{1,2}.*g$`。 |`png;jpg` |
|Connective |String |是 |表示多個 `ConditionRule` 之間的邏輯關係。該參數有以下取值：<br><br><br>* `AND`: 表示邏輯關係是 "AND"。<br><br>* `OR`：表示邏輯關係是 "OR"。<br><br><br>該參數的預設值是 `OR`。<br><br><br>* 當 `URLAuthType` 是 `typeb`、`typec` 時，該參數值必須是 `OR`。 |`OR` |
|SignedUrlAuthAction |Object |是 |表示簽章計算的設定。 | |
|Duration |Long |是 |表示簽章的有效時間，單位是秒。該參數與請求中包含時間標記搭配使用，用來計算簽章的過期時間。該參數的取值範圍是 `0-315,360,000`。簽章的過期時間 = 時間標記 + `Duration`。在 CDN 收到某個請求時，如果簽章的過期時間小於目前時間，CDN 判定簽章已過期。 |`1000` |
|MasterSecretKey |String |是 |表示主金鑰，長度不超過 120 個字元。 |`abcdefg` |
|URLAuthType |String |是 |簽章類型。該參數有以下取值：`typea`、`typeb`、`typec`、`typed`、`typee`，每種類型得驗證說明見 [URL 驗證概覽](https://docs.byteplus.com/en/docs/byteplus-cdn/signed-url-authentication-overview_zh-tw) 。 |`typea` |
|BackupSecretKey |String |否 |表示備用金鑰，長度不超過 120 個字元。 |`abcdefg` |
|CustomVariableRules |Object |否 |表示自訂簽算變數。 | |
|CustomVariableInstances |Object[] |是 |表示一個變數清單。 | |
|Operator |String |是 |表示變數的比對方式。該參數的取值只能是 `match`。 |`match` |
|Type |String |是 |表示變數的類型。該參數有以下取值：<br><br><br>* `queryString`：表示該變數是請求中的一個查詢參數。<br><br>* `requestHeader`：表示該變數是請求中的一個標頭欄位。 |`queryString` |
|Value |String |是 |表示變數的名稱，長度不超過 100 個字元。變數名稱的要求如下：<br><br><br>* 如果 `Type` 是 `queryString`，變數名稱可以包含以下字元：<br><br>   * 字母、數字、連字元（\-）、逗號（,）、句點（.）、驚嘆號（!）<br><br>* 如果 `Type` 是 `requestHeader`，變數名稱不能包含以下字元：<br><br>   * 底線（_）、空格、雙引號（"）、冒號（:） |`myparam1` |
|RewriteM3u8 |Boolean |否 |對於 HLS Manifest (.m3u8) 的請求，該參數表示 CDN 是否要修改 Manifest，從而為每個影片分片產生簽章並將簽章新增到 URI 中。<br><br>該參數有以下取值：<br><br><br>* `true`：表示需要修改 Manifest。<br><br>* `false`：表示不需要修改 Manifest。<br><br><br>該參數的預設值是 `false`。<br><br>當 `URLAuthType` 為 `typee` 時，該參數無效。<br><br>说明<br><br>目前，CDN 不會修改壓縮檔案。因此，在以下任何情況下，CDN 都不會修改 Manifest。<br><br><br>* 來源伺服器回應中包含 `Content-Encoding` 標頭。該標頭表明該 Manifest 已被壓縮。<br><br>* 使用者請求符合 "智慧壓縮" 特性中的規則。 |`true` |
|SignName |String |否 |表示簽章參數的名稱。該參數的說明如下：<br><br><br>* 可以包括英文字母、數字、底線（_）、中線（\-）、句點（.）、逗號（,）、驚嘆號（!）。<br><br>* 長度不能超過 100 個字元。<br><br>* 至少包含一個字母或者數字。<br><br>* 不能與 `TimeName` 相同。<br><br><br>當 `URLAuthType` 為 `typea`、`typed`、`typee` 時，該參數為必填。對於其他類型，該參數不生效。 |`sign` |
|SignatureRule |String[] |否 |當 `URLAuthType` 為 `typee` 時，該參數為必填，表示需要納入簽章計算的欄位。必須納入簽章計算的欄位如下：<br><br><br>* `key`：表示`MasterSecretKey`或 `BackupSecretKey` 指定的金鑰。<br><br>* `uri`：表示使用者請求的 URI，僅包含字路徑和查詢參數。如果 URI 包含中文字元，您需要對 URI 編碼。<br><br>* `TimeName`：表示 `TimeFormat` 指定的時間標記。<br><br><br>可選擇納入簽章計算的欄位如下：<br><br><br>* `domain`：表示網域名稱。<br><br>* `referer`：表示使用者請求攜帶的 referer 值。<br><br>* `ua`：表示使用者請求攜帶的 User\-Agent 值。<br><br>* `ip`：表示使用者請求的用戶端 IP。<br><br>* `origin`：表示使用者請求攜帶的 Origin 值。<br><br>* 自訂變數：表示您在 `CustomVariableInstances` 中定義的變數的值。<br><br><br>CDN 按清單中欄位的順序將這些欄位拼接成一個字串，然後計算該字串的 MD5 值。該 MD5 值就是簽章。 |`["domain","ip","key","TimeName","uri"]` |
|TimeFormat |String |否 |表示 `TimeName` 使用的進位。該參數有以下取值：<br><br><br>* `decimal`：十進位。<br><br>* `heximal`：十六進位。<br><br><br>當 `URLAuthType` 為 `typed`、`typee` 時，該參數為必填。當 `URLAuthType` 為 `typec` 時，無論您是否設定該參數，該參數的值會被強制設定為 `heximal`。對於 `URLAuthType` 的其他值，該參數不生效。 |`heximal` |
|TimeName |String |否 |表示時間標記參數的名稱。`TimeName` 的值可以包括英文字母、數字、底線（_）、中線（\-）、句點（.）、逗號（,）、驚嘆號（!），長度為 `1-100` 個字元。`TimenName` 不能與 `SignName` 相同。<br><br>當 `URLAuthType` 為 `typed`、`typee` 時，該參數為必填。對於其他類型，該參數不生效。 |`TimeParam` |
|DeleteAuthCacheAndOrigin |Boolean |否 |去除鉴权参数缓存和回源，仅类型e | |
|AuthRulesF |Object[] |否 |表示 Type\-F 設定，其中包含一個規則清單。該清單最多可包含 5 條規則。清單中的第一條規則具有最高的優先順序。<br><br>當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。 | |
|ArgumentRule |Object |否 |表示來源伺服器參數相關的設定。 | |
|KeepOriginArg |Boolean |否 |表示是否在來源伺服器請求中包含基於 `AuthTokenCalRule` 計算的權杖。該參數有以下取值：<br><br><br>* `true`：表示在來源伺服器請求中包含權杖。來源伺服器請求中權杖出現的位置與 `SignCapRule` 中的設定相同。<br><br>* `false`：表示不在來源伺服器請求中包含權杖。 |`true` |
|GeneralParamRule |Object |否 |表示 CDN 設定影片分片 URI 中查詢參數的方式。 | |
|ParentLinkParamInherit |String |否 |表示改寫後的影片分片 URI 是否包含使用者請求 URL 中除表示權杖和權杖時間標記的參數之外的所有查詢參數。該參數有以下取值：<br><br><br>* `not_inherit`：表示改寫後的分片 URI 不會包含這些查詢參數。<br><br>* `inherit`：表示改寫後的分片 URI 會包含這些查詢參數。 |`not_inherit` |
|SubLinkParamRule |Object |否 |該結構體包含額外的查詢參數設定。該結構體包含額外的查詢參數設定。 | |
|InheritMode |String |否 |表示當影片分片 URI 和使用者請求 URL 中存在相同的查詢參數時，CDN 如何設定影片分片 URI 中該參數的值。當 `ParentLinkParamInherit` 為 `inherit` 時，您可以設定該參數。<br><br>該參數有以下取值：<br><br><br>* `sub_link_first`：表示使用影片分片 URI 中該參數的值。<br><br>* `inherit_first`：表示使用使用者請求 URL 中該參數的值。 |`inherit_first` |
|KeepSubLinkArg |String |否 |表示改寫後的影片分片 URI 是否保留 URI 中原有的查詢參數。該參數有以下取值：<br><br><br>* `delete`：表示改寫後的分片 URI 不會保留這些查詢參數。<br><br>* `keep`：表示改寫後的分片 URI 會保留這些查詢參數。 |`delete` |
|AuthTokenCalRule |Object |否 |表示權杖計算的設定。請參考 範例程式碼 在用戶端部署權杖計算邏輯，將產生的權杖包含在使用者請求中。<br><br>CDN 使用 `SignJoinSymbol` 將 `SignParam` 中的各物件進行拼接，然後對拼接後的物件套用 `ParamCalRules` 中指定的演算法計算權杖，用於與使用者請求中包含的權杖進行比較。 | |
|ParamCalRules |String[] |否 |表示計算權杖所使用的演算法清單，清單中最多包含 5 個演算法。CDN 按清單中演算法的出現順序產生權杖的計算公式。<br><br>該參數有以下取值：`md5_bin`、`base64url`、`sha256`、`md5`、`base64_encode`、`sha1`、`sha224`、`sha384`、`sha512`、`sha3_224`、`sha3_256`、`sha3_384`、`sha3_512`、`upper_case`、`lower_case`。<br><br>说明<br><br>如果您指定了 `md5_bin`，您必須指定下一個演算法為 `base64url`。<br><br><br>* 正確設定：`sha1`、`md5_bin`、`base64url`<br><br>* 錯誤設定：`sha1`、`md5_bin`、`base64url`、`base64url`、`md5_bin` |`["sha1"、"md5_bin"、"base64url"]` |
|SignJoinSymbol |String |否 |表示拼接 `SignParam` 中各物件而使用的拼接符。該參數的預設值為空（""）。 |`00` |
|SignParam |Object[] |否 |表示 CDN 在計算權杖時使用的物件清單。每個物件由 `ParamType` 和相關設定組成。例如，以下範例表示物件是一個字串，字串的值是 `str-for-token-calc`。<br><br>```json```<br>```{```<br>```    "ParamType": "SupString",```<br>```    "SupContent": "str-for-token-calc"```<br>```}```<br> | |
|CookieToken |String |否 |當 `ParamType` 是 `Cookie` 時，您必須指定該參數。該參數表示您要指定的 cookie 的 key。CDN 會獲取該 cookie 的 value。 |`mycookiekey` |
|ParamSource |String |否 |當 `RewriteMPD` 或者 `RewriteM3U8` 為啟用，並且物件的 `ParamType` 是 `URI`、`URLParam` 或者 `FullURI` 時，您可以指定該參數。<br><br>對於新增到 Manifest 中的權杖，該參數表示 CDN 在使用該物件計算權杖時，該物件的來源。<br><br>該參數有以下取值：<br><br><br>* `ParentLink`：表示該物件來自使用者請求中的 URL。<br><br>* `ChildLink`：表示該物件來自 Manifest 中影片分片的 URI。<br><br><br>該參數的預設值是 `ChildLink`。 |`ParentLink` |
|ParamType |String |否 |表示物件的類型。該參數有以下取值：<br><br><br>* `SecretKey`：表示 `SecretKey` 結構體中的 `MasterSecretKey` 或者 `BackupSecretKey`。當驗證失敗時，CDN 會使用 `BackupSecretKey` 計算權杖，重新對使用者請求進行驗證。<br><br>* `SupString`：表示一個字串。相關設定在 `SupContent` 中指定。<br><br>* `URI`：表示請求路徑中的連續片段。路徑不包含查詢字串。相關設定在 `UriParamSup` 與 `ParamSource` 中指定。<br><br>* `URLParam`：表示請求 URL 中的某類物件。物件可以是一個查詢參數或者某個目錄。相關設定在 `UriParam` 與 `ParamSource` 中指定。<br><br>* `ClientDomain`：表示請求網域名稱。<br><br>* `Referer`：表示使用者請求中 Referer 標頭的值。<br><br>* `Origin`：表示使用者請求中 Origin 標頭的值。<br><br>* `ClientIP`：表示傳送使用者請求的用戶端 IP 位址。<br><br>* `UA`：表示使用者請求中 Use\-Agent 標頭的值。<br><br>* `ReqHeader`：表示使用者請求中某個標頭的值。相關設定在 `RequestHeader` 中指定。<br><br>* `Cookie`：表示請求中的一個 cookie。相關設定在 `CookieToken` 中指定。<br><br>* `FullURI`：表示請求的完整路徑，不包含查詢字串。相關設定在 `ParamSource` 中指定。 |`URI` |
|RequestHeader |String |否 |當 `ParamType` 是 `ReqHeader` 時，您必須指定該參數。該參數表示您要指定的請求標頭。 |`myheader2` |
|SupContent |String |否 |當 `ParamType` 是 `SupString` 時，您必須指定該參數。該參數表示您要指定的字串。 |`123abc` |
|UriParamSup |Object |否 |表示從請求路徑中獲取連續片段的方式。當 `ParamType` 是 `URI` 時，您必須指定該參數。<br><br>該參數是一個結構體，包含以下設定：<br><br><br>* 拆分請求路徑所使用的分隔符號。<br><br>* 所需連續路徑片段的開始層級和結束層級。<br><br>* 拼接這些路徑片段所使用的拼接符。拼接後的路徑片段用於計算權杖。 | |
|JoinSymbol |String |否 |表示拼接這些路徑片段所使用的拼接符，要求如下：<br><br><br>* 長度為 1 個字元，可以是字母、數字、底線（_）、連字元（\-）、反斜線（/）、驚嘆號（!）。<br><br><br>該參數的預設值是空（""）。 |`00` |
|SplitSymbol |String |否 |表示拆分請求路徑所使用的分隔符號，要求如下：<br><br><br>* 長度為 1 個字元，可以是字母、數字、底線（_）、連字元（\-）、反斜線（/）、驚嘆號（!）。 |`-` |
|StartLevel |Long |否 |表示起始片段所在的層級，要求如下：<br><br><br>* 必須是一個正整數。<br><br>* 不能大於層級總數。<br><br>* `StartLevel` 所表示的路徑片段不能在 `TermLevel` 所表示的路徑片段右側。 |`2` |
|TermLevel |Long |否 |表示結束片段所在的層級，要求如下：<br><br><br>* 只能是非 0 的整數。<br><br>* 絕對值不能大於層級總數。<br><br><br>如果 `TermLevel` 是負整數，表示從最右邊的片段開始向左計數。 |`3` |
|UrlParam |Object |否 |表示從 URL 中獲取所需物件的方式。當 `ParamType` 是 `URLParam` 時，您必須指定該參數。<br><br>該參數是一個結構體，包含物件的來源以及相關設定。 | |
|ArgSegment |Object |否 |表示基於 `ParamName` 或者 `UriLevel` 獲取的內容是否需要被拆分，以提取某個層級的片段。該片段才是您需要獲取的物件。 | |
|Level |Long |否 |表示將獲取到的內容拆分為多個層級的片段後，您需要的物件所在的層級。該參數的要求如下：<br><br><br>* 層級是非 0 的整數。<br><br>* 層級的絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從最右邊層級的片段開始向左計數。<br><br>當 `Switch` 為 `true` 時，您必須指定該參數。 |`2` |
|SplitSymbol |String |否 |表示用於拆分內容而使用的分隔符號。<br><br>當 `Switch` 為 `true` 時，您必須指定該參數。 |`-` |
|Switch |Boolean |否 |表示獲取到的內容是否需要被拆分。該參數有以下取值：<br><br><br>* `true`：表示內容需要被拆分。<br><br>* `false`：表示內容無需被拆分。<br><br><br>該參數的預設值是 `false`。 |`true` |
|CapMode |String |否 |表示物件的來源。該參數有以下取值：<br><br><br>* `name`：表示查詢參數。相關設定在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示請求路徑中指定的目錄。相關設定在 `UriLevel` 和 `ArgSegment` 中指定。 |`uri` |
|ParamName |String |否 |當 `ParamType` 是 `name` 時，您必須指定該參數。該參數表示您要指定的查詢參數。 |`myparam3` |
|UriLevel |Long |否 |當 `ParamType` 是 `uri` 時，您必須指定該參數。該參數表示您要指定的目錄層級。<br><br>該參數的要求如下：<br><br><br>* 層級是非 0 的整數。<br><br>* 絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從最右邊的目錄開始向左計數。 |`2` |
|CustomRewrite |Object |否 |表示影片 Manifest 的擴充改寫設定。該設定啟用後，CDN 使用 [特殊重寫邏輯](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw#%E5%BD%B1%E7%89%87-manifest-%E7%9A%84%E7%89%B9%E6%AE%8A%E9%87%8D%E5%AF%AB%E9%82%8F%E8%BC%AF) 覆蓋 [預設改寫邏輯](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw#%E5%BD%B1%E7%89%87-manifest-%E6%AA%94%E6%A1%88%E7%9A%84%E9%A0%90%E8%A8%AD%E6%94%B9%E5%AF%AB%E9%82%8F%E8%BC%AF)。 | |
|RewriteParam |Object[] |否 |表示一個物件清單。CDN 將這些物件拼接而產生權杖，新增到影片分片的 URL 中。 | |
|ParamType |String |否 |表示物件的類型。該參數有以下取值：<br><br><br>* `ParentLinkUrlParam`：表示使用者請求 URL 中的某類物件。物件可以是一個查詢參數或者某個層級的路徑目錄。相關設定在 `ParentLinkUrlParam` 結構體中指定。<br><br>* `SupString`：表示一個字串。相關設定在 `SupContent` 中指定。<br><br>* `ParentLinkURI`：表示使用者請求路徑中的連續片段。路徑不包含查詢字串。相關設定在 `ParentLinkUriParamSup` 中指定。<br><br>* `ParentLinkExpire`：表示使用者請求中權杖的時間標記。參見 `ExpireTimeRule` 下 `Duration` 參數的說明。<br><br>* `AuthToken`：表示基於 `AuthTokenCalRule` 計算的權杖。<br><br>* `ParentFullURI`：表示使用者請求的完整路徑，不包含查詢字串。 |`ParentLinkURI` |
|SupContent |String |否 |當 `ParamType` 是 `SupString` 時，您必須指定該參數。該參數表示您要指定的字串。 |`abc-13343` |
|ParentLinkUriParamSup |Object |否 |表示從使用者請求路徑中獲取物件的方式。當 `ParamType` 是 `ParentLinkURI` 時，您必須指定該參數。<br><br>該參數是一個結構體，包含以下設定：<br><br><br>* 拆分請求路徑所使用的分隔符號。<br><br>* 連續路徑片段的開始層級和結束層級。<br><br>* 拼接這些路徑片段所使用的拼接符。拼接後的路徑片段用於產生權杖。 | |
|JoinSymbol |String |否 |表示拼接這些路徑片段所使用的拼接符，要求如下：<br><br><br>* 長度為 1 個字元，可以是字母、數字、底線（_）、連字元（\-）、反斜線（/）、驚嘆號（!）。 |`00` |
|SplitSymbol |String |否 |表示拆分請求路徑所使用的分隔符號，要求與 `JoinSymbol` 相同。 |`-` |
|StartLevel |Long |否 |表示起始片段所在的層級，要求如下：<br><br><br>* 必須是正整數。<br><br>* 不能大於層級總數。<br><br>* `StartLevel` 所表示的路徑片段不能在 `TermLevel` 所表示的路徑片段右側。 |`1` |
|TermLevel |Long |否 |表示結束片段所在的層級，要求如下：<br><br><br>* 只能是非 0 的整數。<br><br>* 絕對值不能大於層級總數。<br><br><br>如果 `TermLevel` 是負整數，表示從最右邊的片段開始向左計數。 |`3` |
|ParentLinkUrlParam |Object |否 |表示從 URL 中獲取物件的方式。當 `ParamType` 是 `ParentLinkUrlParam` 時，您必須指定該參數。<br><br>該參數是一個結構體，包含物件的來源以及相關設定。 | |
|ArgSegment |Object |否 |表示基於 `ParamName` 或者 `UriLevel` 獲取的內容是否需要被拆分，以提取某個層級的片段。該片段才是您需要獲取的物件。 | |
|Level |Long |否 |表示將獲取到的內容拆分為多個層級的片段後，您需要的物件所在的層級。該參數的要求如下：<br><br><br>* 層級是非 0 的整數。<br><br>* 層級的絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從最右邊層級的片段開始向左計數。<br><br>當 `Switch` 為 `true` 時，您必須指定該參數。 |`2` |
|SplitSymbol |String |否 |表示用於拆分內容的分隔符號。<br><br>當 `Switch` 為 `true` 時，您必須指定該參數。 |`-` |
|Switch |Boolean |否 |表示獲取到的內容是否需要被拆分。該參數有以下取值：<br><br><br>* `true`：表示內容需要被拆分。<br><br>* `false`：表示內容無需被拆分。<br><br><br>該參數的預設值是 `false`。 |`true` |
|CapMode |String |否 |表示物件的來源。該參數有以下取值：<br><br><br>* `name`：表示查詢參數。相關設定在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示請求路徑中指定的目錄。相關設定在 `UriLevel` 和 `ArgSegment` 中指定。 |`name` |
|ParamName |String |否 |當 `CapMode` 是 `name` 時，您必須指定該參數。該參數表示您要指定的查詢參數。 |`myparam5` |
|UriLevel |Long |否 |當 `CapMode` 是 `uri` 時，您必須指定該參數。該參數表示您要指定的目錄層級。<br><br>該參數的要求如下：<br><br><br>* 層級是非 0 的整數。<br><br>* 層級的絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從最右邊的目錄開始向左計數。 |`4` |
|RewriteRule |Object |否 |表示 CDN 在影片分片 URI 中新增權杖的方式。 | |
|CapMode |String |否 |表示 CDN 如何在影片分片 URI 中新增產生的權杖。該參數有以下取值：<br><br><br>* `name`：表示將 URI 中指定的查詢參數設定為權杖。相關設定在 `ParamName` 中指定。<br><br>* `uri`：表示在 URI 中指定的目錄層級插入一個目錄，並將該目錄設定為權杖。相關設定在 `UriLevel` 中指定。 |`name` |
|ParamName |String |否 |當 `CapMode` 是 `name` 時，您必須指定該參數。該參數表示您要指定的查詢參數。 |`myparam4` |
|UriLevel |Long |否 |當 `CapMode` 是 `uri` 時，您必須指定該參數。該參數表示您要指定的目錄層級。<br><br>該參數的要求如下：<br><br><br>* 層級是非 0 的整數。<br><br>* 絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從最右邊層級的目錄開始向左計數。 |`2` |
|SignJoinSymbol |String |否 |表示拼接 `RewriteParam` 中各物件而使用的拼接符。 |`00` |
|Switch |Boolean |否 |表示是否啟用擴充改寫設定。該參數有以下取值：<br><br><br>* `true`：表示啟用擴充改寫設定。<br><br>* `false`：表示不啟用擴充改寫設定。<br><br><br>該參數的預設值是 `false`。 |`true` |
|ExpireTimeRule |Object |否 |表示權杖過期時間的相關設定。 | |
|Duration |Long |否 |表示權杖的有效時長（TTL），單位是秒，取值範圍是 0\-315,360,000，預設值是 `0`。<br><br><br>* 權杖過期時間 = 基於 `ExpTimeCapRule` 獲取的權杖時間標記 + `Duration` |`20` |
|ExpTimeCapRule |Object |否 |表示權杖時間標記的獲取方式。權杖時間標記是一個 Unix 時間標記。 | |
|ArgSegment |Object |否 |表示基於 `ParamName` 或者 `UriLevel` 獲取的內容是否需要被拆分，以提取某個層級的片段。該層級的片段才是您需要獲取的權杖時間標記。 | |
|Level |Long |否 |表示將內容拆分為多個層級的片段後，權杖時間標記所在的層級，要求如下：<br><br><br>* 層級是非 0 的整數。<br><br>* 層級的絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從最右邊的片段開始向左計數。<br><br>當 `Switch` 為 `true` 時，您必須指定該參數。 |`2` |
|SplitSymbol |String |否 |表示用於拆分內容的分隔符號。<br><br>當 `Switch` 為 `true` 時，您必須指定該參數。 |`-` |
|Switch |Boolean |否 |表示獲取到的內容是否需要被拆分。該參數有以下取值：<br><br><br>* `true`：表示內容需要被拆分。<br><br>* `false`：表示內容無需被拆分。<br><br><br>該參數的預設值是 `false`。 |`true` |
|CapMode |String |否 |表示權杖時間標記的來源。該參數有以下取值：<br><br><br>* `name`：表示查詢參數。相關設定在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示請求路徑中的一個目錄。相關設定在 `UriLevel` 和 `ArgSegment` 中指定。<br><br>* `header`：表示請求中的一個標頭。相關設定在 `CustomValue` 中指定。<br><br>* `cookie`：表示請求中的一個 cookie。相關設定在 `CustomValue` 中指定。 |`header` |
|CustomValue |String |否 |該參數的含義如下：<br><br><br>* 當 `CapMode` 是 `header` 時，您必須指定該參數。該參數表示您要指定的請求標頭。<br><br>* 當 `CapMode` 是 `cookie` 時，您必須指定該參數。該參數表示您要指定的 cookie 的 key，CDN 會獲取相應的 value。 |`myheader1` |
|ParamName |String |否 |當 `ParamType` 是 `ReqHeader` 時，您必須指定該參數。該參數表示您要指定的查詢參數。 |`myparm1` |
|UriLevel |Long |否 |當 `ParamType` 是 `uri` 時，您必須指定該參數。該參數表示您要指定的目錄層級。<br><br>該參數的要求如下：<br><br><br>* 層級是非 0 的整數。<br><br>* 層級的絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從路徑最右邊的目錄開始向左計數。 |`2` |
|TimeFormat |String |否 |表示權杖時間標記的格式。<br><br><br>* `octal`：表示八進位。例如 `14751410031`。<br><br>* `decimal`：表示十進位。例如 `1738936345`。<br><br>* `heximal`：表示十六進位。例如 `67a61019`。 |`heximal` |
|RewriteM3U8 |Object |否 |表示 HLS Manifest 改寫的設定，也就是設定如何在 Manifest 中的影片分片 URI 中新增權杖。<br><br>如果 `SignCapRule` 下的 `CapMode` 是 `header` 或 `cookie`，您不能設定該參數。 | |
|RewriteM3U8Tag |Object |否 |表示額外的標籤。對於 `Tags` 中包含的標籤，CDN 會將權杖新增到這些標籤下的 URL 中。參見 [F 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw#m3u8-%E9%A2%9D%E5%A4%96%E6%A0%87%E7%AD%BE%E7%9A%84%E6%94%B9%E5%86%99%E7%A4%BA%E4%BE%8B)。 | |
|Switch |Boolean |否 |表示是否需要設定额外的標籤。該參數有以下取值：<br><br><br>* `true`：表示需要設定额外的標籤。<br><br>* `false`：表示無需設定额外的標籤。<br><br><br>該參數的預設值是 `false`。 |`true` |
|Tags |String[] |否 |表示額外標籤的清單。 |`["tag1","tag2","tag3"]` |
|Switch |Boolean |否 |表示是否需要改寫 HLS Manifest。該參數有以下取值：<br><br><br>* `true`：表示需要改寫 Manifest。<br><br>* `false`：表示無需改寫 Manifest。<br><br><br>預設情況下，CDN 僅對 Manifest 中 `EXTINF` 標籤下的影片分片 URI 新增權杖。 |`true` |
|RewriteMPD |Object |否 |表示 DASH Manifest 改寫的設定，也就是設定如何在 Manifest 中的影片分片 URI 中新增權杖。<br><br>如果 `SignCapRule` 下的 `CapMode` 是 `header` 或 `cookie`，您不能設定該參數。 | |
|MpdVarExpand |Boolean |否 |表示是否要將 `SegmentTemplate` 下 URI 中的變數替換為實際值。該參數有以下取值：<br><br><br>* `true`：表示啟用該設定。該設定啟用後，CDN 會先將影片分片 URI 中的變數替換為實際值，然後基於包含實際值的 URI 產生權杖，最後將權杖新增到 URI 中。<br><br>* `false`：表示不啟用該設定。變數名稱本身會作為固定字串用於產生權杖。<br><br><br>該參數的預設值是 `false`。<br><br>該設定啟用後，目前只有滿足以下所有條件的變數才會被替換為實際值：<br><br><br>* 變數為 `$RepresentationID$`。<br><br>* `SegmentTemplate` 下存在至少一個 URI 符合以下條件：<br><br>   * 在該 URI 中，至少有一個 `$RepresentationID$` 出現的位置不是 URI 路徑中的最後一段。<br><br>* `<SegmentTemplate ... />` 和 `<Representation .../>` 之間不能出現其他內容。<br><br><br>另外，在改寫後的 DASH Manifest 中，原始的 `SegmentTemplate` 會被保留。<br><br>參見 [F 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw#dash-mpd-%E8%AE%8A%E6%95%B8%E6%93%B4%E5%B1%95-%E9%85%8D%E7%BD%AE%E7%9A%84%E9%A1%8D%E5%A4%96%E8%AA%AA%E6%98%8E%E5%92%8C%E7%AF%84%E4%BE%8B)。 |`true` |
|Switch |Boolean |否 |表示是否需要改寫 DASH Manifest。該參數有以下取值：<br><br><br>* `true`：表示需要改寫 Manifest。<br><br>* `false`：表示無需改寫 Manifest。 |`true` |
|SecretKey |Object |否 |表示用於計算權杖的金鑰。包含一個主金鑰和一個備金鑰。 | |
|BackupSecretKey |String |否 |表示備金鑰，長度在 6\-40 個字元之間。 |`secondary-key-456` |
|MasterSecretKey |String |否 |表示主金鑰，長度在 6\-40 個字元之間。 |`primary-key-123` |
|SignCapRule |Object |否 |表示從使用者請求中獲取權杖的方式。 | |
|ArgSegment |Object |否 |表示基於 `ParamName` 或者 `UriLevel` 獲取的內容是否需要被拆分，以提取某個層級的片段。該層級的片段才是您需要獲取的權杖。 | |
|Level |Long |否 |表示將內容拆分為多個層級的片段後，權杖所在的層級，要求如下：<br><br><br>* 層級是非 0 的整數。<br><br>* 層級的絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從最右邊的片段開始向左計數。<br><br>當 `Switch` 為 `true` 時，您必須指定該參數。 |`2` |
|SplitSymbol |String |否 |表示用於拆分內容的分隔符號。<br><br>當 `Switch` 為 `true` 時，您必須指定該參數。 |`//` |
|Switch |Boolean |否 |表示獲取到的內容是否需要被拆分。該參數有以下取值：<br><br><br>* `true`：表示內容需要被拆分。<br><br>* `false`：表示內容無需被拆分。<br><br><br>該參數的預設值是 `false`。 |`true` |
|CapMode |String |否 |表示權杖的來源。該參數有以下取值：<br><br><br>* `name`：表示查詢參數。相關設定在 `ParamName` 中指定。<br><br>* `uri`：表示請求路徑中的一個目錄。相關設定在 `UriLevel` 中指定。<br><br>* `header`：表示請求中的一個標頭。相關設定在 `CustomValue` 中指定。<br><br>* `cookie`：表示請求中的一個 cookie。相關設定在 `CustomValue` 中指定。 |`name` |
|CustomValue |String |否 |該參數的含義如下：<br><br><br>* 當 `CapMode` 是 `header` 時，您必須指定該參數。該參數表示您要指定的請求標頭。<br><br>* 當 `CapMode` 是 `cookie` 時，您必須指定該參數。該參數表示您要指定的 cookie 的 key，CDN 會獲取相應的 value。 |`myheader` |
|ParamName |String |否 |當 `CapMode` 是 `name` 時，您必須指定該參數。該參數表示您要指定的查詢參數。 |`myparam` |
|UriLevel |Long |否 |當 `CapMode` 是 `uri` 時，您必須指定該參數。該參數表示您要指定的目錄層級。<br><br>該參數的要求如下：<br><br><br>* 層級是一個非 0 的整數。<br><br>* 絕對值不能大於層級總數。<br><br><br>如果層級是負整數，表示從路徑最右邊的目錄開始向左計數。 |`3` |
|Condition |Object |否 |表示比對條件的設定。如果一個請求符合比對條件，CDN 對該請求進行 URL 驗證。 | |
|ConditionRule |Object[] |是 |表示一個比對條件清單。清單中最多可以包含 10 個比對條件。 | |
|Object |String |是 |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求檔案的副檔名。<br><br>* `directory`：表示請求路徑中的某個目錄。<br><br>* `path`：表示請求的完整路徑，不包含查詢字串。<br><br>* `regex`：表示用於比對完整路徑的正規表示式。 |`directory` |
|Operator |String |是 |表示比對運算子。該參數有以下取值：<br><br><br>* `match`：表示如果 `Value` 比對了請求中的 `Object`，則該請求符合這個比對條件。<br><br>* `not_match`：表示如果 `Value` 不比對請求中的 `Object`，該請求就符合這個比對條件。 |`match` |
|Type |String |是 |表示比對物件的來源。目前，該參數值只能是 `url`，表示請求 URL。 |`url` |
|Value |String |是 |表示一個或者多個比對值，總長度不能超過 1,024 個字元。多個比對值之間使用分號（;）分隔。比對值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、美元符號（$）、問號（?）。<br><br><br>另外，<br><br><br>* 如果 `Object` 是 `filetype`，每個比對值表示一個檔案副檔名，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個比對值表示一個路徑目錄，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個比對值表示一個完整路徑，不包含查詢字串。完整路徑以斜線（/）開頭。另外，每個比對值中可以包含萬用字元（\*）用來表示一個或者多個任意字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果 `Object` 是 `regex`，每個比對值表示一個正規表示式。例如 `/a{1,2}(.*)g`。 |`/chs/foods/;/us/birds/` |
|Connective |String |是 |表示比對條件之間的關係。該參數有以下取值：<br><br><br>* `OR`：表示關係是 "或"。<br><br>* `AND`：表示關係是 "和"。<br><br><br>該參數的預設值是 `OR`。 |`OR` |
|RuleName |String |否 |表示規則清單中一條規則的名稱，長度不能超過 120 個字元。規則名稱可以包含漢字、字母、數字、連字元（\-）、底線（_）和空格。一個漢字佔 3 個字元。 |`Authentication rule A` |
|RewriteFormat |String |否 |表示改寫後的影片分片 URI 格式。該參數有以下取值：<br><br><br>* `default`：該參數值的含義與 `absolute` 相同。<br><br>* `relative`：保持 URI 的當前格式。需要留意的是，如果 `ExpireTimeRule` 下的 `CapMode` 或者 `SignCapRule` 下的 `CapMode` 為 `uri`，則您不能設定 `RewriteFormat` 為 `relative`。<br><br>* `absolute`：如果 URI 的格式是相對路徑，CDN 將格式轉換成絕對路徑。如果 URI 是絕對路徑或者完整 URL，則保持當前格式。<br><br>* `full`：如果 URI 的格式是絕對路徑或者相對路徑，CDN 將格式轉換成完整 URL。<br><br><br>該參數的預設值是 `default`。 |`default` |


<span id="url-重新導向改寫"></span>
### URL 重新導向改寫


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|RedirectionRewrite |Object |否 |表示 "URL 重新導向改寫" 特性的設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|RedirectionRule |Object[] |否 |表示一個 URL 重新導向改寫的規則的清單。當 `Switch` 是 `true` 時，該參數為必填。該清單最多可以包含 50 條規則。<br><br>清單中的第一條規則具有最高的優先順序。<br><br>當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。 | |
|RedirectionAction |Object |是 |表示一個 URL 重新導向改寫的規則。 | |
|RedirectCode |String |是 |表示 URL 重新導向的回應狀態碼。該參數的取值有 `301`、`302`、`303`、`307`、`308`。<br><br>需要留意的是：<br><br><br>* 對於 301 和 302，如果原請求使用的方法不是 GET，那麼用戶端向新的URL傳送請求時，新請求使用的方法可能變成 GET。<br><br>* 對於 303，新請求使用的方法是 GET。<br><br>* 對於 307 和 308，新請求使用的方法與原請求相同，不會被改變。 |`301` |
|SourcePath |String |是 |表示檔案的原路徑。也就是請求中包含的路徑。路徑必須以斜線（/）開頭並且不能包含雙斜線（//）、百分比符號（%）、空格。該參數值的長度不能超過 1,024 個字元。 |`/img/image.png` |
|TargetHost |String |是 |表示目標路徑所歸屬網站的網域名稱或者 IP 位址。IP 位址必須是 IPv4 類型的位址。該參數值的長度不能超過 1,024 個字元。該參數的預設值就是您的網域名稱。 |`www.test.com` |
|TargetPath |String |是 |表示跳轉後的目標路徑。路徑必須以斜線（/）開頭並且不能包含雙斜線（//）、百分比符號（%）、空格。該參數值的長度不能超過 1,024 個字元。 |`/png/image.png` |
|TargetProtocol |String |是 |表示 URL重新導向後的新請求所使用的協定。該參數有以下取值：<br><br><br>* `followclient`：表示使用原請求的協定。<br><br>* `http`：表示新請求強制使用 HTTP 協定。<br><br>* `https`：表示新請求強制使用 HTTPS 協定。 |`followclient` |
|TargetQueryComponents |Object |是 |表示原請求 URL 中的查詢參數的處理方式。 | |
|Action |String |是 |表示原請求 URL 中的查詢參數的處理方式。該參數有以下取值：<br><br><br>* `include`：表示在跳轉後的 URL 中包含原請求 URL 中的所有查詢參數。<br><br>* `exclude`：表示在跳轉後的 URL 中不包含原請求 URL 中的任何查詢參數。<br><br>* `includePart`：表示在跳轉後的 URL 中包含原請求 URL 中特定的查詢參數。<br><br>* `excludePart`：表示在跳轉後的 URL 中不包含原請求 URL 中特定的查詢參數。 |`include` |
|Value |String |是 |表示要保留或刪除的查詢參數。多個查詢參數間使用英文分號（;）分隔。指定的查詢參數不能包含雙斜線（//）、百分比符號（"）、空格。`Value` 的預設值是 `*`，表示所有的查詢參數。<br><br><br>* 如果 `Action` 是 `include` 或者 `exclude`, 則 `Value` 必須為 `*`。<br><br>* 如果 `Action` 是 `includePart` 或者 `excludePart`，您可以指定一個或者多個查詢參數。此時，您指定的查詢參數不能是 `*`。 |`seq` |


<span id="遠端驗證"></span>
### 遠端驗證


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|RemoteAuth |Object |否 |表示 "遠端驗證" 特性的設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|RemoteAuthRules |Object[] |否 |表示一個驗證規則的清單。目前，清單中只能包含一條規則。該規則包含比對條件設定和驗證設定。當 `Switch` 是 `true` 時，該參數為必填。 | |
|Condition |Object |是 |表示比對條件的設定。如果一個請求滿足比對條件，CDN 對該請求執行 `RemoteAuthRuleAction` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示比對條件清單。清單中最多可以包含 50 個比對條件。<br><br>這些比對條件之間的關係是 "或"。如果一個請求滿足任意比對條件，CDN 就對該請求執行 `RemoteAuthRuleAction` 中指定的操作。 | |
|Object |String |是 |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`filetype` |
|Operator |String |是 |表示比對類型。該參數有以下取值：<br><br><br>* `match`：表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。<br><br>* `not_match`：表示如果 `Value` 不比對請求中的 `Object`，該請求就滿足這個比對條件。<br><br><br>需要留意的是，所有比對條件中的 `Operator` 必須相同。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或者多個比對值，總長度不能超過 1,024 個字元。多個比對值之間使用分號（;）分隔。比對值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、美元符號（$）、問號（?）<br><br><br>同時，<br><br><br>* 如果 `Object` 是 `filetype`，每個比對值表示一個請求 URL 副檔名，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個比對值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個比對值表示一個 URL 路徑，以斜線（/）開頭。每個比對值中可以包含萬用字元（\*）表示一個或者多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png;jpg` |
|RemoteAuthRuleAction |Object |是 |表示驗證相關的設定。<br><br>當一個請求滿足 `Condition` 中的比對條件時，CDN 會將其傳送至驗證伺服器進行驗證，並基於驗證的結果接受或者拒絕該請求。 | |
|AuthModeConfig |Object |是 |表示驗證伺服器的設定。 | |
|MasterRemoteAddr |String |是 |表示驗證伺服器的主位址，長度不能超過 100 個字元。主位址的格式是 `<scheme>://<domain>:<port>` 或 `<scheme>://<ip>:<port>`，其中：<br><br><br>* `<scheme>` 是 `http` 或者 `https`。<br><br>* `<domain>` 不能是 `localhost`。<br><br>* `<ip>` 不能是 `127.0.0.1`。<br><br>* `<port>` 是可選的。 |`https://primary.example.com` |
|PathType |String |是 |表示驗證請求的路徑。驗證位址和請求路徑組成了完整的驗證 URL。CDN 會把使用者的請求轉寄到該驗證 URL。該參數有以下取值：<br><br><br>* `constant`：表示驗證請求中的路徑與使用者請求中的路徑相同。<br><br>* `variable`：表示您需要在 `pathValue` 參數中指定一個驗證請求中的路徑。 |`constant` |
|RequestMethod |String |是 |表示在傳送驗證請求時，CDN 所使用的請求方法。該參數有以下取值：<br><br><br>* `default`：表示驗證請求所使用的方法與使用者的請求相同。<br><br>* `get`：表示驗證請求使用 GET 方法。<br><br>* `post`：表示驗證請求使用 POST方法。<br><br>* `head`：表示驗證請求使用 HEAD 方法。 |`get` |
|BackupRemoteAddr |String |否 |表示驗證伺服器的備用位址。位址格式和要求與主位址相同。 |`https://secondary.example.com` |
|PathValue |String |否 |表示一個驗證請求的路徑，長度不能超過 100 個字元。路徑必須以斜線（/）開頭，不能包含以下字元：<br><br><br>* 雙斜線（//）、百分號（%）、美元符號（$）、空格、問號（?） |`/auth` |
|AuthResponseConfig |Object |是 |CDN 需要對驗證伺服器回傳的驗證狀態碼進行處理。該參數表示相關的設定。 | |
|CacheAction |Object |否 |CDN 可以快取驗證狀態碼。該參數表示相關的設定。 | |
|Action |String |是 |表示 CDN 是否快取驗證狀態碼。該參數有以下取值：<br><br><br>* `nocache`：表示 CDN 不快取驗證狀態碼。<br><br>* `cache`：CDN 快取驗證狀態碼。 |`nocache` |
|Ttl |Long |是 |表示驗證狀態碼的快取時間。單位是秒。取值範圍是 1\-86400。86400秒表示 24小時。 |`5` |
|CacheKey |String[] |否 |快取 key 指定了用於區分不同請求 URI 的查詢參數。每個參數都必須以 `$` 開頭。您也可以指定 [遠端驗證](https://docs.byteplus.com/en/docs/byteplus-cdn/remote-authentication_zh-tw#%E9%A9%97%E8%AD%89%E8%AB%8B%E6%B1%82%E5%8F%83%E6%95%B8)中的參數。 |`[$URI,$host]` |
|ResponseAction |Object |否 |表示驗證失敗時，CDN 如何回應使用者。 | |
|StatusCode |String |否 |表示驗證失敗時，CDN 回應使用者的狀態碼。您可以指定範圍在 400\-499 中的任意一個狀態碼。該參數的預設值是 `403`。 |`403` |
|StatusCodeAction |Object |否 |表示 CDN 對驗證狀態碼的處理方式。 | |
|DefaultAction |String |是 |表示如果驗證狀態碼既不是 `FailCode`，又不是 `SuccessCode` 時，CDN 處理驗證請求的方式。該參數有以下取值：<br><br><br>* `reject`：表示 CDN 認為驗證失敗。<br><br>* `pass`：表示 CDN 認為驗證成功。 |`pass` |
|FailCode |String |是 |表示驗證失敗時的驗證狀態碼。您可以指定範圍在 400\-499 中的一個或者多個狀態碼。多個狀態碼使用英文分號（;）分隔。您也可以指定 4xx 表示 400\-499 中的任意一個狀態碼。 |`403` |
|SuccessCode |String |是 |表示驗證成功時的驗證狀態碼。您可以指定範圍在 200\-299 中的一個或者多個狀態碼。多個狀態碼使用英文分號（;）分隔。您也可以指定 2xx 表示 200\-299 中的任意一個狀態碼。 |`200` |
|TimeOutAction |Object |否 |表示驗證逾時後，CDN 如何處理驗證請求。 | |
|Action |String |是 |表示驗證逾時後，CDN 處理驗證請求的策略。該參數有以下取值：<br><br><br>* `reject`：表示 CDN 認為驗證失敗。<br><br>* `pass`：表示 CDN 認為驗證成功。 |`reject` |
|Time |Long |是 |表示驗證逾時的時間，單位是毫秒，取值範圍是 200 \- 3600。 |`200` |
|QueryStringRules |Object |是 |表示驗證請求的參數設定。 | |
|QueryStringComponents |Object |否 |表示驗證請求參數的設定策略。 | |
|Action |String |否 |表示驗證請求是否包含使用者請求 URL 中的查詢參數。該參數有以下取值：<br><br><br>* `exclude`：表示驗證請求不包含任何查詢參數。<br><br>* `include`：表示驗證請求包含所有查詢參數。<br><br>* `includePart`：表示驗證請求包含指定的查詢參數。 |`exclude` |
|Value |String |否 |表示 `Action` 參數所對應的參數值，長度不能超過1,024 個字元。該參數有以下取值：<br><br><br>* 如果 `Action` 是 `exclude` 或 `include`，`Value` 必須是 `*`。<br><br>* 如果 `Action` 是 `includePart`，您需要在 `Value` 參數中指定使用者請求 URL 中的一個或者多個查詢參數，多個查詢參數使用英文分號（;）分隔。您不能指定 `*`。查詢參數是區分大小寫的，不能包含雙引號（"），也不能包含空格。<br><br><br>該參數的預設值是 `*`。 |`*` |
|QueryStringInstances |Object[] |否 |表示驗證請求中額外的參數設定。您最多可以設定 50 個參數。 | |
|Action |String |否 |表示如何設定驗證請求參數。目前您只能設定 `Action` 為 `set`。`set` 表示設定參數。您需要在 `Key` 中指定您需要設定的驗證請求參數。如果您指定的驗證請求參數不存在，CDN 會在驗證請求中新增該參數。如果您指定的驗證請求參數已存在，CDN 會使用 `Value` 的值作為該驗證請求參數的值。 |`set` |
|Key |String |否 |表示您需要設定的驗證請求參數，長度不能超過 1,024 個字元，不能包含雙引號（"），也不能包含空格。 |`sign` |
|Value |String |否 |表示驗證請求參數的值，長度不能超過 1,024 個字元，並且區分大小寫。`Value`有以下取值：<br><br><br>* 當 `ValueType` 是 `constant` 時，表示驗證請求參數的值是一個常數。您需要指定該常數值。常數值不能以美元符號（$）開頭，也不能包含雙引號（"）。<br><br>* 當 `ValueType` 是 `variable` 時，表示驗證請求參數的值來自一個變數。您可以指定該[遠端驗證](https://docs.byteplus.com/en/docs/byteplus-cdn/remote-authentication_zh-tw#%E9%A9%97%E8%AD%89%E8%AB%8B%E6%B1%82%E5%8F%83%E6%95%B8)中的變數。<br><br>* 當 `ValueType` 是 `customize` 時，表示驗證請求參數的值是清單中的變數與固定字串拼接後的字串。在拼接的字串中，變數使用 `${變數名}` 表示。範例值：`bind${request_uri}to${local_ip}done` |`1235565` |
|ValueType |String |否 |表示您在 `Key` 中設定的驗證請求參數的類型。`ValueType` 有以下取值：<br><br><br>* `constant`：表示驗證請求參數是一個常數。此時，您需要在 `Value` 中指定該常數的值。<br><br>* `variable`：表示驗證請求參數的值來自一個變數。參見 `Value` 的說明。<br><br>* `customize`：表示驗證請求參數的值是一個變數與固定字串拼接後的字串。 |`variable` |
|RequestHeaderRules |Object |是 |表示驗證請求標頭的設定。您最多可以設定 50 個請求標頭。 | |
|RequestHeaderComponents |Object |否 |表示驗證請求標頭的設定策略。 | |
|Action |String |是 |表示驗證請求標頭是否包含使用者請求標頭。該參數有以下取值：<br><br><br>* `exclude`：表示驗證請求標頭中不包含任何使用者請求標頭。<br><br>* `include`：表示驗證請求標頭中包含所有使用者請求標頭。<br><br>* `includePart`：表示驗證請求標頭包含指定的使用者請求標頭。 |`exclude` |
|Value |String |否 |表示 `Action` 參數所對應的參數值，長度不能超過 1,024 個字元。該參數有以下說明：<br><br><br>* 如果 `Action` 是 `exclude` 或 `include`，`Value` 必須是 `*`。<br><br>* 如果 `Action` 是 `includePart`，`Value` 參數的取值是使用者請求中的一個或者多個標頭。多個標頭使用英文分號（;）分隔。其取值不能只是 `*`，不能包含以下字元：<br><br>   * 底線（_）、空格、雙引號（"）<br><br><br>該參數的預設值是 `*`。 |`*` |
|RequestHeaderInstances |Object[] |否 |表示一組驗證請求標頭的設定。<br><br>需要留意的是，在 CDN 發起驗證請求時，請求中可能已經包含了以下標頭：<br><br><br>* `X-Forwarded-Protocol`，`X-Forwarded-Proto`，`X-Client-Scheme`：這三個標頭都表示使用者請求所使用協定，沒有區別。<br><br>* `X-Real-IP`：表示使用者真實的 IP 位址。該標頭的值不會受代理伺服器的影響。<br><br>* `X-Forwarded-For`：表示使用者的 IP 位址。如果使用者的請求經過了代理伺服器，該標頭的值會變成代理伺服器的 IP 位址。<br><br><br>不建議您在該參數中對這些標頭進行設定。如果您設定了這些標頭，這些標頭的原始值會被覆寫。 | |
|Action |String |是 |表示如何設定驗證請求標頭。目前您只能設定該參數值為 `set`。`set` 表示設定請求標頭。此時，您需要在 `Key` 中指定您需要設定的請求標頭。如果您設定的請求標頭不存在，CDN 會在驗證請求中新增該請求標頭。如果您設定的請求標頭已存在，CDN 會使用 `Value` 的值作為該請求標頭的值。 |`set` |
|Key |String |是 |表示您需要設定的請求標頭。請求標頭不能是 `host`，長度不能超過 1,024 個字元，並且不區分大小寫。<br><br>請求標頭不能包含以下字元：<br><br><br>* 底線（_）、空格、雙引號（"） |`x-test-header` |
|ValueType |String |是 |表示請求標頭的類型。該參數有以下取值：<br><br><br>* `constant`：表示請求標頭的值是一個常數。您需要在 `Value` 參數中指定該常數的值。<br><br>* `variable`：表示請求標頭的值來自一個變數。參見 `Value` 的說明。<br><br>* `customize`：表示請求標頭的值是一個變數與固定字串拼接後的字串。 |`variable` |
|Value |String |否 |表示請求標頭的值。該參數有以下取值：<br><br><br>* 當 `ValueType` 是 `constant` 時，您需要指定一個常數值。該常數值的長度不能超過 1,024 個字元，並且區分大小寫。同時，該常數值不能以美元符號（$）開頭，不能包含雙引號（"）。<br><br>* 當 `ValueType` 是 `variable` 時，表示請求標頭的值來自一個變數。您可以指定該 [遠端驗證](https://docs.byteplus.com/en/docs/byteplus-cdn/remote-authentication_zh-tw#%E9%A9%97%E8%AD%89%E8%AB%8B%E6%B1%82%E5%8F%83%E6%95%B8) 中的變數。<br><br>* 當 `ValueType` 是 `customize` 時，表示請求標頭的值是清單中的變數與固定字串拼接後的字串。在拼接的字串中，變數使用 `${變數名}` 表示。範例值：`my${host}is${referer}great` |`1234fdf` |
|RequestHost |String |否 |表示驗證請求中 HOST 標頭的值。該參數的預設值是 `default`，表示 HOST 標頭的值與您的網域名稱相同。 |`www.example.com` |


<span id="下載限速"></span>
### 下載限速


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|DownloadSpeedLimit |Object |否 |表示 "下載限速" 特性的設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|DownloadSpeedLimitRules |Object[] |否 |表示一個限速規則的清單。當 `Switch` 是 `true` 時，該參數為必填。該參數的其他說明如下：<br><br><br>* 每條規則包含比對條件設定和限速設定。<br><br>* 清單中最多可以包含 50 條規則。<br><br>* 清單中規則的出現順序表示規則的優先順序排序。清單中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。 | |
|DownloadSpeedLimitAction |Object |是 |表示限速設定。 | |
|SpeedLimitRate |Long |是 |表示 CDN 在回應單個請求時的最大資料傳輸速度，單位是 `B/S`，使用的進位是 `1,024`。該參數的取值範圍是 1\-1,073,741,824,000,000。`1,073,741,824,000,000` 是 1,000,000 Gbps。 |`500000` |
|SpeedLimitRateAfter |Long |否 |表示一個初始資料量，單位是 `bytes`，使用的進位是 `1,024`。該參數的取值範圍是 0\-1,073,741,824,000,000。<br><br>當 CDN 對一個請求開始傳輸資料時，在傳輸的資料量達到該初始資料量前，該限速規則不會啟用。<br><br>如果該參數值是 `0`，表示在 CDN 對一個請求開始傳輸第一個位元組時，該限速規則就啟用了。 |`1000` |
|SpeedLimitTime |Object |否 |表示限速規則啟用的日期和時間段。 | |
|DayWeek |String |是 |表示該限速規則啟用的日期，有以下取值：`monday`，`tuesday`，`wednesday`，`thursday`，`friday`，`saturday`，`sunday`，`unlimited`。`unlimited` 表示每天。<br><br>您可以指定一個或多個日期，多個日期之間使用分號（;）分隔。 |`monday;friday` |
|BeginTime |String |否 |表示該限速規則啟用的開始時間，格式是 `mm:ss`。<br><br>如果 `DayWeek` 是 `unlimited`, `BeginTime` 會被設定為 `00:00`，您無法更改。 |`05:08` |
|EndTime |String |否 |表示該限速規則啟用的結束時間，格式是 `mm:ss`。<br><br>如果 `DayWeek` 是 `unlimited`, `EndTime` 會被設定為 `23:59`，您無法更改。 |`16:48` |
|Condition |Object |否 |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `DownloadSpeedLimitAction` 中指定的操作。<br><br>如果不指定該參數，CDN 對所有請求執行 `DownloadSpeedLimitAction` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示比對條件清單。目前，清單中只能包含一個比對條件。 | |
|Object |String |是 |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示完整的請求路徑。<br><br>* `unlimited`：表示網域名稱下的所有檔案。<br><br>* `regex`：表示完整的請求路徑，透過正規表示式比對。 |`filetype` |
|Operator |String |是 |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或多個比對值，總長度不能超過 1,024 個字元。多個比對值之間使用分號（;）分隔。比對值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、美元符號（$）、問號（?）<br><br><br>同時，<br><br><br>* 如果 `Object` 是 `filetype`，每個比對值表示一個請求 URL 副檔名，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個比對值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個比對值表示一個 URL 路徑，以斜線（/）開頭。每個比對值中可以包含萬用字元（\*）表示一個或多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果 `Object` 是 `unlimited`，該參數值必須為空（""）。<br><br>* 如果 `Object` 是 `regex`，表示一個或多個正規表示式。多個正規表示式使用分號（;）分隔。例如 `/a/*.jpg`。 |`/www/img/f1/;/www/doc/` |


<span id="快取設定"></span>
## 快取設定

<span id="快取索引鍵"></span>
### 快取索引鍵


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|CacheKey |Object[] |否 |表示 "快取索引鍵" 特性的設定。在該設定中，您可以建立一個規則清單，說明如下：<br><br><br>* 每條規則包含比對條件設定和操作設定。<br><br>* 清單中最多可以包含 50 條規則。<br><br>* 規則在清單中出現的順序表示規則的優先順序。清單中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。<br><br><br>您**必須**在規則清單的最後新增以下預設規則。該預設規則用於比對任何未能比對其他規則的使用者請求。在預設規則中，您可以調整 `CacheKeyAction` 的設定，但不能調整 `Condition` 的設定。<br><br>```json```<br>```{```<br>```            "CacheKeyAction": {```<br>```                "CacheKeyComponents": [```<br>```                    {```<br>```                        "Action": "include",```<br>```                        "IgnoreCase": true,```<br>```                        "Object": "queryString",```<br>```                        "Subobject": "*"```<br>```                    }```<br>```                ]```<br>```            },```<br>```            "Condition": {```<br>```                "ConditionRule": [```<br>```                    {```<br>```                        "Name": "",```<br>```                        "Object": "directory",```<br>```                        "Operator": "match",```<br>```                        "Type": "url",```<br>```                        "Value": "/"```<br>```                    }```<br>```                ]```<br>```            }```<br>```        }```<br> | |
|CacheKeyAction |Object |是 |當一個請求滿足 `Condition` 中的比對條件時，CDN 會為請求檔案設定快取索引鍵。該參數表示快取索引鍵的設定。 | |
|CacheKeyComponents |Object[] |是 |快取索引鍵是由請求中的 host、路徑和查詢字串等部分組成。該參數表示其中各組成部分的設定。目前，您只能對快取索引鍵中包含的查詢字串進行設定。 | |
|Action |String |是 |表示 CDN 如何在請求檔案的快取鍵（Cache Key）中設定查詢字串。該參數有以下取值：<br><br><br>* `exclude`：表示快取鍵不包含請求中的任何查詢參數。<br><br>* `include`：表示快取鍵包含請求中所有的查詢參數。快取鍵中查詢參數的順序與請求 URL 中的順序相同。<br><br>* `includePart`：表示快取鍵僅包含 `Subobject` 中指定的查詢參數。CDN 對包含在快取鍵中的查詢參數按字母順序排序後產生快取鍵。<br><br>* `excludePart`：表示快取鍵包含請求中除了 `Subobject` 中指定的查詢參數之外的所有查詢參數。CDN 對包含在快取鍵中的查詢參數按字母順序排序後產生快取鍵。<br><br><br>说明<br><br>快取鍵中查詢參數的順序會影響快取比對。如果請求 URL 中查詢參數的順序與快取鍵中的查詢參數順序不同，則 CDN 判定請求未命中快取。 |`excludePart` |
|IgnoreCase |Boolean |是 |表示 `Subobject` 是否區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫<br><br><br>該參數的預設值為 `false`，並且僅當 `Action` 是 `includePart` 或 `excluePart` 時有效。 |`true` |
|Object |String |是 |表示快取索引鍵中的一個組成部分。目前該參數值只能是 `querystring`，表示查詢字串。 |`queryString` |
|Subobject |String |是 |該參數對應於 `Action`，表示 CDN 在快取索引鍵中包含的具體查詢參數。該參數的說明如下：<br><br><br>* 如果 `Action` 是 `include` 或 `exclude`，`Subobject` 必須是 `*`，表示請求中的全部查詢參數。<br><br>* 如果 `Action` 是 `includePart` 或 `excludePart`，表示需要保留或不保留的查詢參數。多個查詢參數之間使用分號（;）分隔。您指定的查詢參數不能是 `*`，也不能包含雙斜線（//）、百分號（%）、空格。 |`sign;testParams` |
|Condition |Object |是 |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `CacheKeyAction` 中指定的操作。<br><br>`CacheKey` 中最後一條規則的 `Condition` 必須是以下設定。參見範例請求。<br><br>```json```<br>```"Condition": {```<br>```  "ConditionRule": [```<br>```    {```<br>```      "Object": "directory",```<br>```      "Operator": "match",```<br>```      "Type": "url",```<br>```      "Value": "/"```<br>```    }```<br>```  ]```<br>```}```<br> | |
|ConditionRule |Object[] |是 |表示比對條件清單。清單中只能包含一個比對條件。 | |
|Object |String |是 |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。<br><br>* `regex`：表示請求 URL 中的路徑，透過正規表示式比對。 |`directory` |
|Operator |String |是 |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或多個比對值，總長度不能超過 1,024 個字元。多個比對值之間使用分號（;）分隔。比對值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、美元符號（$）、問號（?）<br><br><br>同時，<br><br><br>* 如果 `Object` 是 `filetype`，每個比對值表示一個請求 URL 副檔名，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個比對值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個比對值表示一個 URL 路徑，以斜線（/）開頭。每個比對值中可以包含萬用字元（\*）表示一個或多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |
|IgnoreCase |Boolean |否 |表示 `Value` 是否區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。<br><br><br>該參數的預設值為 `false` |`true` |


<span id="快取伺服器快取規則"></span>
### 快取伺服器快取規則


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Cache |Object[] |否 |表示 "快取規則" 特性的設定。該特性預設為停用，表示不建立自訂規則。<br><br><br>* 清單中最多可以包含 50 條規則。<br><br>* 清單中規則的順序定義了規則的優先順序。清單中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。<br><br><br>CDN 中有一條 [預設快取規則](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules_zh-tw#%E9%A0%90%E8%A8%AD%E5%BF%AB%E5%8F%96%E8%A6%8F%E5%89%87)，用於比對任何未能比對其他規則的使用者請求。該預設規則始終生效，並且優先順序最低。您**無需**在設定該特性時指定該預設規則。 | |
|CacheAction |Object |是 |當一個請求滿足 `Condition` 中的比對條件時，CDN 會對請求檔案執行指定的操作。該參數定義了該操作相關的設定。 | |
|Action |String |是 |表示 CDN 執行的操作。目前該參數值只能是 `cache`，表示快取請求的檔案。`DefaultPolicy` 中指定了如何快取請求的檔案。 |`cache` |
|IgnoreCase |Boolean |是 |表示 `Value` 是否區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫<br><br><br>該參數的預設值為 `false`。 |`true` |
|Ttl |Long |是 |表示請求檔案的快取時長，單位為`秒`，範圍為 `0-315,360,000`。`315,360,000` 是 10 年。<br><br>如果該參數值為 `0`，CDN 在收到符合規則的請求時，會按以下方式處理：<br><br><br>* 如果檔案尚未被快取，CDN 不會快取該檔案。<br><br>* 如果檔案已被快取，該檔案會立即過期，後續對該檔案的請求將觸發 [回源校驗](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules_zh-tw#%E4%BE%86%E6%BA%90%E4%BC%BA%E6%9C%8D%E5%99%A8%E6%A0%A1%E9%A9%97)。這種情況通常發生在您修改快取規則，將已快取檔案的快取時間從非零值改為 `0` 時。 |`100` |
|DefaultPolicy |String |否 |表示 CDN 對請求檔案的快取行為。該參數有以下取值：<br><br><br>* `force_cache`：對應 CDN 主控台中的 **CDN快取** + **強制快取（開）**  的設定組合。<br><br>* `default`：對應 CDN 主控台中的 **CDN快取** + **強制快取（關）**  的設定組合。<br><br>* `origin_first`：對應 CDN 主控台中的 **遵循來源伺服器** + **補充快取（開）**  的設定組合。<br><br>* `origin_first_Replenish`：對應 CDN 主控台中的 **遵循來源伺服器** + **補充快取（關）**  的設定組合。<br><br>* `no_cache`：對應 CDN 主控台中的 **不快取** 設定。<br><br><br>該參數的預設值是 `default`。關於這些快取策略的描述，參見 [快取規則](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules_zh-tw)。 |`force_cache` |
|SetCookieNoCache |Boolean |否 |表示是否快取包含 Set\-Cookie 頭部的來源伺服器回應。該參數有以下取值：<br><br><br>* `true`：表示 CDN 會快取這類回應。<br><br>* `false`：表示 CDN 不會快取這類回應。<br><br><br>該參數的預設值是 `false`。<br><br>说明<br><br>如果 `DefaultPolicy` 為 `force_cache`，`SetCookieNoCache` 不生效。 |`true` |
|Condition |Object |是 |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `CacheAction` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示比對條件清單。目前，清單中只能包含一個比對條件。 | |
|Object |String |是 |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。<br><br>* `regex`：表示請求 URL 中的路徑，透過正規表示式比對。 |`directory` |
|Operator |String |是 |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或多個比對值，總長度不能超過 1,024 個字元。多個比對值之間使用分號（;）分隔。比對值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、美元符號（$）、問號（?）<br><br><br>同時，<br><br><br>* 如果 `Object` 是 `filetype`，每個比對值表示一個請求 URL 副檔名，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個比對值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個比對值表示一個 URL 路徑，以斜線（/）開頭。每個比對值中可以包含萬用字元（\*）表示一個或多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |


<span id="狀態碼快取規則"></span>
### 狀態碼快取規則


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|NegativeCache |Object[] |否 |表示 "狀態碼快取" 特性的設定。在該設定中，您可以建立一個規則清單，說明如下：<br><br><br>* 每條規則包含過比對條件設定和操作設定。<br><br>* 清單中最多可以包含 50 條規則。<br><br>* 規則在清單中出現的順序表示規則的優先順序。清單中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。 | |
|NegativeCacheRule |Object |是 |當一個請求滿足 `Condition` 中的比對條件時，CDN 會對請求檔案執行指定的操作。該參數定義了該操作相關的設定。 | |
|Action |String |是 |表示 CDN 執行的操作。目前該參數值只能是 `cache`，表示快取來源伺服器的回應狀態碼。 |`cache` |
|StatusCode |String |是 |指定一個需要快取的狀態碼。狀態碼的範圍是 `400-599`。您也可以指定 `4xx` 或 `5xx`。`4xx` 表示 400 到 499 之間的所有狀態碼。`5xx` 表示 500 到 599 之間的所有狀態碼。 |`404` |
|Ttl |Long |是 |表示狀態碼的快取時間。單位是`秒`。時間的範圍是 `1-315,360,000`。`315,360,000` 表示 10 年。 |`100` |
|IgnoreCase |Boolean |否 |表示 `Value` 是否區分大小寫。<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。<br><br><br>該參數的預設值為 `false`。 |`true` |
|Condition |Object |否 |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `NegativeCacheRule` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示比對條件清單。目前，清單中只能包含一個比對條件。 | |
|Object |String |是 |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`directory` |
|Operator |String |是 |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或多個比對值，總長度不能超過 1,024 個字元。多個比對值之間使用分號（;）分隔。比對值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、美元符號（$）、問號（?）<br><br><br>同時，<br><br><br>* 如果 `Object` 是 `filetype`，每個比對值表示一個請求 URL 副檔名，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個比對值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個比對值表示一個 URL 路徑，以斜線（/）開頭。每個比對值中可以包含萬用字元（\*）表示一個或多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |


<span id="瀏覽器快取規則"></span>
### 瀏覽器快取規則


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|BrowserCache |Object[] |否 |表示 "瀏覽器快取" 特性的設定。在該設定中，您可以建立一個規則清單，說明如下：<br><br><br>* 每條規則包含比對條件設定和操作設定。<br><br>* 清單中最多可以包含 50 條規則。<br><br>* 規則在清單中出現的順序表示規則的優先順序。清單中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。 | |
|CacheAction |Object |是 |當一個請求滿足 `Condition` 中的比對條件時，CDN 會對請求檔案執行指定的操作。該參數定義了該操作相關的設定。 | |
|Action |String |是 |表示瀏覽器需要執行的操作。目前該參數值只能是 `cache`，表示快取請求的檔案。`DefaultPolicy` 中指定了如何快取請求的檔案。 |`cache` |
|IgnoreCase |Boolean |是 |表示 `Value` 是否區分大小寫。<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。<br><br><br>該參數的預設值為 `false`。 |`true` |
|Ttl |Long |是 |表示瀏覽器需要快取請求檔案的時長，單位是秒。CDN 會在回應標頭中包含 `Cache-Control: max-age` 標頭，標頭值就是該參數值。 |`100` |
|DefaultPolicy |String |否 |表示瀏覽器該如何快取請求的檔案。該參數有以下取值：<br><br><br>* `cache`：表示需要快取請求的檔案。<br><br>* `origin_first`：表示遵循來自來源伺服器的快取策略。該策略會包含在 CDN 的回應中。<br><br>* `no_cache`：表示不需要快取請求的檔案。<br><br><br>關於瀏覽器快取策略的詳細資訊，參見 [瀏覽器快取策略](https://docs.byteplus.com/en/docs/byteplus-cdn/browser-cache_zh-tw)。 |`cache` |
|SetCookieNoCache |Boolean |否 |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |是 |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `CacheAction` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示比對條件清單。目前，清單中只能包含一個比對條件。 | |
|Object |String |是 |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`directory` |
|Operator |String |是 |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或多個比對值，總長度不能超過 1,024 個字元。多個比對值之間使用分號（;）分隔。比對值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、美元符號（$）、問號（?）<br><br><br>同時，<br><br><br>* 如果 `Object` 是 `filetype`，每個比對值表示一個請求 URL 副檔名，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個比對值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個比對值表示一個 URL 路徑，以斜線（/）開頭。每個比對值中可以包含萬用字元（\*）表示一個或多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |


<span id="http-回應標頭設定"></span>
### HTTP 回應標頭設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|ResponseHeader |Object[] |否 |表示 "HTTP 回應標頭" 特性的設定。 | |
|ResponseHeaderAction |Object |是 |表示 CDN 在回應使用者請求的時候，對回應標頭的操作。 | |
|ResponseHeaderInstances |Object[] |是 |表示一個回應標頭的設定規則清單。每個規則都包含一個標頭的相關操作設定。您最多可以新增 50 條規則。 | |
|Action |String |是 |指定對回應標頭的操作。該參數有以下取值：<br><br><br>* `set`：表示設定一個標頭。設定操作包括新增與修改。如果來源伺服器回應中已包含該標頭，該標頭的值會被覆寫。如果來源伺服器回應中沒有包含該標頭，該標頭會被新增。<br><br>* `delete`，表示刪除一個標頭。 |`set` |
|Key |String |是 |指定一個標頭的名稱。名稱不能超過 1,024個字元，不區分大小寫，不能包含以下字元：<br><br><br>* 底線（_）、空格、雙引號（"）<br><br><br>同時，標頭名稱不能使用這些 [CDN 回應標頭設定](https://docs.byteplus.com/en/docs/byteplus-cdn/response-header-setting_zh-tw#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85)。 |`Content-Disposition` |
|ValueType |String |是 |指定 `Key` 的取值類型。該參數僅當 `Action` 是 `set` 的時候才有效。如果 `Action` 不是 `set`，該參數無效。該參數有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一個字串。<br><br>* `variable`：表示 `Key` 的值來自一個變數。<br><br>* `customize`：表示 `Key` 的值是一個變數與字串拼接後的字串。 |`constant` |
|AccessOriginControl |Boolean |否 |表示在 CDN 回應使用者請求時，是否校驗請求中的 Origin 標頭。<br><br>該參數有以下取值：<br><br><br>* `true`：表示 CDN 會校驗 Origin 標頭。如果校驗成功，CDN 會在回應中包含 Access\-Control\-Allow\-Origin 標頭。標頭值與 Origin 標頭值相同。如果校驗失敗，回應中不會包含 Access\-Control\-Allow\-Origin 標頭。<br><br>* `false`：表示 CDN 不會校驗 Origin 標頭。在回應中，CDN 會包含 Access\-Control\-Allow\-Origin 標頭。標頭值是您設定的 Access\-Control\-Allow\-Origin 的內容。<br><br><br>該參數的預設值是 `false`。<br><br>該參數僅在以下條件都滿足的情況下有效：<br><br><br>* `Action` 是 `set`。<br><br>* `Key` 是 `Access-Control-Allow-Origin`。<br><br>* `ValueType` 是 `constant`。 | |
|Value |String |否 |表示 `Key` 的值。該參數僅當 `Action` 是 `set` 的時候才有效。如果 `Action` 不是 `set`，該參數無效。當 `ValueType` 是 `constant` 時，您需要指定一個字串作為標頭的值。標頭值的長度不能超過 1,024 個字元，不能包含美元符號（$）。<br><br>當 `ValueType` 是 `variable` 時，`Key` 的值可以是來自 [CDN 回應標頭設定](https://docs.byteplus.com/en/docs/byteplus-cdn/response-header-setting_zh-tw#%E8%AE%8A%E6%95%B8%E5%88%97%E8%A1%A8)。除了名稱包含底線的變數，清單中的任何一個變數都可以作為 `Key`，並賦予一個字串來替換其已有的值。也就是說，當您使用任意這些名稱不包含底線的變數作為 `Key` 時，其值是可以被覆寫的。<br><br>當 `ValueType` 是 `customize` 時，表示 `Key` 的值是清單中的變數與字串拼接後的一個字串。在拼接的字串中，變數使用 `${變數名}` 表示。範例值：`${remote_addr}aaa${host}ccc` |`attachment;filename=FileName.xls` |


<span id="自訂錯誤頁面"></span>
### 自訂錯誤頁面


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|CustomErrorPage |Object |否 |表示 "自訂錯誤頁面" 特性的設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|ErrorPageRule |Object[] |否 |表示一個設定規則的集合。您最多可以新增 50 條規則。 | |
|ErrorPageAction |Object |是 |表示規則的相關設定。 | |
|Action |String |否 |表示實際的操作。目前您只能指定該參數值為 `redirect`。表示對用戶端請求進行重新導向。 |`redirect` |
|RedirectCode |String |是 |表示重新導向的回應狀態碼。您可以根據需求選擇合适的狀態碼。該參數的取值有 `301`、`302`、`303`、`307`、`308`。<br><br>需要留意的是：<br><br><br>* 對於 301 和 302，如果原請求使用的方法不是 GET，那麼用戶端向新的URL發送請求時，新請求使用的方法可能變成 GET。<br><br>* 對於 303，新請求使用的方法是 GET。<br><br>* 對於 307 和 308，新請求使用的方法與原請求相同，不會被改變。 |`302` |
|RedirectUrl |String |是 |表示跳轉的目標地址，長度不能超過 1,024 個字元。地址必須包含協定，網域名稱以及路徑，並且符合 URL 的規範。 |`http://www.test.com/friendlyurl.html` |
|StatusCode |String |是 |表示一個狀態碼，取值範圍是 400\-599。您可以輸入 4xx 或者 5xx。4xx 表示 400\-499 之間的所有狀態碼。5xx 表示 500\-599 之間的所有狀態碼。 |`4xx` |


<span id="multi-range"></span>
### Multi\-range


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|MultiRange |Object |否 |表示 "多重範圍（Multi\-range)" 特性的設定。 | |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。該特性啟用後，CDN 允許指定了多重範圍的 Range 請求。<br><br>* `false`：表示不啟用該特性。如果收到一個指定了多重範圍的 Range 請求，CDN 會拒絕該請求並返回 416 回應狀態碼。<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="離線快取"></span>
### 離線快取


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OfflineCache |Object |否 |表示「離線快取」特性的設定。 | |
|Object |String |否 |表示該特性的觸發條件，該參數有以下取值：<br><br><br>* `request_error`：表示來源伺服器請求異常。當來源伺服器請求出現異常時，CDN 沒有獲得來源伺服器的回應。<br><br>* `error_code`：表示來源伺服器的回應狀態碼是 5xx。<br><br>* `request_error,error_code`：表示以上兩個條件都包含。 |`request_error,error_code` |
|StatusCode |String |否 |表示一個或多個回應狀態碼，範圍是 500\-599。多個狀態碼之間使用分號（;）分隔。您也可以輸入 `5xx`，表示任意以數字 5 開頭的狀態碼。<br><br>當 `Object` 是 `error_code` 或 `request_error,error_code` 時，該參數才有效。 |`504;505` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |


<span id="來源伺服器請求設定"></span>
## 來源伺服器請求設定

<span id="range-來源伺服器請求設定"></span>
### Range 來源伺服器請求設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginRange |Boolean |否 |表示 "來源伺服器 Range" 特性的設定。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。<br><br><br>該參數的預設值是 `false`。請求分段大小預設為 1 MB。<br><br>说明<br><br>如果 `Range` 結構體中 `Switch` 為 `true`，則該特性為啟用，即使 `OriginRange` 為 `false`。 |`true` |
|Range |Object |否 |表示分段大小的設定。 | |
|RangeSize |Long |否 |表示分段的大小。<br><br><br>* 如果 `Unit` 是 `MB`，該參數的取值範圍是 1\-40。<br><br>* 如果 `Unit` 是 `KB`，該參數值只能是 `512`。<br><br><br>該參數的預設值是 `1`。 |`512` |
|Switch |Boolean |否 |表示是否啟用此設定。該參數有以下取值：<br><br><br>* `true` ：表示啟用此設定。<br><br>* `false` ：表示停用此設定。<br><br><br>該參數的預設值是 `false` 。 |`true` |
|Unit |String |否 |表示 `RangeSize` 的單位。該參數有以下取值：<br><br><br>* `KB`<br><br>* `MB`<br><br><br>該參數的預設值是 `MB`。 |`KB` |


<span id="來源伺服器請求逾時時間設定"></span>
### 來源伺服器請求逾時時間設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Timeout |Object |否 |表示 "來源伺服器請求逾時" 特性的設定。 | |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。此時，TCP 請求和 HTTP 請求的逾時時間使用預設值，分別是 2 秒和 60 秒。<br><br><br>該參數的預設值是 `false`。 |`true` |
|TimeoutRules |Object[] |否 |表示一組逾時時間的設定。目前您只能指定一個設定。當 `Switch` 是 `true` 時，該參數為必填。 | |
|TimeoutAction |Object |否 |表示逾時時間的設定。 | |
|HttpTimeout |Long |否 |表示 HTTP 請求的逾時時間。該參數的取值範圍是 5\-60。 |`60` |
|TcpTimeout |Long |否 |表示 TCP 請求的逾時時間。該參數的取值範圍是 2\-60。 |`2` |


<span id="來源伺服器請求重新導向跟隨"></span>
### 來源伺服器請求重新導向跟隨


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|FollowRedirect |Boolean |否 |表示 "來源伺服器重新導向跟隨" 特性的設定。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="http-請求標頭設定"></span>
### HTTP 請求標頭設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|RequestHeader |Object[] |否 |表示 "來源伺服器 HTTP 請求標頭" 特性的設定。 | |
|RequestHeaderAction |Object |是 |表示一個請求標頭的設定規則列表。每個規則都包含一個標頭的相關操作設定。您最多可以新增 50 條規則。 | |
|RequestHeaderInstances |Object[] |是 |表示一個請求標頭的設定規則列表。每個規則都包含一個標頭的相關操作設定。您最多可以新增 50 條規則。 | |
|Action |String |是 |指定對請求標頭的操作。該參數有以下取值：<br><br><br>* `set`：表示設定一個標頭。設定操作包括新增與修改。如果請求中已包含該標頭，該標頭的值會被覆蓋。如果請求中沒有包含該標頭，該標頭會被新增。<br><br>* `delete`，表示刪除一個標頭。 |`set` |
|Key |String |是 |指定一個標頭的名稱。名稱的長度不能超過 1,024 個字元，不區分大小寫。同時，名稱不能包含以下字元：<br><br><br>* 底線（_）、空格、雙引號（"）<br><br><br>另外，標頭名稱不能使用這些 [來源伺服器請求標頭設定](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-header_zh-tw#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85)。 |`Cdn-provider` |
|ValueType |String |是 |指定 `Key` 的取值類型。該參數僅當 `Action` 是 `set` 的時候才有效。如果 `Action` 不是 `set`，該參數無效。該參數有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一個固定字串。<br><br>* `variable`：表示 `Key` 的值來自一個變數。<br><br>* `customize`：表示 `Key` 的值是變數與固定字串拼接後的一個字串。 |`constant` |
|Value |String |否 |表示 `Key` 的值。該參數僅當 `Action` 是 `set` 的時候才有效。如果 `Action` 不是 `set`，該參數無效。當 `ValueType` 是 `constant` 時，您需要指定一個字串作為標頭的值。該標頭值的長度不能超過 1,024 個字元，不能包含貨幣符號（$）。<br><br>當 `ValueType` 是 `variable` 時，`Key` 的值可以是來自 [來源伺服器請求標頭設定](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-header_zh-tw#%E8%AE%8A%E6%95%B8%E5%88%97%E8%A1%A8)。除了名稱包含底線的變數，列表中的任何一個變數都可以作為 `Key`，並賦予一個字串來替換其已有的值。也就是說，當您使用任意這些名稱不包含底線的變數作為 `Key` 時，其值是可以被覆蓋的。<br><br>當 `ValueType` 是 `customize` 時，表示 `Key` 的值是列表中的變數與字串拼接後的字串。在拼接的字串中，變數使用 `${變數名}` 表示。範例值：`aaa${http_host}bbb${msec}ccc` |`bp-cdn` |


<span id="來源伺服器請求參數設定"></span>
### 來源伺服器請求參數設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginArg |Object[] |否 |表示 "來源伺服器參數" 設定的規則列表。<br><br><br>* 列表中最多可以包含 50 條規則。<br><br>* 每條規則包含一個匹配條件（`Condition`）和 CDN 執行操作（`OriginArgAction`）。<br><br>* 列表中規則的順序定義了規則的優先順序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 會依照規則的優先順序，從高到低將規則與請求進行比對。如果有一條規則比對成功，CDN 就會停止處理其餘的規則。<br><br><br>您**必須**在規則列表的最後新增以下這條預設規則。該預設規則用於匹配任何未能匹配其他規則的使用者請求。您不可更改該規則中的 `Condition`，但可以更改 `OriginArgAction` 中的設定。<br><br>```json```<br>```{```<br>```            "Condition": {```<br>```                "ConditionRule": [```<br>```                    {```<br>```                        "Object": "directory",```<br>```                        "Operator": "match",```<br>```                        "Type": "url",```<br>```                        "Value": "/"```<br>```                    }```<br>```                ]```<br>```            },```<br>```            "OriginArgAction": {```<br>```                "OriginArgComponents": [```<br>```                    {```<br>```                        "Action": "include",```<br>```                        "Object": "queryString",```<br>```                        "Subobject": "*"```<br>```                    }```<br>```                ]```<br>```            }```<br>```        }```<br> | |
|Condition |Object |是 |表示匹配條件的設定。如果請求滿足該匹配條件，CDN 執行 `OriginArgAction` 中指定的操作。目前您必須且只能指定一個條件。 | |
|ConditionRule |Object[] |是 |表示一個匹配條件的列表。目前，列表中只能包含一個匹配條件。 | |
|Object |String |是 |表示匹配類型。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。<br><br>* `regex`：表示請求 URL 中的完整路徑，透過正規表示式匹配。 |`directory` |
|Operator |String |是 |表示匹配類型。目前，該參數值只能是 `match`，表示只有匹配成功才算是滿足了匹配條件。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或者多個匹配值，總長度不能超過 1,024 個字元。多個匹配值之間使用分號（;）分隔。匹配值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、貨幣符號（$）、問號（?）<br><br><br>同時，<br><br><br>* 如果 `Object` 是 `filetype`，每個匹配值表示一個請求 URL 後綴，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個匹配值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個匹配值表示一個 URL 路徑，以斜線（/）開頭。每個匹配值中可以包含萬用字元（\*）表示一個或者多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果 `Object` 是 `regex`，每個匹配值表示一個正規表示式。關於正規表示式的範例，參見 [來源伺服器請求參數設定](https://docs.byteplus.com/en/docs/byteplus-cdn/query-parameter_zh-tw#%E5%85%A8%E8%B7%AF%E5%BE%91%E6%AD%A3%E5%89%87%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 |`/` |
|OriginArgAction |Object |是 |表示在請求滿足 `Condition` 時 CDN 執行的操作。 | |
|OriginArgComponents |Object[] |是 |表示一個操作列表。這些操作定義了 CDN 如何處理來源伺服器請求中的查詢參數。<br><br>目前，列表中只能包含一個操作。 | |
|Action |String |是 |表示 CDN 執行的操作。該參數有以下取值：<br><br><br>* `include`: 表示來源伺服器請求 URL 中包含使用者請求 URL 中的全部查詢參數。<br><br>* `exclude`：表示來源伺服器請求 URL 中不包含使用者請求 URL 中的任何查詢參數。<br><br>* `addPart`：表示來源伺服器請求 URL 中包含使用者請求 URL 中的全部查詢參數，並額外包含 `Subobject` 中指定的查詢參數。<br><br>* `includePart`：表示如果使用者請求 URL 中包含 `Subobject` 中指定的查詢參數，那麼來源伺服器請求 URL 中包含這些指定的查詢參數。<br><br>* `excludePart`：表示來源伺服器請求 URL 中包含使用者請求 URL 中的全部查詢參數，除了`Subobject` 中指定的查詢參數。<br><br>* `set`：表示來源伺服器請求 URL 中包含使用者請求 URL 中的全部查詢參數。同時，對於您在 `Subobject` 中指定的查詢參數和參數值，CDN 會執行以下操作:<br><br>   * 如果這些查詢參數在使用者請求 URL 中，CDN 會在來源伺服器請求 URL 中將這些參數的值設定為您指定的值。<br><br>   * 如果使用者請求 URL 中不包含這些查詢參數，CDN 會在來源伺服器請求 URL 中新增這些查詢參數。 |`exclude` |
|Object |String |是 |表示 CDN 對哪個對象執行 `Action`。目前，該參數值只能是 `queryString`，表示請求 URL 中的查詢字串。 |`queryString` |
|Subobject |String |是 |表示一個或者多個查詢參數。多個查詢參數之間使用分號（;）分隔，總長度不能超過 1,024 個字元。`Subobject` 只能包含字母、數字、底線（_）、逗號（,）、連字號（\-）、句點（.）和驚嘆號（!）。<br><br>在匹配請求 URL 中的查詢參數時，`Subobject` 中的參數是大小寫敏感的。<br><br>`Subobject` 的額外說明如下：<br><br><br>* 當 `Action` 是 `include` 或 `exclude` 時，`Subobject` 必須是 `*`，表示請求 URL 中的所有查詢參數。<br><br>* 當 `Action` 是 `includePart` 或 `excludePart` 時，`Subobject` 表示一個或者多個查詢參數。例如 `param1;param2`。<br><br>* 當 `Action` 是 `addPart` 或 `set` 時，`Subobject` 表示一個或者多個查詢參數和參數值，格式是 `key=value`。例如 `param1=val1;param2=val2;param3=val3`。 |`*` |


<span id="來源伺服器請求-sni-設定"></span>
### 來源伺服器請求 SNI 設定


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginSni |Object |否 |表示 "來源伺服器 SNI" 特性的設定。 | |
|SniDomain |String |否 |指定來源伺服器 SNI 的網域名稱。當 `Switch` 是 `true` 時，該參數為必填。該參數值的長度不能超過 1,024 個字元。 |`img.example.com` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="來源伺服器路徑改寫"></span>
### 來源伺服器路徑改寫


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|OriginRewrite |Object |否 |表示 "來源伺服器 URL 改寫" 特性的設定。 | |
|OriginRewriteRule |Object[] |否 |表示一個規則列表。當 `Switch` 是 `true` 時，該參數為必填。<br><br><br>* 列表中最多可以包含 50 條規則。<br><br>* 列表中規則的順序定義了規則的優先順序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 按規則的優先順序，從高到低嘗試將請求與規則匹配。如果請求匹配了一條規則，CDN 就停止處理其餘規則。 | |
|OriginRewriteAction |Object |否 |表示 CDN 執行的動作。 | |
|SourcePath |String |否 |表示一個正規表示式，長度不能超過 1,024 個字元，用於匹配使用者請求 URL 中的路徑。參見 [設定範例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn#%E8%B7%AF%E5%BE%84%E6%94%B9%E5%86%99%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 |`^/img/food.png$` |
|TargetPath |String |否 |表示改寫後的路徑，長度不能超過 1,024 個字元。<br><br>您可以在 `TargetPath` 中使用 `$1` 、 `$2` 、 `$3` 等捕獲 `SourcePath` 中定義的組。<br><br>參見 [設定範例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn#%E8%B7%AF%E5%BE%84%E6%94%B9%E5%86%99%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 |`/png/food.webp` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="內容最佳化"></span>
## 內容最佳化

<span id="智慧壓縮"></span>
### 智慧壓縮


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Compression |Object |否 |表示 "智能壓縮" 特性的設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|CompressionRules |Object[] |否 |表示一組規則。每條規則包含匹配條件設定以及操作設定。 | |
|CompressionAction |Object |是 |表示當使用者請求滿足 `Condition` 時，CDN 對請求檔案執行的壓縮操作的設定。 | |
|CompressionType |String[] |是 |表示 CDN 使用的壓縮演算法。該參數有以下取值：<br><br><br>* `br`：表示 Brotli 壓縮演算法。<br><br>* `gzip`：表示 Gzip 壓縮演算法。<br><br><br>您可以同時指定這兩個演算法。<br><br>需要留意的是，CDN 基於使用者請求中 `Accept-Encoding` 標頭來決定是否對請求檔案進行壓縮以及使用的壓縮演算法。 |`["gzip","br"]` |
|CompressionFormat |String |否 |表示 CDN 基於請求中的 `Content-Type` 標頭對請求進行匹配。該參數有以下取值：<br><br><br>* `default`：表示如果 `Content-Type` 標頭值在下方的預設列表中，CDN 對請求檔案執行 `CompressionAction` 中設定的操作。<br><br>* `customize`：表示如果 `Content-Type` 標頭值在 `CompressionFormat` 指定的標頭值中，CDN 對請求檔案執行 `CompressionAction` 中設定的操作。<br><br><br>如果您需要 CDN 基於 `Condition` 中的匹配條件對請求進行匹配，您無需指定 `CompressionFormat` 或者指定 `CompressionFormat` 為 `all`。<br><br>**預設列表**<br><br>text/html、text/xml、text/plain、text/css、application/javascript、application/x\-javascript、application/rss+xml、text/javascript、image/tiff、image/svg+xml、application/json、application/xml、text/plain; charset=utf\-8 |`customize` |
|CompressionTarget |String |否 |表示 `Content-Type` 的過濾值。<br><br><br>* 如果 `CompressionFormat` 為 `default` 或者 `all`，該參數必須為 `*`。<br><br>* 如果 `CompressionFormat` 為 `customize`，您需要指定一個或者多個檔案類型。多個檔案類型之間以逗號（,）分隔。 |`application/xml,hello/world` |
|MinFileSizeKB |Long |否 |表示檔案大小範圍的最小值，CDN 僅對大小在 `MinFileSizeKB` 和 `MaxFileSizeKB` 所表示的範圍內的檔案進行壓縮。該參數的取值範圍是 0 \- 2,147,483,647，單位是 KB，使用的進位是 1,024。該參數的預設值是 `0`。 |`10` |
|MaxFileSizeKB |Long |否 |表示檔案大小範圍的最大值，取值範圍是 0 \- 2,147,483,647，單位是 KB，使用的進位是 1,024。如果不指定該參數，表示您不限制檔案大小的上限。 |`1000` |
|Condition |Object |否 |表示匹配條件的設定。如果請求匹配了某个條件，CDN 對該請求執行 `CompressionAction` 中指定的操作。<br><br>需要留意的是，如果您指定了 `CompressionFormat`，`Condition` 必須為 `null` 或者不指定。 | |
|ConditionRule |Object[] |是 |表示匹配條件列表。目前，列表中只能包含一個匹配條件。 | |
|Object |String |是 |表示匹配對象。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`directory` |
|Operator |String |是 |表示匹配類型。該參數的值只能是 `match`，表示如果 `Value` 匹配了請求中的 `Object`，該請求就滿足這個匹配條件。 |`match` |
|Type |String |是 |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |是 |表示一個或者多個匹配值，總長度不能超過 1,024 個字元。多個匹配值之間使用分號（;）分隔。匹配值不能包含以下字元：<br><br><br>* 雙斜線（//）、空格、貨幣符號（$）、問號（?）<br><br><br>同時，<br><br><br>* 如果 `Object` 是 `filetype`，每個匹配值表示一個請求 URL 後綴，無需以句點（.）開頭，只能包含字母和數字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每個匹配值表示一個目錄路徑，以斜線（/）開頭和結尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每個匹配值表示一個 URL 路徑，以斜線（/）開頭。每個匹配值中可以包含萬用字元（\*）表示一個或者多個字元。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`/img/` |


<span id="頁面最佳化"></span>
### 頁面最佳化


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|PageOptimization |Object |否 |表示 "頁面最佳化" 特性的設定。 | |
|OptimizationType |String[] |是 |表示最佳化的對象。該參數有以下取值：<br><br><br>* `html`: 表示 HTML 頁面。<br><br>* `js`: 表示 Javascript 程式碼。<br><br>* `css`: 表示 CSS 程式碼。<br><br><br>該參數的預設值是 `html`。如果您指定了 `js` 或者 `js`，`html` 也必須指定。 |`["html","js"]` |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |


<span id="影片拖曳"></span>
### 影片拖曳


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|VideoDrag |Object |否 |表示 "影片拖曳" 特性的設定。 | |
|Switch |Boolean |是 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |


<span id="高級設定"></span>
## 高級設定

<span id="共享快取"></span>
### 共享快取


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|CacheHost |Object |否 |表示 "共享快取" 特性的設定。要使用該特性，請 [提交工單](https://console.byteplus.com/workorder/create)。<br><br>如果您要對多個網域名稱設定共享快取，您需要呼叫該 API 對每個網域名稱設定目標網域名稱。 | |
|CacheHostRule |Object[] |否 |表示一組共享快取的設定。目前您只能只能建立一個設定。當 `Switch` 是 `true` 時，該參數為必填。 | |
|CacheHostAction |Object |否 |表示設定的詳情。 | |
|CacheHost |String |否 |表示目標網域名稱。 該目標網域名稱必須是您帳戶下的一個網域名稱。該參數指示 `Domain` 共享 `CacheHost` 的 CDN 快取。 |`www.test.com` |
|Switch |Boolean |否 |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。<br><br><br>該參數的預設值是 `false`。 |`true` |


<span id="回應"></span>
## 回應

<span id="更新結果"></span>
## 更新結果

<span id="各網域名稱更新結果"></span>
### 各網域名稱更新結果


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|DeployResult |Object[] |表示 `Domains` 清單中各網域名稱的設定更新結果。該參數僅當 `Aggregate` 是 `false` 時才會出現。 | |
|Domain |String |表示 `Domains` 清單中的一個網域名稱。 |`www.example.com` |
|ErrorMsg |String |表示更新失敗的原因。該參數僅當 `Status` 是 `fail` 時才會出現。 |`some error` |
|Status |String |表示該網域名稱的設定更新結果。該參數有以下取值：<br><br><br>* `success`：表示該網域名稱的設定更新成功。<br><br>* `fail`：表示該網域名稱的設定更新失敗。 |`fail` |


<span id="请求示例-1"></span>
## 请求示例 1

```json
POST https://cdn.byteplusapi.com/?Action=BatchUpdateCdnConfig&Version=2021-03-01
{
    "Domains": [
        "www.example.com",
        "img.example.com",
        "videos.example.com"
    ],
    "OriginProtocol": "http",
    "HTTPS": {
        "Switch": true,
        "OCSP": true
    },
    "Aggregate": true
}
```


<span id="返回示例-1"></span>
## 返回示例 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202410091237542EE1A0C61B73114E0B08",
        "Action": "BatchUpdateCdnConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1",
        "Error": {
            "Code": "InvalidParameter.Domain.xxxxx",
            "Message": "some error"
        }
    }
}
```


<span id="请求示例-2"></span>
## 请求示例 2

```json
POST https://cdn.byteplusapi.com/?Action=BatchUpdateCdnConfig&Version=2021-03-01
{
    "Domains": [
        "www.example.com",
        "img.example.com",
        "videos.example.com"
    ],
    "OriginProtocol": "http",
    "HTTPS": {
        "Switch": true,
        "OCSP": true
    },
    "Aggregate": false
}
```


<span id="返回示例-2"></span>
## 返回示例 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20241009141640E5DE873D9A01D9F72861",
        "Action": "BatchUpdateCdnConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DeployResult": [
            {
                "Domain": "www.example.com",
                "Status": "success"
            },
            {
                "Domain": "img.example.com",
                "ErrorMsg": "error message 1",
                "Status": "fail"
            },
            {
                "Domain": "videos.example.com",
                "ErrorMsg": "error message 2",
                "Status": "fail"
            }
        ]
    }
}
```


&nbsp;
