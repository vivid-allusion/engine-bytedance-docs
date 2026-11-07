---
title: "DescribeTemplateOperations"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateOperations_zh-tw"
---

獲取指定策略的操作歷史。操作歷史最多包含 10 條記錄。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateOperations&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeTemplateOperations`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示要查詢的策略 ID。 |`tpl-s5wzdn0` |
|PageSize |Long |否 |該 API 對獲取的記錄進行分頁。該參數表示每頁包含的記錄數量。該參數的取值範圍是 1\-50，預設值是 `10`。 |`10` |
|PageNum |Long |否 |表示展示哪個分頁上的記錄。該參數的值只能是 `1`，預設值也是 `1`。 |`1` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Operations |Object[] |表示指定策略的操作歷史，最多包含 10 條記錄。列表中的記錄按 `OperateTime` 排序，第一條記錄對應最近的操作。 | |
|Action |String |表示所記錄的操作。該參數有以下取值：<br><br><br>* `bind`：表示網域名稱綁定。<br><br>* `create`：表示策略建立。<br><br>* `release`：表示策略發佈。 |`bing` |
|DomainsAfter |Object[] |如果 `Action` 是 `bind`，該參數表示綁定的網域名稱資訊。如果 `Action` 不是 `bind`，該參數值為 `null`。 | |
|Domain |String |表示綁定的網域名稱。 |`abc.example.com` |
|DomainsBefore |Object[] |如果 `Action` 是 `bind`，該參數表示綁定操作前，該策略所綁定的網域名稱資訊。<br><br>在以下任意情況下，該參數值為 `null`：<br><br><br>* `Action` 不是 `bind`。<br><br>* 所記錄的操作是首次綁定網域名稱。 | |
|Domain |String |表示綁定操作前，該策略所綁定的網域名稱。 |`www.example.com` |
|OperateTime |Long |表示記錄的操作時間，格式是 Unix 時間標記，精確到秒。 |`1755314680` |
|Total |Long |表示操作歷史中的記錄數量。 |`3` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateOperations&Version=2021-03-01
{
    "TemplateId": "tpl-s5wzdn0"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910090657D2AD1B292BAAA8BF5384",
        "Action": "DescribeTemplateOperations",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Operations": [
            {
                "Action": "release",
                "DomainsAfter": [
                    {
                        "Domain": "www.example.com"
                    }
                ],
                "DomainsBefore": [
                    {
                        "Domain": "abc.example.com"
                    }
                ],
                "OperateTime": 1755323476
            },
            {
                "Action": "bind",
                "DomainsAfter": [
                    {
                        "Domain": "abc.example.com"
                    }
                ],
                "DomainsBefore": null,
                "OperateTime": 1755314680
            },
            {
                "Action": "release",
                "DomainsAfter": null,
                "DomainsBefore": null,
                "OperateTime": 1755312538
            },
            {
                "Action": "create",
                "DomainsAfter": null,
                "DomainsBefore": null,
                "OperateTime": 1755309241
            }
        ],
        "Total": 4
    }
}
```


&nbsp;
