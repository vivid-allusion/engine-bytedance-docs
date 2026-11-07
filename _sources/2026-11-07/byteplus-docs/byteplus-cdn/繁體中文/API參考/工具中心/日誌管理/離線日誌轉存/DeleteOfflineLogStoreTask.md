---
title: "DeleteOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteOfflineLogStoreTask_zh-tw"
---

刪除一個已停用的離線日誌轉存任務。

<span id="使用限制"></span>
## 使用限制

節流限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DeleteOfflineLogStoreTask&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DeleteOfflineLogStoreTask`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TaskID |String |是 |表示待刪除的一個任務 ID。該任務的 `Status` 必須是 `disable`。 |`dPFEQ8vwbRShTdW5kNbZe3` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DeleteOfflineLogStoreTask&Version=2021-03-01
{
    "TaskID": "dPFEQ8vwbRShTdW5kNbZe3"
}
```


&nbsp;
