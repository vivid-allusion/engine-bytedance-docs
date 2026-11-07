---
title: "DescribeTemplateDomainOperations"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomainOperations_zh-cn"
---

获取指定域名的操作历史。操作历史最多包含 10 条记录。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateDomainOperations&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeTemplateDomainOperations`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示要查询的域名。 |`www.example.com` |
|PageSize |Long |否 |该 API 对获取的记录进行分页。该参数表示每页包含的记录数量。该参数的取值范围是 1\-50，默认值是 `10`。 |`10` |
|PageNum |Long |否 |表示展示哪个分页上的记录。该参数的值只能是 `1`，默认值也是 `1`。 |`1` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Operations |Object[] |表示指定域名的操作历史，最多包含 10 条记录。列表中的记录按 `OperateTime` 排序，第一条记录对应最近的操作。 | |
|Action |String |表示所记录的操作。该参数有以下取值：<br><br><br>* `create`：表示域名创建。<br><br>* `update`：表示配置更新。 |`create` |
|ConfigAfter |String |表示更新后的域名配置，包括以下信息：<br><br><br>* 绑定的分发策略 ID。<br><br>* 绑定的加密策略 ID。<br><br>* 绑定的规则引擎策略 ID。<br><br>* 是否启用了 HTTPS 加密服务。<br><br>* 关联的证书 ID。<br><br>* 服务区域。<br><br>* 是否启用了 WAF。<br><br><br>该参数是一个 JSON 字符串，包含经过序列化处理的域名配置信息。 | |
|ConfigBefore |String |如果 `Action` 是 `update`，该参数表示更新前的域名配置。如果 `Action` 是 `create`，该参数值为 `null`。 | |
|OperateTime |Long |表示记录的操作时间，格式是 Unix 时间戳，精确到秒。 |`1755314680` |
|Total |Long |表示操作历史中的记录数量。 |`3` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateDomainOperations&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="返回示例"></span>
### 返回示例

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
