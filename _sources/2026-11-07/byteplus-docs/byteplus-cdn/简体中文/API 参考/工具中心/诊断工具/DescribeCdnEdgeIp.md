---
title: "DescribeCdnEdgeIp"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnEdgeIp-cn"
---

获取 BytePlus CDN 分配给域名的所有边缘节点的 IP 地址。这些边缘节点属于域名的加速区域。您可以指定多个过滤条件对这些 IP 地址进行过滤。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您需要使用该 API，请 <a href="https://console.byteplus.com/workorder/create">提交工单</a>。</div>


<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以发送 20 个请求。

数据延时：如果分配给域名的边缘节点发生了变化，可能需要 10\-15 分钟才会体现在该 API 返回的 IP 列表中。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeCdnEdgeIp&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeCdnEdgeIp`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示一个域名，用于获取分配给该域名的边缘节点的 IP 地址。<br><br>说明<br><br>如果域名的 `status` 是 `offline`，该 API 返回的 IP 地址列表是 `null`。您可以调用 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplatedomains-7f84f-cn) 获取域名的状态。 |`www.example.com` |
|IpVersion |String |否 |表示 IP 地址的版本，以获取该版本的 IP 地址。该参数的取值如下：<br><br><br>* `ipv4`：表示 IPv4 地址。<br><br>* `ipv6`：表示 IPv6 地址。<br><br><br>如果不指定该参数，表示不使用该参数对该 API 返回的结果进行过滤。<br><br>当 `RsIp` 为 `true` 时，该 API 仅返回 IPv4 地址。 |`ipv4` |
|Isp |String |否 |表示一个本地网络运营商的代码，以获取属于该网络运营商的 IP 地址。您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 获取所有本地网络运营商的代码。<br><br>如果不指定该参数，表示不使用该参数对该 API 返回的结果进行过滤。<br><br>如果 `RsIp` 是 `true`，`Isp` 无效。 |`CTCC` |
|Region |String |否 |表示一个国家或地区的代码，以获取属于该国家或地区的 IP 地址。您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 获取所有国家和地区的代码。<br><br>如果不指定该参数，表示不使用该参数对该 API 返回的结果进行过滤。<br><br>如果 `RsIp` 是 `true`，`Region` 无效。 |`BJ` |
|Status |String |否 |表示一个节点状态，以获取该状态下的边缘节点的 IP 地址。该参数有以下取值：<br><br><br>* `online`：表示状态是在线。<br><br><br>如果不指定该参数，表示不使用该参数对该 API 返回的结果进行过滤。 |`online` |
|RsIp |Boolean |否 |表示是否返回节点的物理 IP 地址。该参数有以下取值：<br><br><br>* `true`：表示返回节点的物理 IP 地址列表。这些地址用于接收用户请求。<br><br>* `false`：表示返回节点的虚拟 IP 地址列表。这些地址用于向回源节点发送请求。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|CdnIpv4 |String[] |表示一个 IPv4 地址的列表。<br><br>说明<br><br>如果 `IpVersion` 是 `ipv6`，该参数值为 `null`。 |`["xxx.xx.xxx.32","xxx.xx.xx.90"]` |
|CdnIpv6 |String[] |表示一个 IPv6 地址的列表。<br><br>说明<br><br>如果 `IpVersion` 是 `ipv4` 或者 `RsIp` 是 `true`，该参数值为 `null`。 |`["xxxx:xx:xxxx:4::13","xxxx:xx:xxxx:4::14"]` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnEdgeIp&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "202211301702110102100671410480265A",
        "Action": "DescribeCdnEdgeIp",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CdnIpv4": [
            "xxx.xxx.xxx.23",
            "xxx.xxx.xxx.80",
            ...
        ],
        "CdnIpv6": [
            "xxxx:xxxx:xxxx:xxxx:xxxx:0:b00:92",
            "xxxx:xxxx:xxxx:xxxx:xxxx:0:b00:93",
            ...
        ]
    }
}
```
