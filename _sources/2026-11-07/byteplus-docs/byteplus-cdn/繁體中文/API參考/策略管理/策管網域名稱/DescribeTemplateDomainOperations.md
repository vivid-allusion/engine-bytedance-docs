---
title: "DescribeTemplateDomainOperations"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomainOperations_zh-tw"
---

獲取指定網域名稱的操作歷史。操作歷史最多包含 10 條記錄。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateDomainOperations&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeTemplateDomainOperations`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示要查詢的網域名稱。 |`www.example.com` |
|PageSize |Long |否 |該 API 對獲取的記錄進行分頁。該參數表示每頁包含的記錄數量。該參數的取值範圍是 1\-50，預設值是 `10`。 |`10` |
|PageNum |Long |否 |表示展示哪個分頁上的記錄。該參數的值只能是 `1`，預設值也是 `1`。 |`1` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|Operations |Object[] |表示指定網域名稱的操作歷史，最多包含 10 條記錄。列表中的記錄按 `OperateTime` 排序，第一條記錄對應最近的操作。 | |
|Action |String |表示所記錄的操作。該參數有以下取值：<br><br><br>* `create`：表示網域名稱建立。<br><br>* `update`：表示設定更新。 |`create` |
|ConfigAfter |String |表示更新後的網域名稱設定，包括以下資訊：<br><br><br>* 綁定的分發策略 ID。<br><br>* 綁定的加密策略 ID。<br><br>* 綁定的規則引擎策略 ID。<br><br>* 是否啟用了 HTTPS 加密服務。<br><br>* 關聯的憑證 ID。<br><br>* 服務區域。<br><br>* 是否啟用了 WAF。<br><br><br>該參數是一個 JSON 字串，包含經過序列化處理的網域名稱設定資訊。 | |
|ConfigBefore |String |如果 `Action` 是 `update`，該參數表示更新前的網域名稱設定。如果 `Action` 是 `create`，該參數值為 `null`。 | |
|OperateTime |Long |表示記錄的操作時間，格式是 Unix 時間標記，精確到秒。 |`1755314680` |
|Total |Long |表示操作歷史中的記錄數量。 |`3` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateDomainOperations&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910092134B929D683A64BF500C428",
        "Action": "DescribeTemplateDomainOperations",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Operations": [
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747921048
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747921044
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747900254
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747900155
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747899947
            },
            {
                "Action": "create",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "",
                "OperateTime": 1747795591
            }
        ],
        "Total": 6
    }
}
```


&nbsp;
