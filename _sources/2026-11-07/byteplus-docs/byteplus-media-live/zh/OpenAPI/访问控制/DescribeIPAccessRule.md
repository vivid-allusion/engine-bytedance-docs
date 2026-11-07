---
title: "DescribeIPAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeipaccessrule-zh-CN"
---

查询指定域名空间的 IP blocklist 或 allowlist。

<span id="07d60fcc"></span>
## 请求

<span id="3eb268f1"></span>
### 详情


* API 操作：`DescribeIPAccessRule`

* 请求方式：**POST**

* 请求 URL：https://open.byteplusapi.com/?Action=DescribeIPAccessRule&Version=2023\-01\-01

* 配额：每个账号每秒 10 次查询


<span id="0c94222a"></span>
### **查询字符串参数**

下表未包含所有公共参数。完整列表请参见[公共参数](https://docs.byteplus.com/byteplus-media-live/docs/calling-byteplus-medialive-openapi#Common%20request%20parameters)。


|**参数** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |此 API 操作的版本。当前版本：`2023-01-01`。 |


<span id="be600f30"></span>
### 请求体参数


|**参数** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Vhost |是 |字符串 |[域名空间](https://docs.byteplus.com/en/byteplus-media-live/docs/glossary#Vhost)。 |
|Domain |是 |字符串 |域名。 |


<span id="4e7cf17f"></span>
### 请求示例

```JSON
POST https://open.byteplusapi.com?Action=DescribeIPAccessRule&Version=2023-01-01
{
    "Vhost": "example",
    "Domain": "example.com"
}
```


<span id="3238ad86"></span>
## 返回调用结果

<span id="b1276522"></span>
### 响应架构


|**参数** |**数据类型** |**接口行为** |
|---|---|---|
|AccessRuleLists |数组<[AccessRuleLists](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeipaccessrule#f67e0c26)\> |IP 限制规则列表。 |


<span id="f67e0c26"></span>
#### AccessRuleLists


|**参数** |**数据类型** |**接口行为** |
|---|---|---|
|Vhost |字符串 |域名空间。 |
|Domain |字符串 |域名。 |
|IPAccessRule |[IPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeipaccessrule#fcd9863b) |IP 限制规则。 |


<span id="fcd9863b"></span>
#### IPAccessRule


|**参数** |**数据类型** |**接口行为** |
|---|---|---|
|Type |字符串 |访问规则类型。有效选项包括：<br><br><br>* `allow`：allowlist。仅允许 allowlist 中的 IP 地址访问资源。<br><br>* `deny`：blocklist。blocklist 中的 IP 地址无法访问资源。 |
|Enable |布尔值 |配置是否已开启。<br><br><br>* `true`：配置已开启。<br><br>* `false`：配置未开启。 |
|IPList |数组 |allowlist 或 blocklist 中的 IP 地址列表。 |


<span id="92ffb89a"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeIPAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "IPAccessRuleLists": [
            {
                "Vhost": "example",
                "Domain": "example.com"
                "IPAccessRule": {
                    "Type": "deny",
                    "Enable": true,
                    "IpList": [
                    "192.168.1.1", 
                    "192.168.1.2"
                    ]
                }
            }
        ]
    }
}
```
