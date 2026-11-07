---
title: "DescribeCdnRegionAndIsp"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp"
---

获取 BytePlus IP 地址数据库所覆盖的中国省级行政区、全球的国家和地区、以及中国大陆网络运营商的名称和代码。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeCdnRegionAndIsp&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeCdnRegionAndIsp`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Area |String |否 |表示查询的范围。该参数有以下取值：<br><br><br>* `China`：表示中国省级行政区和中国内地网络运营商的代码和名称。<br><br>* `Global`：表示全球国家和地区、以及中国内地网络运营商的代码和名称。<br><br><br>该参数的默认值是 `China`。 |`Global` |
|Lang |String |否 |表示查询结果显示的语言。该参数有以下取值：<br><br><br>* `zh`：表示简体中文。<br><br>* `en`：表示英文。<br><br><br>该参数的默认值是 `en`。 |`en` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Isps |Object[] |表示中国内地的网络运营商。 | |
|Code |String |表示一个网络运营商的代码。 |`CU` |
|Name |String |表示该网络运营商的名称。 |`China Unicom` |
|Regions |Object[] |表示一个区域列表。<br><br><br>* 如果 `Area` 是 `Global`，该参数表示一个全球各国家和地区的列表。<br><br>* 如果 `Area` 是 `China`，该参数表示一个中国各省级行政区的列表。 | |
|Code |String |表示一个国家、地区、或中国省级行政区的代码。 |`BJ` |
|Name |String |表示该国家、地区、或中国省级行政区的名称。 |`Beijing` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnRegionAndIsp&Version=2021-03-01
{
    "Area": "Global"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423061106DA1BD20A355B07CBEC2D",
        "Action": "DescribeCdnRegionAndIsp",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Isps": [
            {
                "Code": "CT",
                "Name": "China Telecom"
            },
            {
                "Code": "CM",
                "Name": "China Mobile"
            },
            {
                "Code": "CU",
                "Name": "China Unicom"
            },
            {
                "Code": "GWBN",
                "Name": "Great Wall Broadband"
            },
            ...
        ],
        "Regions": [
            {
                "Code": "CHE",
                "Name": "Switzerland"
            },
            {
                "Code": "AZE",
                "Name": "Azerbaijan"
            },
            {
                "Code": "PNG",
                "Name": "Papua New Guinea"
            },
            {
                "Code": "PSE",
                "Name": "Palestine"
            },
            {
                "Code": "FSM",
                "Name": "Micronesia"
            },
            ...
        ]
    }
}
```


&nbsp;
