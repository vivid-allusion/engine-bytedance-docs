---
title: "DescribeTemplateOperations"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateOperations_zh-cn"
---

获取指定策略的操作历史。操作历史最多包含 10 条记录。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateOperations&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeTemplateOperations`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示要查询的策略 ID。 |`tpl-s5wzdn0` |
|PageSize |Long |否 |该 API 对获取的记录进行分页。该参数表示每页包含的记录数量。该参数的取值范围是 1\-50，默认值是 `10`。 |`10` |
|PageNum |Long |否 |表示展示哪个分页上的记录。该参数的值只能是 `1`，默认值也是 `1`。 |`1` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Operations |Object[] |表示指定策略的操作历史，最多包含 10 条记录。列表中的记录按 `OperateTime` 排序，第一条记录对应最近的操作。 | |
|Action |String |表示所记录的操作。该参数有以下取值：<br><br><br>* `bind`：表示域名绑定。<br><br>* `create`：表示策略创建。<br><br>* `release`：表示策略发布。 |`bind` |
|DomainsAfter |Object[] |如果 `Action` 是 `bind`，该参数表示绑定的域名信息。如果 `Action` 不是 `bind`，该参数值为 `null`。 | |
|Domain |String |表示绑定的域名。 |`abc.example.com` |
|DomainsBefore |Object[] |如果 `Action` 是 `bind`，该参数表示绑定操作前，该策略所绑定的域名信息。<br><br>在以下任意情况下，该参数值为 `null`：<br><br><br>* `Action` 不是 `bind`。<br><br>* 所记录的操作是首次绑定域名。 | |
|Domain |String |表示绑定操作前，该策略所绑定的域名。 |`www.example.com` |
|OperateTime |Long |表示记录的操作时间，格式是 Unix 时间戳，精确到秒。 |`1755314680` |
|Total |Long |表示操作历史中的记录数量。 |`3` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateOperations&Version=2021-03-01
{
    "TemplateId": "tpl-s5wzdn0"
}
```


<span id="返回示例"></span>
### 返回示例

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
