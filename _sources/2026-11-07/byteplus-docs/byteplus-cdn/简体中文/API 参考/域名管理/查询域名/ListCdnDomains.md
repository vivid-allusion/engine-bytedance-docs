---
title: "ListCdnDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnDomains_zh-cn"
---

获取 BytePlus CDN 中的域名列表以及每个域名的基础信息，包括业务类型、运行状态、CNAME 地址、服务区域等。您可以指定过滤条件对域名列表进行过滤。若需要获取详细的域名配置，请调用 [DescribeCdnConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_zh-cn)。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=ListCdnDomains&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `ListCdnDomains`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |否 |表示要查询的域名，支持模糊匹配。 |`example` |
|ServiceType |String |否 |表示一个业务类型，用来对域名进行过滤，获取该业务类型的域名。该参数有以下取值：<br><br><br>* `download`：表示文件下载。<br><br>* `web`：表示网页。<br><br>* `video`：表示音视频点播。 |`web` |
|ResourceTags |String[] |否 |表示一个标签列表，用于对域名进行过滤，获取带有列表中任意标签的域名。列表中最多可以包含 10 个标签，每个标签的格式是 `key:value`。参见右边该参数的示例。 |`["key1:val1","key2:val2"]` |
|Status |String |否 |表示一个域名状态，用来对域名进行过滤，获取该状态下的域名。该参数有以下取值：<br><br><br>* `online`：表示状态是 "在线"。<br><br>* `configuring`：表示状态是 "配置中"。<br><br>* `offline`：表示状态是 "离线"。 |`offline` |
|Project |String |否 |表示一个项目，获取归属该项目的域名。 |`default` |
|OriginProtocol |String |否 |表示一个协议，获取回源请求使用该协议的域名。该参数有以下取值：<br><br><br>* `http`：表示 HTTP 协议。<br><br>* `https`：表示 HTTPS 协议。<br><br>* `followclient`：表示用户请求使用的协议。 |`http` |
|IPv6 |Boolean |否 |表示根据是否启用了 IPv6 特性来过滤域名。该参数有以下取值：<br><br><br>* `true`: 表示 IPv6 已启用。<br><br>* `false`: 表示 IPv6 未启用。 |`true` |
|HTTPS |Boolean |否 |表示根据是否启用了 HTTPS 加密服务来过滤域名。该参数有以下取值：<br><br><br>* `true`: 表示 HTTPS 加密服务已启用。<br><br>* `false`: 表示 HTTPS 加密服务未启用。 |`true` |
|PrimaryOrigin |String |否 |表示一个主源站，以获取主源站配置中包含该主源站的那些域名。该参数值可以是一个 IP 地址，也可以是一个域名。 |`helloworld.example.com` |
|PageNum |Long |否 |表示一个页码，用以获取该页面上域名列表。该参数的默认值为 `1`。<br><br>CDN 对符合过滤条件的域名进行分页。您可以根据响应参数 `Total` 和请求参数 `PageSize` 计算该 API 返回的页数。 |`1` |
|PageSize |Long |否 |表示每页包含的域名数量。该参数的取值范围是 1\-100，默认值是 `10`。 |`10` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|PageNum |Long |表示请求参数中的 `PageNum`。 |`1` |
|PageSize |Long |表示请求参数中的 `PageSize`。 |`10` |
|Total |Long |表示符合过滤条件的域名数量。该参数值不受请求参数 `PageSize` 和 `PageNum` 的影响。 |`100` |
|Data |Object[] |表示符合过滤条件的域名列表。 | |
|Domain |String |表示列表中的一个域名。 |`www.example.com` |
|ServiceType |String |表示该域名的业务类型。该参数有以下取值：<br><br><br>* `download`：表示文件下载。<br><br>* `web`：表示网页。<br><br>* `video`：表示音视频点播。 |`web` |
|Status |String |表示该域名的状态。该参数有以下取值：<br><br><br>* `online`：表示状态是 "在线"。<br><br>* `configuring`：表示状态是 "配置中"。<br><br>* `offline`：表示状态是 "离线"。 |`online` |
|Cname |String |表示 CDN 分配给该域名的 CNAME。 |`www.example.com.bplslb.com` |
|ServiceRegion |String |表示该域名的服务区域。该参数有以下取值：<br><br><br>* `chinese_mainland`：表示中国内地。<br><br>* `global`：表示全球。<br><br>* `outside_chinese_mainland`：表示全球（不含中国内地）。 |`outside_chinese_mainland` |
|CreateTime |Long |表示该域名添加到 CDN 中的时间，格式为 Unix 时间戳。 |`1625587200` |
|UpdateTime |Long |表示该域名最近一次更新的时间，格式是 Unix 时间戳。更新操作包括启用域名、停用域名、修改域名配置等。 |`1601371409` |
|Project |String |表示该域名所归属的项目。 |`default` |
|OriginProtocol |String |表示回源请求使用的协议。该参数有以下取值：<br><br><br>* `http`：表示 HTTP 协议。<br><br>* `https`：表示 HTTPS 协议。<br><br>* `followclient`：表示用户请求使用的协议。 |`http` |
|IPv6 |Boolean |表示该域名是否启用了 IPv6 特性。该参数有以下取值：<br><br><br>* `true`: 表示 IPv6 已启用。<br><br>* `false`: 表示 IPv6 未启用。 |`true` |
|HTTPS |Boolean |表示该域名是否启用了 HTTPS 加密服务。该参数有以下取值：<br><br><br>* `true`: 表示 HTTPS 加密服务已启用。<br><br>* `false`: 表示 HTTPS 加密服务未启用。 |`true` |
|PrimaryOrigin |String[] |表示该域名配置的主源站列表。 |`"xxx.xx.xxx.xx","helloworld1.example.com"` |
|BackupOrigin |String[] |表示该域名配置的备源站列表。如果该域名没有配置任何备源站，该参数值是 `null`。 |`"xxx.xx.xxx.xx","helloworld2.example.com"` |
|ResourceTags |Object[] |表示该域名带的标签列表。如果该域名没有带任何标签，该参数值是 `null`。 | |
|Key |String |表示标签列表中一个标签的 key。 |`userKey` |
|Value |String |表示该标签的 value。 |`userValue` |
|CacheShared |String |表示该域名在共享缓存配置中的角色。该参数有以下取值：<br><br><br>* `target_host`：表示存在一个共享缓存配置，在该配置中该域名的角色是目标域名。<br><br>* `cache_shared_on`：表示存在一个共享缓存配置，在该配置中该域名的角色是被配置的域名。<br><br>* `""`：该参数值为空，表示该域名不存在于任何共享缓存配置中。 |`cache_shared_on` |
|CacheSharedTargetHost |String |如果`CacheShared` 是 `cache_shared_on`，表示与该域名共享缓存的目标域名。如果`CacheShared` 是 `target_host` 或者是空值（""），该参数值是空（""）。 |`www.example.net` |
|Waf |Boolean |表示该域名是否启用了 WAF 防护。该参数有以下取值：<br><br><br>* `true`：表示已启用了 WAF 防护。<br><br>* `false`：表示未启用 WAF 防护。 |`false` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=ListCdnDomains&Version=2021-03-01
{
    "Domain": "example",
    "ResourceTags": [
        "key1:val1",
        "key2:val2"
    ]
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20250821112545F5890E6D640605A33280",
        "Action": "ListCdnDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "BackupOrigin": [
                    "203.0.113.9",
                    "img2.example.com"
                ],
                "CacheShared": "",
                "CacheSharedTargetHost": "",
                "Cname": "www.example.com.bplslb.com",
                "CreateTime": 1755585663,
                "Domain": "www.example.com",
                "HTTPS": true,
                "IPv6": true,
                "OriginProtocol": "https",
                "PrimaryOrigin": [
                    "203.0.113.8",
                    "img.example.com",
                    "bpcntest.tos-ap-southeast-3.bytepluses.com",
                    "mybucket.oss-ap-southeast-1.aliyuncs.com",
                    "mybucket.cos.ap-singapore.myqcloud.com",
                    "my-bucket.s3.ap-southeast-1.amazonaws.com",
                    "myazstorage.blob.core.windows.net"
                ],
                "Project": "default",
                "ResourceTags": [
                    {
                        "Key": "mykey",
                        "Value": "myvalue"
                    }
                ],
                "ServiceRegion": "outside_chinese_mainland",
                "ServiceType": "web",
                "Status": "online",
                "UpdateTime": 1755585663,
                "Waf": false
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
