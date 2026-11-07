---
title: "DescribeTemplates"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw"
---

獲取符合篩選條件的策略列表。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeTemplates&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeTemplates`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Filters |Object[] |否 |表示一組篩選條件，用於獲取符合條件的策略列表。如果您不指定任何篩選條件，該 API 則返回所有您帳戶下的策略。<br><br>多個篩選條件之間是 "與" 的關係，即只有滿足所有篩選條件，一個策略才會包含在該 API 返回的策略列表中。<br><br>在該 API 的回應中，實際返回的策略受 `PageNum` 和 `PageSize` 的影響。 | |
|Fuzzy |Boolean |否 |表示匹配方式。該參數有以下取值：<br><br><br>* `true`：表示模糊匹配。在策略的匹配過程中，如果 `Name` 的對應值包含 `Value` 陣列中的任意值，該策略就被認為是符合篩選條件。<br><br>* `false`：表示精確匹配。如果 `Name` 的對應值與 `Value` 陣列中的值相同，該策略就被認為是符合篩選條件。<br><br>   同時，您可以指定的 `Fuzzy` 值會受到 `Name` 值的影響。 參見 `Name` 的描述。<br><br><br>該參數的預設值是 `false`。<br><br>需要留意的是，匹配過程是大小寫敏感的。 |`true` |
|Name |String |否 |表示篩選類型。該參數有以下取值：<br><br><br>* `Title`：表示按名稱對策略進行篩選。<br><br>* `Id`：表示按 ID 對策略進行篩選。對於該參數值，`Fuzzy` 的值只能是 `false`<br><br>* `Domain`：表示按網域名稱對綁定該網域名稱的策略進行篩選。<br><br>* `Type`：表示按類型對策略進行篩選。對於該參數值，`Fuzzy` 的值只能是 `false`。<br><br>* `Status`：表示按狀態對策略進行篩選。對於該參數值，`Fuzzy` 的值只能是 `false`。<br><br><br>您可以同時指定多個篩選條件，但是不同篩選條件中的 `Name` 不能相同。 |`Title` |
|Value |String[] |否 |表示 `Name` 對應的值，是一個陣列。<br><br><br>* 當 `Name` 是 `Title`、`Id` 或 `Domain` 時，`Value` 陣列中每個值的長度不能超過 100 個字元。<br><br>* 當 `Name` 是 `Type` 時，`Value` 陣列中可以包含以下一個或者多個值：<br><br>   * `cipher`：表示加密策略。<br><br>   * `service`：表示分發策略。<br><br>   * `rule`：表示規則引擎策略。<br><br>* 當 `Name` 是 `Status` 時，`Value` 陣列中可以包含以下一個或者多個值：<br><br>   * `locked`：表示狀態是 "已發布"。<br><br>   * `editing`：表示狀態是 "草稿"。<br><br><br>說明<br><br><br>* 當 `Fuzzy` 是 `false` 時，您可以在陣列中指定多個值。<br><br>* 當 `Fuzzy` 是 `true` 時，您只能在陣列中指定一個值。 |`["NetTVWeb001","NetTV003"]` |
|PageNum |Long |否 |對於 API 返回的策略列表，該參數表示一個頁碼。該 API 實際返回的策略是該頁碼所指定的分頁上的那些策略。<br><br>該 API 返回的策略是根據 PageSize 而分頁的。假設該 API 返回的策略數量是 100，您指定的 `PageSize` 是 `10`，那麼返回的策略是分布在 10 個頁上。如果您指定的 `PageNum` 是 `2`，表示獲取第 2 頁上的那些策略。<br><br>如果您指定的分頁上沒有策略，則返回結果中 `Templates` 參數的值為 `null`。<br><br>`PageNum` 的預設值是 `1`。 |`1` |
|PageSize |Long |否 |表示每個分頁包含的策略數量。<br><br>該參數的取值範圍是 1\-200，預設值是 `10`。 |`10` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Templates |Object[] |表示該 API 回應的策略列表。<br><br>需要留意的是，列表中的策略是請求參數 `PageNum` 所表示的分頁上的那些策略，不一定是所有符合篩選條件的策略。 | |
|BoundDomains |Object[] |表示一個與 `TemplateId` 所指定的策略綁定的網域名稱列表。 如果該策略未與任何網域名稱綁定，該參數值為 `null`。 | |
|BoundTime |Long |表示該策略與 `Domain` 所指定的網域名稱綁定的時間，格式是 `Unix` 時間標記。 |`1709174039` |
|Domain |String |表示一個與該策略綁定的網域名稱。 |`www.example.com` |
|CreateTime |Long |表示該策略的建立時間，格式是 Unix 時間標記。 |`1709173909` |
|Message |String |表示該策略的描述。 |`This is a test` |
|Status |String |表示 `ProdVersion` 的狀態，該參數有以下取值：<br><br><br>* `editing`：表示狀態為 "草稿"。此時， `ProdVersion` 的值為空（""）。<br><br>* `locked`：表示狀態為 "已發布"。 |`locked` |
|TemplateId |String |表示 API 回傳的策略列表中一個策略的 ID。 |`tpl-sZRpwq` |
|Title |String |表示該策略的名稱。 |`NetTVWeb001` |
|Type |String |表示該策略的類型。該參數有以下取值：<br><br><br>* `cipher`：表示加密策略。<br><br>* `service`：表示分發策略。<br><br>* `rule`：表示規則引擎策略。 |`cipher` |
|UpdateTime |Long |表示該策略的最近修改時間，格式是 Unix 時間標記。<br><br>如果該策略自建立後未被更新，該參數值與 `CreateTime` 的值相同。 |`1709174039` |
|Exception |Boolean |表示該策略是否包含特殊配置。特殊配置指的是那些不由使用者，而是由 BytePlus 工程師操作的設定。該參數有以下取值：<br><br><br>* `true`：表示包含特殊配置。<br><br>* `false`：表示不包含特殊配置。 |`false` |
|Project |String |表示該策略所歸屬的專案。 |`default` |
|ProdVersion |String |表示該策略下已發布，也就是狀態為 `running` 的版本。如果不存在狀態為 `running` 的版本，該參數值為空（""）。 |`P-250411.32717` |
|DomainCount |Long |域名数量 | |
|TotalCount |Long |表示符合篩選條件的策略數量。該參數值不受 `PageSize` 和 `PageNum` 的影響。 |`2` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplates&Version=2021-03-01
{
    "Filters": [
        {
            "Name": "Title",
            "Fuzzy": false,
            "Value": [
                "NetTVWeb001",
                "NetTV003"
            ]
        },
        {
            "Name": "Id",
            "Fuzzy": false,
            "Value": [
                "tpl-sZRpwq",
                "tpl-sWm5EW"
            ]
        },
        {
            "Name": "Domain",
            "Fuzzy": true,
            "Value": [
                "example.com"
            ]
        },
        {
            "Name": "Type",
            "Fuzzy": false,
            "Value": [
                "cipher",
                "service"
            ]
        },
        {
            "Name": "Status",
            "Fuzzy": false,
            "Value": [
                "locked",
                "editing"
            ]
        }
    ]
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202403030536061418EF0E947E85EC76B6",
        "Action": "DescribeTemplates",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Templates": [
            {
                "BoundDomains": [
                    {
                        "BoundTime": 1709174039,
                        "Domain": "www.example.com"
                    }
                ],
                "CreateTime": 1709173909,
                "Exception": false,
                "Message": "",
                "Project": "default",
                "Status": "locked",
                "TemplateId": "tpl-sZRpwq",
                "Title": "NetTVWeb001",
                "Type": "service",
                "UpdateTime": 1709174039,
                "ProdVersion": "P-250411.32717"
            },
            {
                "BoundDomains": null,
                "CreateTime": 1709018409,
                "Exception": false,
                "Message": "Rewrite",
                "Project": "default",
                "Status": "editing",
                "TemplateId": "tpl-sWm5EW",
                "Title": "NetTV003",
                "Type": "service",
                "UpdateTime": 1709018409,
                "ProdVersion": ""
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
