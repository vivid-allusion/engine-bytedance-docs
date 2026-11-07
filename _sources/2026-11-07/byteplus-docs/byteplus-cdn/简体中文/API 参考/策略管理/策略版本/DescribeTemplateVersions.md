---
title: "DescribeTemplateVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateVersions_zh-cn"
---

对指定策略进行溯源，获取创建历史记录。当前，该 API 最多展示 10 条记录。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeTemplateVersions&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeTemplateVersions`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示要进行溯源的策略 ID。 |`tpl-s5o2jz6` |
|PageSize |Long |否 |该 API 对获取的记录进行分页。该参数表示每页包含的记录数量。该参数的取值范围是 1\-50，默认值是 `10`。 |`10` |
|PageNum |Long |否 |表示展示哪个分页上的记录。该参数的值只能是 `1`，默认值也是 `1`。 |`1` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Total |Long |表示该 API 获取的记录总数。 |`3` |
|Versions |Object[] |表示指定策略的创建历史，最多包含 10 条记录。列表中的记录按 `OperateTime` 排序，第一条记录对应最近的操作。 | |
|Action |String |对于 `ReferredId` 所表示的策略，该参数表示对该策略的操作，有以下取值：<br><br><br>* `create`：表示创建。<br><br>* `duplicate`：表示复制。 |`create` |
|OperateTime |Long |表示 `Action` 发生的时间，格式是 Unix 时间戳，精确到秒。 |`1757489199` |
|ReferredId |String |表示所记录策略的来源。<br><br><br>* 如果 `Action` 是 `duplicate`，该参数表示所记录策略是从哪个策略复制而来的。<br><br>* 如果 `Action` 是 `create`，该参数表示所记录策略的 ID，其含义是所记录策略是从零开始创建的。 |`tpl-sekkg4o` |
|Status |String |表示所记录策略的状态。该参数有以下取值：<br><br><br>* `locked`：表示已发布。<br><br>* `editing`：表示草稿。<br><br>* `deleted`：表示已删除。 |`locked` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

请求示例演示了对策略 tpl\-s57n9yr 进行溯源。该策略的创建历史如下：


1. 从零开始创建策略 tpl\-s5o2jz6 并发布。

2. 通过复制 tpl\-s5o2jz6 创建了策略 tpl\-sekkg4o，并发布 tpl\-sekkg4o。

3. 通过复制 tpl\-sekkg4o 创建了策略 tpl\-s57n9yr。


```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateVersions&Version=2021-03-01
{
    "TemplateId": "tpl-s57n9yr"
}
```


<span id="返回示例"></span>
### 返回示例

返回示例展示了 tpl\-s57n9yr 的创建历史。

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
