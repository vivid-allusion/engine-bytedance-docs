---
title: "DescribeCdnIP"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_Cn"
---

查询指定的一个或者多个 IP 地址是否是 BytePlus CDN 节点的 IP 地址。CDN 节点涵盖边缘节点和回源节点。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeCdnIP&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeCdnIP`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|IPs |String[] |是 |表示待查询的 IP 地址列表。列表中最多可以包含 50 个 IP 地址。 |`["xx.xxx.xxx.102", "xxx.xxx.234.67"]` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|IPs |Object[] |表示请求参数中的 IP 地址列表。 | |
|IP |String |表示 IP 地址列表中的一个 IP 地址。 |`xx.xxx.xxx.102` |
|CdnIp |Boolean |表示该 IP 地址是否是某个 CDN 边缘节点的 IP 地址。该参数有以下取值：<br><br>true：表示该 IP 地址是某个 CDN 边缘节点的 IP 地址。<br><br>false：表示该 IP 地址不是任何 CDN 边缘节点的 IP 地址。 |`false` |
|ISP |String |表示该 IP 地址归属的网络运营商（ISP）。<br><br><br>* 如果 `CdnIp` 是 `false`，该参数值为空（""）。<br><br>* 如果 `CdnIp` 是 `true` 但是 CDN 未获取该 IP 地址归属的网络运营商，该参数值是 `DEFAULT`。 |`电信` |
|Location |String |表示该 IP 地址归属的国家或地区。如果 `CdnIp` 是 `false`，该参数值为空（""）。<br><br>对于归属地属于中国内地的 IP 地址：<br><br><br>* 如果归属地所属城市是一个直辖市，`Location` 精确到区。<br><br>* 如果归属地所属城市不是直辖市，`Location` 精确到城市。 |`中国-山东-青岛市` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnIP&Version=2021-03-01
{
    "IPs": [
        "xxx.xxx.xx.139",
        "xxx.xx.xx.34"
    ]
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024101011033668CF51ECED9C5477E3C6",
        "Action": "DescribeCdnIP",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "IPs": [
            {
                "CdnIp": true,
                "IP": "xxx.xxx.xx.139",
                "ISP": "DEFAULT",
                "Location": "Singapore-Singapore-Singapore"
            },
            {
                "CdnIp": false,
                "IP": "xxx.xx.xx.34",
                "ISP": "",
                "Location": ""
            }
        ]
    }
}
```


&nbsp;
