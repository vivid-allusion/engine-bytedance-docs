---
title: "DescribeRemoteAuth"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeremoteauth-2023-zh-CN"
---

调用`DescribeRemoteAuth` API，查询拉流域名的远程鉴权配置。

## 要求

速率限制：每个账号每秒 10 次查询

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=DescribeRemoteAuth&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeRemoteAuth` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |需要配置远程鉴权的拉流域名所属的域名空间。您可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取要查询的域名空间。 |
|Domain |String |是 |`pull.example.com` |需要配置远程鉴权的拉流域名。您可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取要查询的域名。 |

## 响应参数

下表列出了该 API 特有的响应参数。更多详情，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Enable |Boolean |`true` |是否启用当前远程鉴权配置。取值及含义如下。<br><br><br>* `true`：启用；<br><br>* `false`：禁用。 |
|AuthURL |String |`http://remoteauth.com` |远程鉴权服务器地址，支持 HTTP/HTTPS 协议地址，并支持填写服务器 IP 地址。远程鉴权服务器默认使用端口 80/443。如果使用非默认端口，支持以`domain name:port`或`IP:port`形式设置。 |
|AuthURLPath |String |`/auth` |自定义远程鉴权请求路径。当`UseUserRequest`设置为`false`时必填。 |
|UseUserRequest |Boolean |`false` |远程鉴权请求路径使用用户请求路径或自定义请求路径。取值及含义如下。<br><br><br>* `true`：使用用户请求路径，并将用户请求路径拼接到鉴权请求地址。<br><br>* `false`：自定义远程鉴权请求路径。 |
|Method |String |`POST` |鉴权请求方法。取值及含义如下。<br><br><br>* `POST`：请求的数据作为请求体发送到服务器；<br><br>* `GET`：请求的数据包含在 URL 中。 |
|Timeout |Float |`10` |单次鉴权请求的超时时间，默认为 1，单位为秒，取值范围为 [0, 600]。 |
|DenyOnFailed |Boolean |`false` |当请求发生异常时，是否视为鉴权失败。取值及含义如下。<br><br><br>* `true`：鉴权失败；<br><br>* `false`：鉴权成功。<br><br><br>> **说明**<br><br><br>> 当请求未能到达鉴权服务器时会发生异常，例如请求超时、请求端口与鉴权服务器端口不匹配等。<br> |
|RetryTimes |Float |`3` |鉴权请求超时后的重试次数，默认为 3 次，取值范围为 [0, 10]。 |
|RetryInterval |Float |`10` |鉴权请求超时后的重试间隔，单位为秒，默认为 10，取值范围为 [1, 30]。 |
|QueryParamConfig |Object of [ParamConfig](https://docs.byteplus.com/en/docs/24/106897#paramconfig) |`-` |鉴权请求 URL 参数配置。 |
|HeaderParamConfig |Object of [ParamConfig](https://docs.byteplus.com/en/docs/24/106897#paramconfig) |`-` |鉴权请求 Header 参数配置。 |
|HeaderHost |String |`remoteauth.com` |自定义鉴权请求头中 Host 参数的值，不支持输入空格，最大长度为 1024 个字符。 |
|BodyParams |Array of [Params](https://docs.byteplus.com/en/docs/24/106897#params) |`-` |鉴权请求 Body 参数配置。<br><br>> **说明**<br><br><br>> 当鉴权请求方法为 POST 时，支持配置鉴权请求的 body 参数。<br> |
|AllowStatus |Array of Integer |`[200,201,202]` |鉴权成功时鉴权服务器返回的状态码。所有状态码应在 [200, 499] 范围内，且不得与 DenyStatus 重复。 |
|DenyRule |Object of [DenyRule](https://docs.byteplus.com/en/docs/24/106897#denyrule) |`-` |鉴权失败时鉴权服务器返回的状态码。所有状态码应在 [200, 499] 范围内，且不得与 AllowStatus 重复。 |
|DenyReturnCode |Float |`403` |鉴权失败时，MediaLive 返回给客户端的状态码应在 [400, 699] 范围内。 |
|DenyOtherStatus |Boolean |`true` |当鉴权服务器返回的状态码不在已定义的鉴权成功或鉴权失败状态码中时，将其视为鉴权成功或鉴权失败。取值及含义如下。<br><br><br>* `true`：鉴权失败；<br><br>* `false`：鉴权成功。 |
|CacheConfig |Object of [CacheConfig](https://docs.byteplus.com/en/docs/24/106897#cacheconfig) |`-` |鉴权缓存配置。当配置为空时，表示不使用缓存判断鉴权结果。 |
|EnableHLSAuth |Boolean |`true` |是否为 HLS 协议拉流请求启用鉴权开关。取值及含义如下。<br><br><br>* `true`：启用；<br><br>* `false`：禁用。 |
|EnableHLSTSAuth |Boolean |`true` |是否为 HLS 协议流的 TS 分片启用远程鉴权。取值及含义如下。<br><br><br>* `true`：启用；<br><br>* `false`：禁用。<br><br><br>> **说明**<br><br><br>> 启用 HLS 协议拉流请求的远程鉴权开关时，必须启用 TS 分片的远程鉴权。<br> |

### ParamConfig

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|UseUserParam |Boolean |`true` |远程鉴权请求的 URL 或 Header 参数是否使用用户请求参数或自定义参数。取值及含义如下。<br><br><br>* `true`：使用用户请求参数；<br><br>* `false`：自定义参数。 |
|Params |Array of [Params](https://docs.byteplus.com/en/docs/24/106897#params) |`-` |自定义参数时的参数配置。总共支持不超过 25 个常量参数和变量参数，并支持提取不超过 25 个用户请求参数。 |

### Params

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Type |String |`const_string` |参数类型。取值及含义如下。<br><br><br>* `const_string`：常量；<br><br>* `header`：用户请求的 Header 参数；<br><br>* `query`：用户请求的 URL 参数；<br><br>* `vhost`：取变量 vhost 值的参数，表示拉流请求中域名所属的域名空间；<br><br>* `domain`：取变量 domain 值的参数，表示拉流请求中使用的域名；<br><br>* `app`：取变量 app 值的参数，表示拉流请求中使用的 AppName；<br><br>* `stream`：取变量 stream 值的参数，表示拉流请求中使用的 StreamName；<br><br>* `client_ip`：取变量 client_ip 值的参数，表示拉流客户端的 IP 地址；<br><br>* `server_ip`：取变量 server_ip 值的参数，表示响应拉流请求的 CDN 节点 IP 地址；<br><br>* `request_uri`：取变量 request_uri 值的参数，表示拉流请求地址的 URI。 |
|ParamName |String |`name` |参数名称，最大长度为 100 个字符，不支持空格。<br><br>> **说明**<br><br><br><br>* > 当参数类型为常量时，表示常量参数的参数名称。<br><br><br>* > 当参数类型为用户请求的 Header 参数或 URL 参数时，表示从用户请求中提取对应参数。<br><br><br>* > 当参数类型为变量时，不生效。<br> |
|ToName |String |`Name` |新参数名称，最大长度为 100 个字符，默认为空，表示不设置新参数名称，不支持空格。<br><br>> **说明**<br><br><br><br>* > 当参数类型为常量时，不生效；<br><br><br>* > 当参数类型为用户请求的 Header 参数或 URL 参数时，表示鉴权请求中使用 ToName 值替代用户请求中的对应参数名称；<br><br><br>* > 当参数类型为变量时，表示使用 ToName 的值作为该变量的参数名称。<br> |
|Value |String |`website` |参数类型为常量时的参数值，最大长度为 100 个字符，不支持空格。 |

### DenyRule

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|DenyStatus |Array of Float |`[403,404]` |鉴权失败时鉴权服务器返回的状态码。所有状态码应在 [200, 499] 范围内，且不得与 AllowStatus 重复。 |

### CacheConfig

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|UseSameCache |Boolean |`false` |成功鉴权和失败鉴权是否使用相同配置（包括缓存 key 值和缓存过期时间）。<br><br><br>* `true`：使用相同配置；<br><br>* `false`：不使用相同配置。 |
|CacheExpireSecond |Float |`1800` |缓存过期时间，默认值`0`表示不缓存，单位为秒，取值范围为 [0, 3600]。<br><br>> **说明**<br><br><br><br>* > 当成功鉴权和失败鉴权使用相同配置时，表示鉴权缓存过期时间；<br><br><br>* > 当成功鉴权和失败鉴权不使用相同配置时，表示成功鉴权缓存的过期时间。<br> |
|CacheKeys |Object of [Keys](https://docs.byteplus.com/en/docs/24/106897#keys) |`-` |用于生成鉴权结果缓存 key 的参数配置，最多支持 50 个参数。<br><br>> **说明**<br><br><br><br>* > 当成功鉴权和失败鉴权使用相同配置时，表示鉴权结果缓存 key 的配置；<br><br><br>* > 当成功鉴权和失败鉴权不使用相同配置时，表示成功鉴权缓存的过期时间。<br> |
|DenyExpireSecond |Float |`1800` |鉴权失败缓存的过期时间，默认值为`0`时表示不缓存，单位为秒，取值范围为 [0, 3600]。<br><br>> **说明**<br><br><br>> 当成功鉴权和失败鉴权不使用相同配置时生效，即`UseSameCache`配置为`false`时。<br> |
|DenyKeys |Object of [Keys](https://docs.byteplus.com/en/docs/24/106897#keys) |`-` |用于生成鉴权失败结果缓存 key 的参数配置，最多支持 50 个参数。<br><br>> **说明**<br><br><br>> 当成功鉴权和失败鉴权不使用相同配置时生效，即`UseSameCache`配置为`false`时。<br> |

### Keys

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Type |String |`header` |用于生成缓存 key 的参数类型。取值及含义如下。<br><br><br>* `query`：用户拉流请求的 URL 参数；<br><br>* `header`：用户拉流请求的 Header 参数；<br><br>* `vhost`：使用用户拉流所在域名的 vhost 值作为参数；<br><br>* `domain`：使用用户拉流请求的 domain 值作为参数；<br><br>* `app`：使用用户拉流请求中的 AppName 值作为参数；<br><br>* `stream`：使用用户拉流请求中的 StreamName 值作为参数；<br><br>* `client_ip`：使用拉流用户客户端的 IP 地址作为参数；<br><br>* `request_uri`：使用拉流请求地址的 URI 作为参数。 |
|ParamName |String |`host` |参数名称，当参数类型为 query 或 Header 时生效且必填，表示使用指定拉流请求中与参数名称对应的参数值作为生成缓存 key 的参数。 |

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=DescribeRemoteAuth&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 示例响应

```json
{
    "ResponseMetadata": {
        "Action": "DescribeRemoteAuth",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1",
        "RequestId": "202306041104200100100232280022D31"
    },
    "Result": {
        "Enable": true,
        "AuthURL": "http://remoteauth.com",
        "AuthURLPath": "/auth",
        "UseUserRequest": true,
        "Method": "POST",
        "Timeout": 10,
        "RetryTimes": 3,
        "RetryInterval": 10,
        "DenyRule": {
            "DenyStatus": [
                400
            ]
        },
        "DenyReturnCode": 403,
        "CacheConfig": {
            "CacheExpireSecond": 1800,
            "DenyExpireSecond": 1800,
            "CacheKeys": {
                "Type": "header",
                "ParamName": "host"
            },
            "DenyKeys": {
                "Type": "query",
                "ParamName": "lr"
            },
            "UseSameCache": true
        },
        "EnableHLSAuth": true,
        "EnableHLSTSAuth": true,
        "HeaderHost": "remoteauth.com",
        "QueryParamConfig": {
            "UseUserParam": true,
            "Params": [
                {
                    "Type": "query",
                    "ParamName": "lr",
                    "ToName": "LR",
                    "Value": "lang_en"
                }
            ]
        },
        "HeaderParamConfig": {
            "UseUserParam": true,
            "Params": [
                {
                    "Type": "header",
                    "ParamName": "Accept",
                    "ToName": "Accept",
                    "Value": "text/html"
                }
            ]
        },
        "BodyParams": [
            {
                "Type": "const_string",
                "ParamName": "name",
                "ToName": "Name",
                "Value": "website"
            }
        ],
        "AllowStatus": [
            200,
            202
        ],
        "DenyOnFailed": true,
        "DenyOtherStatus": false
    }
}
```

## 错误码

以下是与当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/106897#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数验证失败。请检查数据类型是否正确。 |
|400 |InvalidParam.Format |%s format error |参数格式不正确。请检查错误消息中指定参数是否存在非法字符或 URL 格式错误。 |
|400 |InvalidParam.DomainAndApp |domain and app exist can not exist at the same time |不能同时传入 Domain 和 App。请修改输入参数。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生数据库相关内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
