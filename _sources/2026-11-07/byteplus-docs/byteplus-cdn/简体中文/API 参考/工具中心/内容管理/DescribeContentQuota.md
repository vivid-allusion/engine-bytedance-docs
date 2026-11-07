---
title: "DescribeContentQuota"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/describecontentquota"
---

获取您 BytePlus 账号下每日的刷新和预热任务的配额及配额余量。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeContentQuota&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeContentQuota`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|PreloadLimit |Long |表示每次可预热的最大 URL 数量。 |`100` |
|PreloadQuota |Long |表示每日可预热的 URL 数量。 |`1000` |
|PreloadRemain |Long |表示今天可预热的 URL 剩余数量。 |`10` |
|RefreshDirLimit |Long |表示每次可刷新的最大目录数量。 |`100` |
|RefreshDirQuota |Long |表示每日可刷新的目录数量。 |`50` |
|RefreshDirRemain |Long |表示今天可刷新的目录剩余数量。 |`15` |
|RefreshQuota |Long |表示每日可刷新的 URL 数量。 |`10000` |
|RefreshQuotaLimit |Long |表示每次可刷新的最大 URL 数量。 |`100` |
|RefreshRemain |Long |表示今天可刷新的 URL 剩余数量。 |`200` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeContentQuota&Version=2021-03-01
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202310271225559FCEDC662FFE48246DCB",
        "Action": "DescribeContentQuota",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PreloadLimit": 100,
        "PreloadQuota": 1000,
        "PreloadRemain": 1000,
        "RefreshDirLimit": 100,
        "RefreshDirQuota": 50,
        "RefreshDirRemain": 50,
        "RefreshQuota": 10000,
        "RefreshQuotaLimit": 100,
        "RefreshRemain": 1000
    }
}
```


&nbsp;
