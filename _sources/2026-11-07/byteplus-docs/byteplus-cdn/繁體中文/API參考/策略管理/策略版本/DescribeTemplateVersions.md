---
title: "DescribeTemplateVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateVersions_zh-tw"
---

對指定策略進行溯源，獲取建立歷史記錄。當前，該 API 最多展示 10 條記錄。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateVersions&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeTemplateVersions`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示要進行溯源的策略 ID。 |`tpl-s5o2jz6` |
|PageSize |Long |否 |該 API 對獲取的記錄進行分頁。該參數表示每頁包含的記錄數量。該參數的取值範圍是 1\-50，預設值是 `10`。 |`10` |
|PageNum |Long |否 |表示展示哪個分頁上的記錄。該參數的值只能是 `1`，預設值也是 `1`。 |`1` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Total |Long |表示該 API 獲取的記錄總數。 |`3` |
|Versions |Object[] |表示指定策略的建立歷史，最多包含 10 條記錄。列表中的記錄按 `OperateTime` 排序，第一條記錄對應最近的操作。 | |
|Action |String |對於 `ReferredId` 所表示的策略，該參數表示對該策略的操作，有以下取值：<br><br><br>* `create`：表示建立。<br><br>* `duplicate`：表示複製。 |`create` |
|OperateTime |Long |表示 `Action` 發生的時間，格式是 Unix 時間標記，精確到秒。 |`1757489199` |
|ReferredId |String |表示所記錄策略的來源。<br><br><br>* 如果 `Action` 是 `duplicate`，該參數表示所記錄策略是從哪個策略複製而來的。<br><br>* 如果 `Action` 是 `create`，該參數表示所記錄策略的 ID，其含義是所記錄策略是從零開始建立的。 |`tpl-sekkg4o` |
|Status |String |表示所記錄策略的狀態。該參數有以下取值：<br><br><br>* `locked`：表示已發佈。<br><br>* `editing`：表示草稿。<br><br>* `deleted`：表示已刪除。 |`locked` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

範例請求示範了對策略 tpl\-s57n9yr 進行溯源。該策略的建立歷史如下：


1. 從頭開始建立策略 tpl\-s5o2jz6 並發佈。

2. 透過複製 tpl\-s5o2jz6 建立了策略 tpl\-sekkg4o，並發佈 tpl\-sekkg4o。

3. 透過複製 tpl\-sekkg4o 建立了策略 tpl\-s57n9yr。


```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateVersions&Version=2021-03-01
{
    "TemplateId": "tpl-s57n9yr"
}
```


<span id="範例回應"></span>
### 範例回應

範例回應展示了 tpl\-s57n9yr 的建立歷史。

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910081614E4D94A367CDBAF00B94E",
        "Action": "DescribeTemplateVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 3,
        "Versions": [
            {
                "Action": "duplicate",
                "OperateTime": 1757489199,
                "ReferredId": "tpl-sekkg4o",
                "Status": "locked"
            },
            {
                "Action": "duplicate",
                "OperateTime": 1757488579,
                "ReferredId": "tpl-s5o2jz6",
                "Status": "locked"
            },
            {
                "Action": "create",
                "OperateTime": 1747795522,
                "ReferredId": "tpl-s5o2jz6",
                "Status": "locked"
            }
        ]
    }
}
```


&nbsp;
