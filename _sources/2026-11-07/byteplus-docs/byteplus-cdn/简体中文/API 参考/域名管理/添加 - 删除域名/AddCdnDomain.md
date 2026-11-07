---
title: "AddCdnDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/AddCdnDomain_zh-cn"
---

在 CDN 中添加一个或者多个具有相同配置的域名，并指定这些配置。

当您使用该 API 添加域名时，CDN 会为每个域名创建一个分发策略，以存储相应的域名配置。如果您在添加域名时指定了 HTTPS 相关配置，CDN 还会为每个域名创建一个加密策略。创建的策略会自动与相应的域名绑定。这些策略都具有相同的策略名称 `system-tpl`，表示它们是系统创建的策略。但是，每个策略的 ID 是不同的。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=AddCdnDomain&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `AddCdnDomain`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body

<span id="基础配置"></span>
## 基础配置

<span id="域名"></span>
### 域名


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示要修改配置的域名。 |`www.example.com` |


<span id="服务区域"></span>
### 服务区域


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ServiceRegion |String |否 |表示域名的服务区域。该参数有以下取值：<br><br><br>* `chinese_mainland`：表示中国内地。<br><br>* `global`：表示全球。<br><br>* `outside_chinese_mainland`：表示全球（不含中国内地）。<br><br><br>该参数的默认值是 `outside_chinese_mainland`。要指定另两个值，请 [提交工单](https://console.byteplus.com/workorder/create)。 |`outside_chinese_mainland` |


<span id="项目"></span>
### 项目


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Project |String |否 |表示域名所归属的项目。您可以在 [项目管理](https://console.byteplus.com/iam/resourcemanage/project) 页面查看已存在的项目以及项目下的资源。<br><br>该参数的默认值是 `default`，表示名称是 `default` 的项目。 |`default` |


<span id="标签"></span>
### 标签


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ResourceTags |Object[] |否 |表示您对该域名设置的标签。您最多可以设置 10 个标签。 | |
|Key |String |否 |表示一个标签的 Key，可以包含字母和数字，长度不超过 128 个字符。 |`userKey` |
|Value |String |否 |表示该标签的 Value，可以包含字母和数字，长度不超过 128 个字符。 |`userValue` |


<span id="ipv6-加速"></span>
### IPv6 加速


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|IPv6 |Object |否 |表示 IPv6 配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |


<span id="源站清单"></span>
### 源站清单


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Origin |Object[] |否 |表示源站配置。 | |
|OriginAction |Object |是 |表示源站配置，应用于所有用户请求。 | |
|OriginLines |Object[] |是 |表示一个源站列表。列表中最多可以包含 50 个源站。 | |
|OriginType |String |是 |表示该源站的类别。该参数有以下取值：<br><br><br>* `primary`：表示主源站。<br><br>* `backup`：表示备源站。<br><br><br>源站列表中至少需要包含一个主源站。备源站是可选的。 |`primary` |
|InstanceType |String |是 |表示源站的类型。该参数有以下取值：<br><br><br>* `ip`：表示 IP 地址。<br><br>* `domain`：表示域名。<br><br>* `tos`：表示对象存储桶。<br><br><br>注意<br><br>在 CDN 向对象存储源站发送回源请求时，回源请求使用的方法与用户请求相同。默认情况下，用户请求可以使用的请求方法有 DELETE、GET、HEAD、POST、PUT、PATCH、OPTIONS、CONNECT。如果您不希望回源请求使用某些请求方法，例如您不希望回源请求使用 DELETE 方法，可能导致误删源站上的文件，建议您采取以下步骤：<br><br><br>1. 在存储桶所在的对象存储服务中设置权限，组织不符合预期的操作。<br><br>2. 在 CDN 的 `MethodDeniedRule` 特性中，指定 CDN 不支持的请求方法。 |`ip` |
|Address |String |是 |表示列表中一个源站的地址。该参数有以下说明：<br><br><br>* 如果 `InstanceType` 是 `ip`，您指定的是源站的 IP 地址。IP 地址可以是 IPv4 或 IPv6 地址。<br><br>* 如果 `InstanceType` 是 `domain`，您指定的是源站的域名。该域名不能是泛域名，也不能与该策略要绑定的域名相同。<br><br>* 如果 `InstanceType` 是 `tos`，您指定的是存储桶域名，可以是云厂商分配的桶域名，也可以是您在云厂商处为存储桶设置的自定义域名。桶域名不能包含 `https://`，长度不能超过 100 个字符。存储桶可以来自 BytePlus TOS、阿里云 OSS、腾讯云 COS、AWS S3 或者任何使用鉴权方式与 S3 兼容的第三方对象存储服务。<br><br><br>说明<br><br><br>* 如果存储桶来自您账号下的 TOS 服务，在调用该 API 前，您需要在 CDN 控制台中打开该域名的配置页面。在该页面中，点击 **授权** CDN 访问您账号下的 TOS 服务。<br><br>* 在 Azure Blob Storage 中，对象存储桶称为 container。 |`www.example.com` |
|HttpPort |String |否 |表示 CDN 使用 HTTP 协议访问该源站时所访问的端口，取值范围是 1\-65535，默认值是 `80`。如果源站服务器没有开放该端口，您无需指定该参数。<br><br>该参数仅当 `InstanceType` 为 `ip` 或 `domain` 时才有效。 |`80` |
|HttpsPort |String |否 |表示 CDN 使用 HTTPS 协议访问该源站时所访问的端口，取值范围是 1\-65535，默认值是 `443`。如果源站服务器没有开放该端口，您无需指定该参数。<br><br>该参数仅当 `InstanceType` 为 `ip` 或 `domain` 时才有效。 |`443` |
|Weight |String |否 |表示该源站的权重，取值范围是 1\-100，默认值是 `1`。权重越大，该源站在 CDN 发送回源请求时被选择到的概率也越大。<br><br>该参数仅当 `InstanceType` 为 `ip` 或 `domain` 时才有效。 |`100` |
|PrivateBucketAccess |Boolean |否 |表示存储桶是否是私有桶。该参数仅当 `InstanceType` 为 `tos` 时有效。该参数有以下取值：<br><br><br>* `true`：表示该存储桶是私有桶。<br><br>* `false`：表示该存储桶不是私有桶。<br><br><br>该参数的默认值是 `false`。 |`false` |
|OriginHost |String |否 |表示回源请求访问的站点域名，适用于源站服务器上有多个站点的情况。<br><br><br>* 该参数的默认值与全局 `OriginHost` 相同，但优先级高于全局 `OriginHost` 参数。<br><br>* 该参数值的长度不能超过 1,024 个字符。<br><br>* 如果您在调用该 API 时，即没有修改 `Address`，也没有指定 `OriginHost`，`OriginHost` 不会被默认值覆盖，而是保持当前值。 |`img.example.com` |
|PrivateBucketAuth |Object |否 |表示访问存储桶的鉴权配置。<br><br>说明<br><br>如果存储桶是本账号下的 TOS 存储桶并且您希望使用跨服务授权方式访问 TOS 存储桶，该参数无需指定。跨服务授权访问方式无需指定 AccessKey。 | |
|Switch |Boolean |是 |表示访问存储桶是否需要凭证。如果您指定了 `PrivateBucketAuth` 结构体，该参数值必须是 `true`。 |`false` |
|AuthType |String |否 |表示存储桶使用的是哪个对象存储服务所提供的鉴权方式。该参数有以下取值：<br><br><br>* `tos`：表示 BytePlus TOS，您使用 AccessKey 访问 TOS 存储桶。<br><br>* `cos`：表示腾讯云 COS。<br><br>* `oss`：表示阿里云 OSS。<br><br>* `azure`：表示 Microsoft Azure。<br><br>* `aws_common`：表示 AWS S3 和 S3 兼容的鉴权方式。 |`cos` |
|TosAuthInformation |Object |否 |表示存储桶的访问凭证（AccessKey）。 | |
|AccessKeyId |String |否 |表示访问凭证中的 AccessKey ID，在腾讯云称为 SecretId，长度为 5\-100 个字符。 |`xxxxxxxx` |
|AccessKeySecret |String |否 |表示访问凭证中的 AccessKey Secret，在腾讯云称为 SecretKey，长度为 5\-100 个字符。 |`xxxxxx` |
|AccountKey |String |否 |表示您 Azure 存储账号的共享密钥（Key）。该参数仅当 `AuthType` 为 `azure` 时有效。 |`xxxxxx` |
|Region |String |否 |表示存储桶所在地域的信息，也就是存储桶的 region code。Region code 参与签名的计算。<br><br>如果 `AuthType` 是 `aws_common` 并且 `PrivateBucketAccess` 是 `true`，您必须指定该参数。 |`us-east-1` |
|BucketName |String |否 |表示您 Azure 存储账号的名称。该参数仅当 `AuthType` 为 `azure` 时有效。 |`mystorageaccount` |


<span id="条件源站"></span>
### 条件源站


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ConditionalOrigin |Object |否 |表示 "条件源站" 特性的配置。 | |
|OriginRules |Object[] |否 |表示一个规则列表。列表中的每条规则中定义了一组匹配条件以及 CDN 对满足匹配条件的请求所执行的操作。<br><br>列表中最多可以包含 20 条规则。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|Actions |Object |否 |表示一条规则中定义的操作配置。 | |
|OriginLines |Object[] |否 |表示一个源站列表。当前，列表中只能包含一个源站。 | |
|Address |String |否 |表示一个源站的地址。<br><br><br>* 当 `InstanceType` 是 `ip` 时，`Address` 表示一个 IPv4 或者 IPv6 地址。<br><br>* 当 `InstanceType` 是 `domain` 时，`Address` 表示一个域名。该域名不能是泛域名。<br><br>* 如果 `InstanceType` 是 `storage`，您指定的是存储桶域名，可以是云厂商分配的桶域名，也可以是您在云厂商处为存储桶设置的自定义域名。桶域名不能包含 `https://`，长度不能超过 100 个字符。存储桶可以来自火山引擎 TOS、阿里云 OSS、腾讯云 COS、AWS S3 或者任何使用鉴权方式与 S3 兼容的第三方对象存储服务，如七牛云、华为云等。 |`203.0.113.8` |
|HttpPort |String |否 |表示 CDN 使用 HTTP 协议访问该源站时所使用的端口，取值范围是 1\-65535，默认值是 `80`。如果源站服务器没有开放该端口，您无需指定该参数。 |`80` |
|HttpsPort |String |否 |表示 CDN 使用 HTTPS 协议访问该源站时所使用的端口，取值范围是 1\-65535，默认值是 `443`。如果源站服务器没有开放该端口，您无需指定该参数。 |`443` |
|InstanceType |String |否 |表示源站的类型。该参数有以下取值：<br><br><br>* `ip`：表示 IP 地址。<br><br>* `domain`：表示域名。<br><br>* `storage`：表示对象存储桶。<br><br><br>注意<br><br>在 CDN 向对象存储源站发送回源请求时，回源请求使用的方法与用户请求相同。默认情况下，用户请求可以使用的请求方法有 DELETE、GET、HEAD、POST、PUT、PATCH、OPTIONS、CONNECT。如果您不希望回源请求使用某些请求方法，例如您不希望回源请求使用 DELETE 方法，可能导致误删源站上的文件，建议您采取以下步骤：<br><br><br>1. 在存储桶所在的对象存储服务中设置权限，组织不符合预期的操作。<br><br>2. 在 CDN 的 `MethodDeniedRule` 特性中，指定 CDN 不支持的请求方法。 |`ip` |
|OriginHost |String |否 |表示回源请求访问的站点域名，适用于源站服务器上有多个站点的情况。<br><br><br>* 该参数的默认值与全局 `OriginHost` 相同，但优先级高于全局 `OriginHost` 参数。<br><br>* 该参数值的长度不能超过 1,024 个字符。<br><br>* 如果您在调用该 API 时，即没有修改 `Address`，也没有指定 `OriginHost`，`OriginHost` 不会被默认值覆盖，而是保持当前值。 |`img.example.com` |
|BucketSource |String |否 |表示存储桶使用的是哪个对象存储服务所提供的鉴权方式。该参数有以下取值：<br><br><br>* `tos`：表示 BytePlus TOS。<br><br>* `cos`：表示腾讯云 COS。<br><br>* `oss`：表示阿里云 OSS。<br><br>* `azure`：表示 Microsoft Azure。<br><br>* `aws_common`：表示 AWS S3 和 S3 兼容的鉴权方式。 |`aws_common` |
|PrivateBucketAccess |Boolean |否 |表示存储桶是否是私有桶。该参数仅当 `InstanceType` 为 `storage` 时有效。该参数有以下取值：<br><br><br>* `true`：表示该存储桶是私有桶。<br><br>* `false`：表示该存储桶不是私有桶。<br><br><br>该参数的默认值是 `false`。 |`true` |
|TosAuthInformation |Object |否 |表示存储桶的访问凭证（AccessKey）。<br><br>说明<br><br>如果存储桶是本账号下的 TOS 存储桶并且您使用跨服务授权方式访问 TOS 存储桶，该参数无需指定。跨服务授权访问方式无需指定 AccessKey。 | |
|AccessKeyId |String |否 |表示访问凭证中的 AccessKey ID，在腾讯云称为 SecretId。 |`xxxxxxxx` |
|AccessKeySecret |String |否 |表示访问凭证中的 AccessKey Secret，在腾讯云称为 SecretKey。 |`xxxxxxx` |
|Region |String |否 |表示存储桶所在地域的信息，也就是存储桶的 region code。Region code 参与签名的计算。<br><br>如果 `BucketSource` 是 `aws_common` 并且 `PrivateBucketAccess` 是 `true`，您必须指定该参数。 |`us-east-1` |
|AccountName |String |否 |表示您 Azure 存储账号的共享密钥（Key）。该参数仅当 `AuthType` 为 `azure` 时有效。 |`xxxxxxxxxxxxxxxxx` |
|OriginType |String |否 |表示源站的类别。该参数有以下取值：<br><br><br>* `primary`：表示主源站。<br><br>* `backup`：表示备源站。<br><br><br>源站列表中至少需要包含一个主源站。备源站是可选的。 |`primary` |
|Weight |String |否 |表示该源站的权重，取值范围是 1\-100，默认值是 `1`。权重越大，该源站在 CDN 发送回源请求时被选择到的概率也越大。 |`1` |
|Condition |Object |否 |表示该规则中匹配条件的配置。 | |
|ConditionGroups |Object[] |否 |表示一个匹配条件列表。列表中可以包含最多 50 个匹配条件。 | |
|Condition |Object |否 |表示一个匹配条件的配置。 | |
|Object |String |否 |表示一个匹配对象。该参数有以下取值：<br><br><br>* `path`：表示请求 URL 中的完整路径。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `full_querystring`：表示请求 URL 中的所有查询参数。<br><br>* `client_ip`：表示客户端的 IP 地址。<br><br>* `query_name`：表示请求 URL 中的而某个查询参数。<br><br>* `customize`：表示用户请求中的某个头部。 |`path` |
|Operator |String |否 |表示匹配类型。对于每个 `Object`，可指定的 `Operator` 如下所示：<br><br><br>* `path`：可指定 `equal`、`not_equal`、`regex_match`、`regex_not_match`。<br><br>* `directory`：可指定 `equal`、`not_equal`。<br><br>* `filetype`：可指定 `equal`、`not_equal`。<br><br>* `full_querystring`：可指定 `regex_match`、`regex_not_match`。<br><br>* `client_ip`：可指定 `equal`、`not_equal`、`belong`、`not_belong`。<br><br>* `query_name`：可指定 `equal`、`not_equal`、`regex_match`、`regex_not_match`、`exist`、`not_exist`、`empty`、`not_empty`。<br><br>* `customize`：可指定 `equal`、`not_equal`、`empty`、`not_empty`。<br><br><br>在以上取值中，`belong` 和 `not_belong` 的说明如下：<br><br><br>* `belong`：表示如果客户端 IP 地址归属地在 `Value` 所表示国家和地区列表中，该请求就满足这个匹配条件。<br><br>* `not_belong`：表示如果客户端 IP 地址归属地不在 `Value` 所表示国家和地区列表中，该请求才满足这个匹配条件。 |`equal` |
|Value |String[] |否 |表示一个或者多个匹配值，多个匹配值之间以分号（;）分隔。但是当 `Object` 是 `customize` 时，多个头部值之间以竖线（\\|）分隔。关于配置值的输入要求，参见 [控制台说明文档](https://docs.byteplus.com/en/docs/byteplus-cdn/conditional_origins_cn)。<br><br>说明<br><br>当 `Object` 是 `client_ip` 并且 `Operator` 是 `belong` 或者 `not_belong` 时，匹配值是一个或者多个国家或地区的代号。您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp)，以获取 CDN 支持的所有国家和地区的代号。在调用 `DescribeCdnRegionAndIsp` 时，请指定请求参数 `Area` 为 `Global`。 |`/www/img/my*image.png;/doc` |
|Name |String |否 |* 当 `Object` 为 `query_name` 时，该参数表示指定的查询参数的名称。<br><br>* 当 `Object` 为 `customize` 时，该参数表示指定的请求头的名称。<br><br>* 当 `Object` 为其他值时，该参数无需指定。 |`param1` |
|Type |String |否 |* 当 `Object` 为 `query_name` 时，该参数值必须是 `querystring`。<br><br>* 当 `Object` 为 `customize` 时，该参数值必须是 `request_header`。<br><br>* 当 `Object` 为其他值时，该参数无需指定。 |`request_header` |
|Connective |String |否 |表示这些匹配条件之间的关系。该参数有以下取值：<br><br><br>* `or`：表示关系是 "或"。<br><br>* `and`：表示关系是 "与"。<br><br><br>该参数的默认值是 `or`。 |`and` |
|IsGroup |Boolean |否 |该参数值必须是 `true`。 |`true` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="回源协议"></span>
### 回源协议


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginProtocol |String |是 |表示回源请求使用的协议。该参数有以下取值：<br><br><br>* `http`：表示回源请求使用 HTTP 协议。<br><br>* `https`：表示回源请求使用 HTTPS 协议。<br><br>* `followclient`：表示回源协议与用户请求使用的协议相同。 |`http` |


<span id="源站证书校验"></span>
### 源站证书校验


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginCertCheck |Object |否 |表示 "源站证书校验" 特性的配置。要使用此特性，请 [提交工单](https://console.byteplus.com/workorder/create)。<br><br>该特性启用后，CDN 会校验源站证书的合法性，包括证书是否已被吊销、证书是否由可信 CA 签发、证书与源站域名是否匹配等。CDN 内置了常见可信 CA 的根证书。如果源站证书未通过校验，CDN 进行 [回源重试](https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-cn)。如果回源重试时源站证书依然未通过校验，CDN 判定无法从该源站获取文件，并对用户请求响应 504 状态码。 | |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |
|CertInfoList |Object[] |否 |表示一个 CA 证书列表，列表中的 CA 证书托管在 CDN，且不能是国密证书。CDN 使用该列表中的 CA 证书对来自源站的服务器证书进行校验。<br><br>当前，该列表中只能包含一本 CA 证书。 | |
|CertId |String |否 |表示列表中一本 CA 证书的 ID，以 `cert_hosting` 开头。<br><br>您可以调用 [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcertinfo-cn) 查询托管在 CDN 的 CA 证书列表以获取您要指定的证书的 ID。 |`cert_hosting-104663` |


<span id="ipv6-回源"></span>
### IPv6 回源


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginIPv6 |String |否 |表示 "IPv6 回源" 的配置。该参数有以下取值：<br><br><br>* `ipv6_first`：表示 CDN 始终尝试获取源站域名的 IPv6 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv4 地址。<br><br>* `ipv4_first`：表示 CDN 始终尝试获取源站域名的 IPv4 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv6 地址。<br><br>* `followclient`：表示 CDN 尝试获取与用户请求相同类型的 IP 地址。<br><br><br>该参数的默认值是 `followclient`。<br><br>由于海外部分 CDN 回源节点不支持向 IPv6 地址发送回源请求，该功能仅适用于位于中国内地的回源节点。 |`followclient` |


<span id="回源-host"></span>
### 回源 Host


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginHost |String |否 |如果源站服务器上有多个站点，该参数表示回源请求访问的站点域名。该参数对所有源站配置生效，但是优先级低于源站配置中 `OriginHost` 参数。<br><br>该参数的默认值与 `Domain` 相同。<br><br>如果源站是一个对象存储桶，您无需指定该参数。其默认值与源站配置中的 `Address` 相同。 |`img.example.com` |


<span id="https-配置"></span>
## HTTPS 配置

<span id="https"></span>
### HTTPS


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|HTTPS |Object |否 |表示 HTTPS 加密服务的配置。 | |
|Switch |Boolean |是 |表示是否启用 HTTPS 加密服务。该参数有以下取值：<br><br><br>* `true`：表示启用 HTTPS 加密服务。<br><br>* `false`：表示禁用 HTTPS 加密服务。<br><br><br>如果 `Switch` 是 `true`，您必须指定 `CertInfo`。<br><br>您指定的证书可以托管在 BytePlus 证书中心，也可以托管在 CDN。 |`true` |
|CertInfo |Object |否 |表示要与域名关联的证书。<br><br><br>* 如果该证书已托管在 BytePlus 证书中心或者 CDN，您必须在 `CertId` 中指定该证书的 ID。<br><br>* 否则，您可以调用 [AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-cn-addcertificate) 上传您的证书或者在证书中心控制台购买证书，然后调用 `UpdateCdnConfig` 关联该证书。 | |
|CertId |String |否 |表示要关联的证书 ID。<br><br>您可以调用 [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcertinfo-cn) 获取您想要关联的证书 ID。 |`cert-eb5d99026753499a8a34d2a4f0a08d92` |
|DisableHttp |Boolean |否 |表示是否允许请求 URL 中 Scheme 是 `HTTP` 的请求。该参数有以下取值：<br><br><br>* `true`：表示允许 Scheme 是 `HTTP` 的请求。<br><br>* `false`：表示不允许 Scheme 是 `HTTP` 的请求。<br><br><br>该参数的默认值是 `false`。 |`false` |
|ForcedRedirect |Object |否 |表示 "HTTP 强制跳转到 HTTPS" 特性的配置。<br><br>说明<br><br>CDN 提供了两种协议重定向的特性。<br><br><br>* HTTP 重定向到 HTTPS，也就是 `ForcedRedirect` 特性。<br><br>* HTTPS 重定向到 HTTP，也就是 `HttpForcedRedirect` 特性。<br><br><br>这两个协议重定向特性是互斥的。也就是说，如果您启用了其中任意一个特性，就不能启用另一个。 | |
|StatusCode |String |是 |表示当收到 HTTPS 请求时 CDN 的重定向响应状态码。该参数有以下取值：<br><br><br>* `301`：表示返回的状态码是 301。<br><br>* `302`：表示返回的状态码是 302。<br><br><br>该参数的默认值是 `301`。 |`301` |
|EnableForcedRedirect |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。启用后，CDN 会将收到的 HTTP 请求重定向到 HTTPS 请求。<br><br>* `false`：表示禁用该特性。禁用后，CDN 不会将 HTTP 请求重定向到 HTTPS 请求。<br><br><br>要启用该特性，您的域名必须已启用 HTTPS。 |`true` |
|HTTP2 |Boolean |否 |表示是否为用户请求启用 HTTP/2 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 HTTP/2。<br><br>* `false`：表示禁用 HTTP/2。<br><br><br>要启用该特性，您的域名必须已经启用了 HTTPS 加密服务。<br><br>该参数的默认值是 `false`。 |`true` |
|Hsts |Object |否 |表示 HSTS 特性的配置。 | |
|Subdomain |String |否 |表示 HSTS 配置是否也应用于域名的子域名。该参数有以下取值：<br><br><br>* `include`：表示 HSTS 配置应用于子域名站点。<br><br>* `exclude`：表示 HSTS 配置不应用于子域名站点。<br><br><br>该参数的默认值是 `exclude`。 |`include` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |
|Ttl |Long |否 |表示 `Strict-Transport-Security` 响应头在浏览器中的缓存过期时间，单位是秒。如果 `Switch` 是 `true`，该参数为必填。该参数的取值范围是 0 \- 31,536,000。31,536,000 秒表示 365 天。如果该参数值为 `0`，其效果等同于禁用 HSTS 设置。 |`300` |
|OCSP |Boolean |否 |表示是否启用 "OCSP 装订" 特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>要启用该特性，您的域名必须启用了 HTTPS。该参数的默认值是 `false`。 |`true` |
|TlsVersion |String[] |否 |表示 "TLS 版本" 特性的配置。该参数指定用户请求可以使用的 TLS 版本，有以下取值：<br><br><br>* `tlsv1.0`：表示 TLS 1.0。<br><br>* `tlsv1.1`：表示 TLS 1.1。<br><br>* `tlsv1.2`：表示 TLS 1.2。<br><br>* `tlsv1.3`：表示 TLS 1.3。<br><br><br>该参数的默认值是 `["tlsv1.1", "tlsv1.2", "tlsv1.3"]` |`["tlsv1.1","tlsv1.2"]` |
|CertCheck |Object |否 |表示 "访问双向认证" 特性的配置。 | |
|CertInfoList |Object[] |否 |表示一个 CA 证书列表。列表中最多包含两个 CA 证书。这些 CA 证书必须是已经托管在 CDN 的。CA 证书使用的加密算法可以是 RSA 或者 ECC。<br><br>如果要关联的证书还未上传，您可以先调用 [AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-cn-addcertificate) 将该证书上传到 CDN。 | |
|CertId |String |否 |表示一个 CA 证书的 ID。ID 是以 `cert_hosting-` 开头的。<br><br>您可以调用 [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-listcertinfo-cn) 获取您需要关联的证书的 ID。 |`cert_hosting-31869` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="https-强制跳转到-http-设置"></span>
### HTTPS 强制跳转到 HTTP 设置

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要配置 HTTP 重定向至 HTTPS，参见 <code>HTTPS</code> 下的 <code>ForcedRedirect</code> 特性。<code>HttpForcedRedirect</code> 与 <code>ForcedRedirect</code> 是互斥的。也就是说，如果您配置了其中任意一个特性，就不能配置另一个。</div>



|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|HttpForcedRedirect |Object |否 |表示 "HTTPS 强制跳转到 HTTP" 特性的配置。 | |
|StatusCode |String |是 |表示当收到 HTTPS 请求时，CDN 返回的重定向状态码。该参数有以下取值：**301**、**302**、**303**、**307**、**308**。<br><br>该参数的默认值是 `301`。<br><br>需要留意的是：<br><br><br>* 对于 301 和 302，如果原请求使用的方法不是GET，那么客户端向新的URL发送请求时，新请求使用的方法可能变成 GET。<br><br>* 对于 303，新请求使用的方法是 GET。<br><br>* 对于 307 和 308，新请求使用的方法与原请求相同，不会被改变。 |`302` |
|EnableForcedRedirect |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。启用后，CDN 会将收到的 HTTPS 请求重定向到 HTTP 请求。<br><br>* `false`：表示禁用该特性。CDN 不会将 HTTPS 请求重定向到 HTTP 请求。<br><br><br>要启用该特性，您的域名必须已启用 HTTPS。 |`true` |


<span id="quic-设置"></span>
### QUIC 设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Quic |Object |否 |表示 QUIC 配置。 | |
|Switch |Boolean |是 |表示是否为用户请求启用 QUIC。该参数有以下取值：<br><br><br>* `true`：表示启用 QUIC。<br><br>* `false`：表示禁用 QUIC。<br><br><br>要启用该特性，您的域名必须已启用 HTTPS。 |`true` |


<span id="访问控制"></span>
## 访问控制

<span id="websocket"></span>
### WebSocket


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Websocket |Object |否 |表示 WebSocket 配置。 | |
|Switch |Boolean |否 |表示是否为用户请求启用 WebSocket 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 WebSocket。该特性启用后，CDN 可以响应来自客户端的 Websocket 请求。<br><br>* `false`：表示禁用 WebSocket。<br><br><br>该参数的默认值是 `false`。 |`true` |
|Timeout |Long |否 |表示 Websocket 连接的超时时间，单位是秒，取值范围是 1\-900。<br><br>该参数的默认值是 60 秒。 |`60` |


<span id="proxy-protocol"></span>
### PROXY Protocol


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ProxyProtocol |Object |否 |表示 PROXY Protocol 的配置。 | |
|Switch |Boolean |否 |表示是否为用户请求启用 PROXY Protocol 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 PROXY Protocol。该特性启用后，CDN 就可以对收到的 PROXY 协议头进行解析，以获取客户端的真实 IP 地址。<br><br>* `false`：表示禁用 PROXY Protocol。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="server-send-events-sse"></span>
### Server\-Send Events (SSE)


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ServerSentEvent |Object |否 |表示 SSE 的设置。 | |
|Switch |Boolean |否 |表示是否为用户请求启用 SSE 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 SSE。该特性启用后，对于收到的客户端 SSE 请求，CDN 扮演 SSE 代理的角色，将客户端请求透传到源站，并将源站 SSE 格式数据流推送至客户端。<br><br>* `false`：表示禁用 SSE。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="url-标准化"></span>
### URL 标准化


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|UrlNormalize |Object |否 |表示 "URL 标准化" 特性的配置。 | |
|NormalizeObject |String[] |否 |表示一个 URL 标准化选项列表。当 `Switch` 为 `true` 时，该参数为必填。列表中可以包含以下选项：<br><br><br>* `dot_segments`：表示将请求 URL 中的以下内容进行替换：<br><br>   * `/./`：替换为单个斜杠（/）。<br><br>   * `/../`：如果 `/../` 前还有一个级别的目录，则删除 `/../` 与该目录。如果 `/../` 前没有目录，则保留原 URL。<br><br>* `back_slashes`：表示将请求 URL 中的反斜杠（\）替换为单个斜杠（/）。<br><br>* `successive_slashes`：表示将请求 URL 中双斜杠（//）替换为单个斜杠（/）。 |`["dot_segments","back_slashes","successive_slashes"]` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="禁用-http-method"></span>
### 禁用 HTTP Method


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|MethodDeniedRule |Object |否 |表示 "禁用 HTTP Method" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|Methods |String |否 |表示被禁用的一个或多个 HTTP 请求方法。当 `Switch` 是 `true` 时，该参数为必填。多个方法使用逗号（,）分隔。该参数有以下取值：<br><br><br>* `get`：表示禁用 GET 请求方法。<br><br>* `post`：表示禁用 POST 请求方法。<br><br>* `delete`：表示禁用 DELETE 请求方法。<br><br>* `put`：表示禁用 PUT 请求方法。<br><br>* `head`：表示禁用 HEAD 请求方法。<br><br>* `patch`：表示 PATCH 请求方法。<br><br>* `connect`：表示 CONNECT 请求方法。<br><br>* `options`：表示 OPTIONS 请求方法。 |`delete,put` |


<span id="地域访问控制"></span>
### 地域访问控制


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|AreaAccessRule |Object |否 |表示 "地域访问控制" 特性的配置。 | |
|Area |String[] |否 |表示一个国家和地区的列表，对该列表应用地域访问限制。当 `Switch` 是 `true` 时，该参数为必填。国家和地区的名称使用简写来表示。您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 并指定 `Area` 为 `Global` 以获取国家和地区的简写。 |`["CHE","AZE"]` |
|RuleType |String |否 |表示 `Area` 的类型。当 `Switch` 是 `true` 时，该参数为必填。该参数有以下取值：<br><br><br>* `deny`: 表示 `Area` 是一个黑名单。CDN 将阻止来自这些国家和地区的请求。<br><br>* `allow`: 表示 `Area` 是一个白名单。CDN 仅允许来自这些国家和地区的请求。 |`allow` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |


<span id="ip-黑白名单"></span>
### IP 黑白名单


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|IpAccessRule |Object |否 |表示 "IP 黑白名单" 特性的配置。<br><br>该特性提供了两种配置方式：<br><br><br>* 常规配置：指定 `RuleType` 和 `Ip` 对当前域名进行配置。<br><br>* 全局配置：指定 `SharedConfig` 使用一个全局配置。<br><br><br>您只能选择一种配置方式。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RuleType |String |是 |表示 IP 名单的类型。当 `Switch` 是 `true` 时，该参数为必填。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。<br><br><br>如果您指定了 `SharedConfig`，就不能指定该参数。 |`deny` |
|Ip |String[] |是 |表示黑名单或白名单中的 IP 地址。当 `Switch` 是 `true` 时，该参数为必填。您可以指定一个或者多个 IP 地址和 IP 地址网段。IP 地址和网段可以是 IPv4 或 IPv6 格式。您最多可输入 1,000 个地址。<br><br>如果您指定了 `SharedConfig`，就不能指定该参数。 |`["xx.xxx.xx.xx","x.x.x.x"]` |
|SharedConfig |Object |否 |表示一个全局配置。<br><br>如果您指定了该参数，就不能指定 `RuleType` 和 `Ip`。 | |
|ConfigName |String |否 |表示一个全局配置的名称。该全局配置的 `ConfigType` 必须是 `deny_ip_access_rule` 或者 `allow_ip_access_rule`。<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名单。<br><br>* `allow_ip_access_rule`：表示 IP 白名单。<br><br><br>您可以调用 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn) 获取全局配置的列表。 |`my_whitelist` |
|DenyStatusCode |Long |否 |表示 CDN 在拒绝请求时响应的状态码，范围是 200 \- 999。如果不指定该配置，则 CDN 默认响应 403 状态码。 |`402` |
|IpSource |Object |否 |表示客户端 IP 地址获取方式的配置。 | |
|SourceList |String[] |否 |表示当 `Type` 为 `custom` 时，用于判断客户端 IP 地址的一个或多个来源。<br><br>取值：<br><br><br>* `x-real-ip`：表示从 `X-Real-IP` 请求头获取的 IP 地址。<br><br>* `x-forwarded-for`：表示从 `X-Forwarded-For` 请求头获取的 IP 地址。<br><br>* `client-ip`：表示真实建连 IP，即与 CDN 节点直接建立网络连接的对端 IP 地址。<br><br><br>对于 IP 黑名单，只要任一指定来源中获取的 IP 地址匹配黑名单规则，CDN 就拒绝请求。对于 IP 白名单，只有所有指定来源中获取的 IP 地址均匹配白名单规则，CDN 才允许请求。 |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |否 |表示 CDN 判断客户端 IP 地址的方式。<br><br>取值：<br><br><br>* `default`：使用真实建连 IP。<br><br>* `custom`：使用 `SourceList` 中指定的一个或多个来源。无法从已选请求头获取 IP 地址时，CDN 对该来源使用真实建连 IP。<br><br><br>该参数的默认值是 `default`。 |`custom` |


<span id="referer-黑白名单"></span>
### Referer 黑白名单


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|RefererAccessRule |Object |否 |表示 "Referer 黑白名单" 特性的配置。关于不同配置对请求匹配结果的影响，参见 [配置示例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-referer-restrictions-cn#%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RuleType |String |是 |表示 Referer 名单的类型。当 `Switch` 是 `true` 时，该参数为必填。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。 |`deny` |
|ReferersType |Object |是 |表示一个 `ReferersType` 对象。其包含一个 `CommonType` 对象和一个 `RegularType` 对象，分别表示一个常规 Referer 列表和一个用于匹配 Referer 的正则表达式列表。您可以同时定义这两个对象。<br><br>如果您指定了 `SharedConfig`，就不能指定该参数。 | |
|RegularType |Object |是 |表示一个 `RegularType` 对象，其包含一个正则表达式列表用来匹配请求中的 Referer 头部。要使用该参数，请 [提交工单](https://console.byteplus.com/workorder/create)。 | |
|Referers |String[] |是 |表示一个用于匹配 Referer 的正则表达式列表。该参数值的长度不能超过 30,000 个字符。 |`^http://a.com` |
|CommonType |Object |是 |表示一个 `CommonType` 对象，其包含一个常规 Referer 列表。 | |
|Referers |String[] |是 |表示一个常规 Referer 列表。在该列表中，您可以指定一个或者多个 IP 地址，CIDR 网段，域名和泛域名。域名可以是二级域名。IP 地址只能是 IPv4 格式的地址。您最多可输入 1,000 个 IP 地址。输入的域名不能包含 `http://` 或 `https://`。该参数值的长度不能超过 30,000 个字符。 |`["www.test.com","xxx.xxx.xx.xxx","1xx.xx.xx.x/24"]` |
|IgnoreCase |Boolean |否 |表示 `CommonType` 下的 `Referers` 列表是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`: 表示大小写不敏感。<br><br>* `false`: 表示大小写敏感。<br><br><br>该参数的默认值是 `true`。 |`true` |
|IgnoreScheme |Boolean |否 |表示 CDN 是否对 Referer 中的 scheme 进行校验，也就是校验 Referer 是否包含 `http://` 或者 `https://`。该参数有以下取值：<br><br><br>* `true`: 表示 CDN 不校验 Referer 是否包含 scheme。在这个情况下，无论 Referer 是否包含 scheme，CDN 都会将 Referer 与您配置的名单进行匹配校验。<br><br>* `false`: 表示 CDN 会先校验 Referer 是否包含 scheme。只有 Referer 包含 scheme，CDN 才会将 Referer 与您配置的名单进行匹配校验。否则，CDN 判定请求与您配置的名单不匹配。<br><br><br>该参数的默认值是 `false`。<br><br>另外，该配置对 `RegularType` 下的正则表达式列表不生效，因为 CDN 依赖正则表达式来判断 Referer 是否匹配正则名单。 |`false` |
|Referers |String[] |是 |表示一个 Referer 列表，该参数的输入要求与 `ReferersType` 下 `CommonType` 类型的 `Referers` 的输入要求相同。建议您使用 `ReferersType` 来指定 Referer 列表。<br><br>另外，如果您指定了 `SharedConfig`，就不能指定该参数。 |`["www.test.com","xxx.xx.x.x","xx.xx.xx.x/24"]` |
|AllowEmpty |Boolean |是 |表示当用户请求不包含 Referer 头部时，CDN 处理请求的方式。该参数有以下取值：<br><br><br>* `true`：表示如果请求不包含 Referer 头部，则该请求被认为匹配您配置的 Referer 列表。<br><br>* `false`：表示如果请求不包含 Referer 头部，则该请求被认为不匹配您配置的 Referer 列表。<br><br><br>该参数的默认值是 `false`。 |`true` |
|SharedConfig |Object |否 |表示一个全局配置。<br><br>如果您指定了该参数，就不能指定 `Referers`，也不能指定 `ReferersType`。 | |
|ConfigName |String |否 |表示一个全局配置的名称。该全局配置的 `ConfigType` 必须是 `deny_referer_access_rule` 或者 `allow_referer_access_rule`。<br><br><br>* `deny_referer_access_rule`：表示 Referer 黑名单。<br><br>* `allow_referer_access_rule`：表示 Referer 白名单。<br><br><br>您可以调用 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn) 获取全局配置的列表。 |`my_allowlist` |


<span id="ua-黑白名单"></span>
### UA 黑白名单


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|UaAccessRule |Object |否 |表示 "UA 黑白名单" 特性的配置。 | |
|UserAgent |String[] |是 |表示一个 UA 的列表。当 `Switch` 是 `true` 时，该参数为必填。该列表最多包含 1,000 个 UA。该参数的说明如下：<br><br><br>* 该参数值的长度不能超过 30,000 个字符。<br><br>* 如果 `RuleType` 是 `allow`，表示仅允许包含列表中的 UA 的请求访问域名。<br><br>* 如果 `RuleType` 是 `deny`，表示如果访问请求包含列表中的 UA，则不允许访问域名。<br><br><br>UA 能包含的字符有以下限制：<br><br><br>* UA 中可以使用 `*` 表示一个或者多个字符。`*` 仅可以出现在 UA 的开头和末尾。<br><br>* UA 不能只包含 `*`或者空格。<br><br>* UA 如果包含符号，符号必须是被 HTML 编码的。 |`["*curl*","*Mozilla*"]` |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RuleType |String |是 |表示 UA 名单的类型。当 `Switch` 是 `true` 时，该参数为必填。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。 |`deny` |
|IgnoreCase |Boolean |是 |表示 UA 字符串是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`: 表示 UA 字符串是大小写不敏感的。<br><br>* `false`: 表示 UA 字符串是大小写敏感的。<br><br><br>该参数的默认值是 `false`。 |`true` |
|AllowEmpty |Boolean |是 |表示当用户请求不包含 User\-Agent 头部时，CDN 处理请求的方式。该参数有以下取值：<br><br><br>* `true`：表示如果请求不包含 User\-Agent 头部，则该请求被认为匹配您配置的 User\-Agent 列表。<br><br>* `false`：表示如果请求不包含 User\-Agent 头部，则该请求被认为不匹配您配置的 User\-Agent 列表。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="origin-黑白名单"></span>
### Origin 黑白名单


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginAccessRule |Object |否 |表示 "Origin 黑白名单" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RuleType |String |是 |表示 Origin 列表的类型。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。 |`deny` |
|Origins |String[] |是 |表示一个 Origin 列表。列表中可以包含最多 100 个 Origins，总长度不能超过 3,000 个字符。Origin 可以是 IP 地址，CIDR 网段，域名或泛域名。域名可以是二级域名。IP 地址可以是 IPv4 或 IPv6 格式的地址。 |`["www.test.com"]` |
|IgnoreCase |Boolean |是 |表示 Origin 列表是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`: 表示 Origin 列表是大小写不敏感的。<br><br>* `false`: 表示 Origin 列表是大小写敏感的。<br><br><br>该参数的默认值是 `true`。 |`true` |
|AllowEmpty |Boolean |是 |表示当用户请求不包含 Origin 头部时，CDN 处理请求的方式。该参数有以下取值：<br><br><br>* `true`：表示如果请求不包含 Origin 头部，则该请求被认为匹配您配置的 Origin 列表。<br><br>* `false`：表示如果请求不包含 Origin 头部，则该请求被认为不匹配您配置的 Origin 列表。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="自定义拦截规则"></span>
### 自定义拦截规则


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|RequestBlockRule |Object |否 |表示 "自定义拦截" 特性的配置。要使用该功能，请 [提交工单](https://console.byteplus.com/workorder/create)。 | |
|BlockRule |Object[] |是 |表示一个规则列表。列表中最多可以包含 10 条规则。当 `Switch` 是 `true` 时，该参数为必填。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|BlockAction |Object |是 |表示一条规则中 CDN 行为的配置。 | |
|Action |String |是 |表示 CDN 如何处理匹配 `Condition` 的请求。该参数有以下取值：<br><br><br>* `refuse`：表示 CDN 拒绝请求并响应一个 4xx 的错误码。错误码在 `StatusCode` 中指定。<br><br>* `redirect`：表示 CDN 将请求重定向到 `RedirectUrl` 中指定的 URL。 |`refuse` |
|StatusCode |String |是 |表示对于匹配 `Condition` 的用户请求，CDN 的响应状态码。<br><br><br>* 当 `Action` 是 `refuse` 时，该参数表示一个 400\-499 范围内的错误码。<br><br>* 当 `Action` 是 `redirect` 时，该参数有以下取值：<br><br>   * `301`：表示响应状态码是 301。<br><br>   * `302`：表示响应状态码是 302。 |`403` |
|ErrorPage |String |否 |* 当 `Action` 是 `refuse` 时，该参数是可选的，说明如下：<br><br>   * 如果指定该参数，该参数表示 "全局配置" 特性中的一个自定义响应页面的名称。也就是说，当 CDN 拒绝请求时，返回该自定义页面。<br><br>   * 如果不指定该参数，表示 CDN 使用 `StatusCode` 中指定错误码的标准响应正文。<br><br>* 当 `Action` 是 `redirect` 时，该参数无效，可以不指定。 |`GlobalConfigName` |
|RedirectUrl |String |否 |* 当 `Action` 是 `redirect` 时，该参数必填，表示重定向 URL。URL 必须以 `http://` 或 `https://` 开头，长度不能超过 1,024 个字符。<br><br>* 当 `Action` 是 `refuse` 时，该参数无效，可以不指定。 |`http://www.example.com` |
|Condition |Object |是 |表示该规则中匹配条件的定义。 | |
|ConditionRule |Object[] |是 |表示一个匹配条件列表，用于匹配请求 URL 中的路径和查询参数、以及请求来自的客户端 IP 地址。列表中最多可以包含 5 个匹配条件。每个匹配条件包含匹配类型、对比类型和匹配值。 | |
|Object |String |是 |表示一个匹配类型。<br><br><br>* 当 `Type` 是 `url` 时，该参数有以下取值：<br><br>   * `path`：表示表示请求 URL 中的路径。<br><br>   * `directory`：表示路径中的一个目录。<br><br>   * `filetype`：表示路径末尾的扩展名。<br><br>   * `regex`：表示请求 URL 中的路径，通过正则表达式匹配。<br><br>* 当 `Type` 是 `querystring` 时，该参数有以下取值：<br><br>   * `query_name`：表示请求 URL 中的一个查询参数。<br><br>   * `full_querystring`：表示请求 URL 中的查询字符串。<br><br>* 当 `Type` 是 `client_ip` 时，该参数有以下取值：<br><br>   * `client_ip`：表示客户端的 IP 地址。<br><br>* 当 `Type` 是 `request_header` 时，该参数有以下取值：<br><br>   * `ua`：表示请求中 User\-Agent 头部。<br><br>   * `customize`：表示请求中的自定义头部。 |`filetype` |
|Operator |String |是 |表示一个对比类型。<br><br><br>* 当 `Object` 是 `path`、`directory`、`filetype` 时，该参数有以下取值：<br><br>   * `equal`：表示如果匹配 `Value` 中的任何值，该请求就满足这个匹配条件。<br><br>   * `not_equal`：表示如果不匹配 `Value` 中的所有值，该请求才满足这个匹配条件。<br><br>* 当 `Object` 是 `query_name` 时，该参数有以下取值：<br><br>   * `exist`：表示存在。匹配逻辑与 `equal` 相同。<br><br>   * `not_exist`：表示不存在。匹配逻辑与 `not_equal` 相同。<br><br>   * `belong_shared_config`：表示如果匹配 `Value` 表示的全局配置中所包含的任何值，该请求就满足这个匹配条件。<br><br>   * `not_belong_shared_config`：表示如果不匹配 `Value` 表示的全局配置中的所有值，该请求才满足这个匹配条件。<br><br>   * `empty`：表示值为空。<br><br>   * `not_empty`：表示值不为空。<br><br>   * `equal`：参见以上描述。<br><br>   * `not_equal`：参见以上描述。<br><br>* 当 `Object` 是 `regex`、`full_querystring`、`client_ip` 或 `ua` 时，该参数有以下取值：<br><br>   * `match`：描述与 `equal` 相同。<br><br>   * `not_match`：描述与 `not_equal` 相同。<br><br>* 当 `Object` 是 `ua` 或 `customize` 时，该参数还有以下**额外**取值：<br><br>   * `empty`：参见以上描述。<br><br>   * `not_empty`：参见以上描述。 |`not_equal` |
|Type |String |是 |表示一个匹配对象的类型。该参数有以下取值：<br><br><br>* `url`：表示请求 URL。<br><br>* `querystring`：表示请求 URL 中的查询字符串。<br><br>* `request_header`：表示请求中的头部。 |`url` |
|Value |String |是 |表示一个或者多个匹配值。<br><br><br>* 如果 `Type` 是 `request_header`，多个匹配值之间使用竖线（\\|）分隔。<br><br>* 如果 `Type` 不是 `request_header`，多个匹配值之间使用分号（;）分隔。<br><br><br>&nbsp;<br><br>该参数的输入要求如下：<br><br><br>* 当 `Object` 是 `path`、`directory` 或 `filetype` 时，所有匹配值的总长度不能超过 1,024 个字符，不能包含以下字符：<br><br>   * 双斜杠（//）、空格、美元符号（$）、问号（?）、句点（.）<br><br>* 当 `Object` 是 `path` 时，该参数有以下**额外**要求：<br><br>   * 每个匹配值必须以斜杠（/）开头。您可以在匹配值中使用一个或者多个星号（\*），每个星号表示一个或者多个字符。例如：`/www/img/my*image.png`。<br><br>* 当 `Object` 是 `directory` 时，该参数有以下**额外**要求：<br><br>   * 每个匹配值必须以斜杠（/）开头和结尾。例如：`/www/img/`。<br><br>* 当 `Object` 是 `filetype` 时，该参数有以下**额外**要求：<br><br>   * 每个匹配值无需以句点（.）开头。例如：`png;txt`。<br><br>* 当 `Object` 是 `query_name` 时，<br><br>   * 如果 `Operator` 是 `equal` 或者 `not_equal`，您只能指定一个匹配值，表示 `Name` 所表示的查询参数的值。该值的长度不能超过 256 个字符，可以包含数字、字母、百分号（%）、下划线（_）、中划线（\-）。<br><br>   * 如果 `Operator` 是 `belong_shared_config`、`not_belong_shared_config` 时，您只能指定一个匹配值。该匹配值是一个全局配置的名称。<br><br>   * 如果 `Operator` 是 `exist`、`not_exist`、`empty`、`not_empty`，该参数无效，可以不指定。<br><br>* 当 `Object` 是 `full_querystring` 或者 `regex` 时，每个匹配值都是一个正则表达式。多个匹配值之间使用分号（;）分隔。所有匹配值的总长度不能超过 1,024 个字符。<br><br>* 当 `Object` 是 `client_ip` 时，`Value` 中最多可以包含 50 个匹配值，总长度不能超过 30,000 个字符。每个匹配值是一个 IP 地址。IP 地址可以是 IPv4 地址、IPv4 CIDR 地址、IPv6 地址、IPv6 CIDR 地址。<br><br>* 当 `Object` 是 `custom` 或者 `ua` 时，`Value` 中最多可以包含 50 个匹配值，总长度不能超过 1,024 个字符。匹配值可以以 \* 开头和结尾。\* 表示任意连续字符。<br><br>   * 如果 `Object` 是 `custom`，每个匹配值是 `Name` 所表示的头部的值。<br><br>   * 如果 `Object` 是 `ua`，每个匹配值是一个 User\-Agent 头部值。<br><br>   * 如果 `Operator` 是 `empty`、`not_empty`，该参数无效，可以不指定。 |`png;txt` |
|Name |String |否 |当 `Object` 是 `query_name` 或者 `customize` 时，该参数有效。<br><br><br>* 如果 `Object` 是 `query_name`，该参数表示一个查询参数的名称。<br><br>* 如果 `Object` 是 `customize`，该参数表示一个自定义请求头的名称。<br><br><br>`Name` 的长度不能超过 256 个字符，可以包含数字、字母、百分号（%）、下划线（_）、中划线（\-）。 |`color` |
|Connective |String |是 |表示多条 `ConditionRule` 之间的关系。该参数有以下取值：<br><br><br>* `AND`：表示 "和"。<br><br>* `OR`：表示 "或"。<br><br><br>该参数的默认值是 `OR`。 |`AND` |
|RuleName |String |是 |表示规则的名称，长度不超过 20 个字符，可以包含字母、数字、下划线（_）、中划线（\-）、汉字。一个汉字占 3 个字符。 |`MyRule` |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |


<span id="url-重定向改写"></span>
### URL 重定向改写


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|RedirectionRewrite |Object |否 |表示 "URL 重定向改写" 特性的配置。要使用该功能，请 [提交工单](https://console.byteplus.com/workorder/create)。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RedirectionRule |Object[] |否 |表示一个 URL 重定向改写的规则的列表。当 `Switch` 是 `true` 时，该参数为必填。该列表最多可以包含 50 条规则。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|RedirectionAction |Object |是 |表示一个 URL 重定向改写的规则。 | |
|RedirectCode |String |是 |表示 URL 重定向的响应状态码。该参数的取值有 `301`、`302`、`303`、`307`、`308`。<br><br>需要留意的是：<br><br><br>* 对于 301 和 302，如果原请求使用的方法不是 GET，那么客户端向新的URL发送请求时，新请求使用的方法可能变成 GET。<br><br>* 对于 303，新请求使用的方法是 GET。<br><br>* 对于 307 和 308，新请求使用的方法与原请求相同，不会被改变。 |`301` |
|SourcePath |String |是 |表示文件的原路径。也就是请求中包含的路径。路径必须以斜杠（/）开头并且不能包含双斜杠（//）、百分号（%）、空格。该参数值的长度不能超过 1,024 个字符。 |`/img/image.png` |
|TargetHost |String |是 |表示目标路径所归属站点的域名或者 IP 地址。IP 地址必须是 IPv4 类型的地址。该参数值的长度不能超过 1,024 个字符。该参数的默认值就是您的域名。 |`www.test.com` |
|TargetPath |String |是 |表示跳转后的目标路径。路径必须以斜杠（/）开头并且不能包含双斜杠（//）、百分号（%）、空格。该参数值的长度不能超过 1,024 个字符。 |`/png/image.png` |
|TargetProtocol |String |是 |表示 URL重定向后的新请求所使用的协议。该参数有以下取值：<br><br><br>* `followclient`：表示使用原请求的协议。<br><br>* `http`：表示新请求强制使用 HTTP 协议。<br><br>* `https`：表示新请求强制使用 HTTPS 协议。 |`followclient` |
|TargetQueryComponents |Object |是 |表示原请求 URL 中的查询参数的处理方式。 | |
|Action |String |是 |表示原请求 URL 中的查询参数的处理方式。该参数有以下取值：<br><br><br>* `include`：表示在跳转后的 URL 中包含原请求 URL 中的所有查询参数。<br><br>* `exclude`：表示在跳转后的 URL 中不包含原请求 URL 中的任何查询参数。<br><br>* `includePart`：表示在跳转后的 URL 中包含原请求 URL 中特定的查询参数。<br><br>* `excludePart`：表示在跳转后的 URL 中不包含原请求 URL 中特定的查询参数。 |`include` |
|Value |String |是 |表示要保留或删除的查询参数。多个查询参数间使用英文分号（;）分隔。指定的查询参数不能包含双斜杠（//）、百分号（"）、空格。`Value` 的默认值是 `*`，表示所有的查询参数。<br><br><br>* 如果 `Action` 是 `include` 或者 `exclude`, 则 `Value` 必须为 `*`。<br><br>* 如果 `Action` 是 `includePart` 或者 `excludePart`，您可以指定一个或者多个查询参数。此时，您指定的查询参数不能是 `*`。 |`seq` |


<span id="url-鉴权"></span>
### URL 鉴权


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|SignedUrlAuth |Object |否 |表示 "URL 鉴权" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|SignedUrlAuthRules |Object[] |否 |表示一个规则列表。每条规则包含匹配条件配置和鉴权配置。当前，列表中只能包含一条规则。当 `Switch` 是 `true` 时，该参数为必填。 | |
|Condition |Object |是 |表示匹配条件的配置。CDN 对符合条件的用户请求进行鉴权。 | |
|ConditionRule |Object[] |是 |表示一个匹配条件列表。<br><br><br>* 当 `URLAuthType` 是 `typea`、`typed`、`typee` 时，您最多可以创建 10 个条件。<br><br>* 当 `URLAuthType` 是 `typeb`、`typec` 时，您只能创建 1 个条件。 | |
|Object |String |是 |表示匹配条件中的匹配类型。该参数有以下取值：<br><br><br>* `filetype`：表示 URL 路径末尾的扩展名。<br><br>* `directory`：表示 URL 路径中的一个目录。<br><br>* `path`：表示完整的 URL 路径。<br><br>* `regex`: 表示完整的 URL 路径，通过正则表达式匹配。要指定该参数值，请 [提交工单](https://console.byteplus.com/workorder/create)。<br><br><br>需要留意的是，当 `URLAuthType` 是 `typeb`、`typec` 时，您只能指定该参数值为 `filetype` 或 `directory`。 |`directory` |
|Operator |String |是 |表示匹配条件中的匹配方式。该参数有以下取值：<br><br><br>* `match`：表示如果 `object` 匹配 `Value`，该请求就满足了这个匹配条件。<br><br>* `not_match`：表示如果 `object` 不匹配 `Value`，该请求就满足了这个匹配条件。<br><br><br>该参数的默认值是`match`。<br><br>需要留意的是，当 `URLAuthType` 是 `typeb`、`typec` 时，您只能指定该参数值为 `match`。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示匹配条件中的匹配值。多个匹配值之间以分号（;）分隔，总长度不能超过 1,024 个字符，不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>另外，<br><br><br>* 如果 `Object` 是 `filetype`，则每个匹配值是一个文件后缀，不能以句点（.）开头。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，则每个匹配值是一个目录路径，必须以斜杠（/）开头和结尾。例如：`/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，则每个匹配值是一个 URL 路径，必须以斜杠（/）开头。匹配值可以包含星号（\*）用来表示一个或者多个任意字符。例如：`/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果 `Object` 是 `regex`，则每个匹配值是一个正则表达式，用于匹配 URL 路径。例如：`^/a{1,2}.*g$`。 |`png;jpg` |
|Connective |String |是 |表示多个 `ConditionRule` 之间的逻辑关系。该参数有以下取值：<br><br><br>* `AND`: 表示逻辑关系是 "AND"。<br><br>* `OR`：表示逻辑关系是 "OR"。<br><br><br>该参数的默认值是 `OR`。<br><br><br>* 当 `URLAuthType` 是 `typeb`、`typec` 时，该参数值必须是 `OR`。 |`OR` |
|SignedUrlAuthAction |Object |是 |表示签名计算的配置。 | |
|Duration |Long |是 |表示签名的有效时间，单位是秒。该参数与请求中包含时间戳搭配使用，用来计算签名的过期时间。该参数的取值范围是 `0-315,360,000`。签名的过期时间 = 时间戳 + `Duration`。在 CDN 收到某个请求时，如果签名的过期时间小于当前时间，CDN 判定签名已过期。 |`1000` |
|MasterSecretKey |String |是 |表示主密钥，长度不超过 120 个字符。 |`abcdefg` |
|URLAuthType |String |是 |签名类型。该参数有以下取值：`typea`、`typeb`、`typec`、`typed`、`typee`，每种类型得鉴权说明见 [配置 URL 鉴权](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-overview-cn) 。 |`typea` |
|BackupSecretKey |String |否 |表示备密钥，长度不超过 120 个字符。 |`abcdefg` |
|CustomVariableRules |Object |否 |表示自定义签算变量。 | |
|CustomVariableInstances |Object[] |是 |表示一个变量列表。 | |
|Operator |String |是 |表示变量的匹配方式。该参数的取值只能是 `match`。 |`match` |
|Type |String |是 |表示变量的类型。该参数有以下取值：<br><br><br>* `queryString`：表示该变量是请求中的一个查询参数。<br><br>* `requestHeader`：表示该变量是请求中的一个头部字段。 |`queryString` |
|Value |String |是 |表示变量的名称，长度不超过 100 个字符。变量名称的要求如下：<br><br><br>* 如果 `Type` 是 `queryString`，变量名称可以包含以下字符：<br><br>   * 字母、数字、连字符（\-）、逗号（,）、句号（.）、感叹号（!）<br><br>* 如果 `Type` 是 `requestHeader`，变量名称不能包含以下字符：<br><br>   * 下划线（_）、空格、双引号（"）、冒号（:） |`myparam1` |
|KeepOriginArg |Boolean |否 |表示 CDN 是否在回源请求中包含用户请求中的签名参数，仅当 `URLAuthType` 是 `typea` 或 `typed` 时有效。<br><br>该参数有以下取值：<br><br><br>* `true`：表示 CDN 在回源请求中包含签名参数。<br><br>* `false`：表示 CDN 在回源请求中不包含签名参数。<br><br><br>该参数的默认值是 `false`。<br><br>当 `URLAuthType` 是 `typeb`、`typec` 或 `typee` 时，该参数不生效。<br><br><br>* 对于 `typeb` 和 `typec`CDN 在回源请求中不包含签名参数。<br><br>* 对于 `typee`，CDN 基于 `DeleteAuthCacheAndOrigin` 来判定是否在回源请求中包含签名参数。 |`true` |
|RewriteM3u8 |Boolean |否 |对于 HLS Manifest (.m3u8) 的请求，该参数表示 CDN 是否要修改 Manifest，从而为每个视频分片生成签名并将签名添加到 URI 中。<br><br>该参数有以下取值：<br><br><br>* `true`：表示需要修改 Manifest。<br><br>* `false`：表示不需要修改 Manifest。<br><br><br>该参数的默认值是 `false`。<br><br>说明<br><br>当前，CDN 不会修改压缩文件。因此，在以下任何情况下，CDN 都不会修改 Manifest。<br><br><br>* 源站响应中包含 `Content-Encoding` 头部。该标头表明该 Manifest 已被压缩。<br><br>* 用户请求匹配 "智能压缩" 特性中的规则。 |`true` |
|SignName |String |否 |表示签名参数的名称。该参数的说明如下：<br><br><br>* 可以包括英文字母、数字、下划线（_）、中划线（\-）、句号（.）、逗号（,）、感叹号（!）。<br><br>* 长度不能超过 100 个字符。<br><br>* 至少包含一个字母。<br><br>* 不能与 `TimeName` 相同。<br><br><br>当 `URLAuthType` 为 `typea`、`typed`、`typee` 时，该参数为必填。对于其他类型，该参数不生效。 |`sign` |
|SignatureRule |String[] |否 |当 `URLAuthType` 为 `typee` 时，该参数为必填，表示需要纳入签名计算的字段。必须纳入签名计算的字段如下：<br><br><br>* `key`：表示`MasterSecretKey`或 `BackupSecretKey` 指定的密钥。<br><br>* `uri`：表示用户请求的 URI，仅包含字路径和查询参数。如果 URI 包含中文字符，您需要对 URI 编码。<br><br>* `TimeName`：表示 `TimeFormat` 指定的时间戳。<br><br><br>可选择纳入签名计算的字段如下：<br><br><br>* `domain`：表示域名。<br><br>* `referer`：表示用户请求携带的 referer 值。<br><br>* `ua`：表示用户请求携带的 User\-Agent 值。<br><br>* `ip`：表示用户请求的客户端 IP。<br><br>* `origin`：表示用户请求携带的 Origin 值。<br><br>* 自定义变量：表示您在 `CustomVariableInstances` 中定义的变量的值。<br><br><br>CDN 按列表中字段的顺序将这些字段拼接成一个字符串，然后计算该字符串的 MD5 值。该 MD5 值就是签名。 |`["domain","ip","key","TimeName","uri"]` |
|TimeFormat |String |否 |表示 `TimeName` 使用的时间格式。该参数有以下取值：<br><br><br>* `basicFormat2m`：格式为 YYYYMMDDHHMM。<br><br>* `decimal`：十进制时间戳。<br><br>* `heximal`：十六进制时间戳。<br><br><br>该参数的使用说明如下：<br><br><br>* 当 `URLAuthType` 为 `typea` 时，该参数可以不指定，其值始终为 `decimal`。<br><br>* 当 `URLAuthType` 为 `typeb` 时，该参数为必填，可选取值为 `decimal`、`heximal` 和 `basicFormat2m`。<br><br>* 当 `URLAuthType` 为 `typec` 时，该参数可以不指定，其值始终为 `heximal`。<br><br>* 当 `URLAuthType` 为 `typed`、`typee` 时，该参数为必填，可选取值为 `decimal` 和 `heximal`。 |`heximal` |
|TimeName |String |否 |表示时间戳参数的名称。`TimeName` 的值可以包括英文字母、数字、下划线（_）、中划线（\-）、句号（.）、逗号（,）、感叹号（!），长度为 `1-100` 个字符。`TimenName` 不能与 `SignName` 相同。<br><br>当 `URLAuthType` 为 `typed`、`typee` 时，该参数为必填。对于其他类型，该参数不生效。 |`TimeParam` |
|RewriteM3u8Rule |Object |否 |表示 "M3U8 改写" 功能的配置。该配置仅当 `RewriteM3u8` 是 `true` 时才有效。 | |
|DeleteParam |Boolean |否 |表示在改写分片 URL 时是否保留 URL 中原有的参数。该参数有以下取值：<br><br><br>* `true`：表示删除原有参数。<br><br>* `false`：表示保留原有参数。<br><br><br>该参数的默认值是 `false`。需要留意的是，该参数的设置影响签名的计算。 |`true` |
|KeepM3u8Param |Boolean |否 |表示是否将来自该 M3U8 文件请求的不表示签名的查询参数添加到分片 URL 中。该参数有以下取值：<br><br><br>* `true`：表示在分片 URL 中添加查询参数。<br><br>* `false`：表示不添加查询参数。<br><br><br>该参数的默认值是 `false`。需要留意的是，该参数的设置影响签名的计算。 |`true` |
|RewriteTag |Object |否 |表示 "标签改写" 的配置。您可以定义除了 `EXTINF` 以外的标签。 | |
|Switch |Boolean |否 |表示是否需要改写额外标签中的分片 URL。该参数有以下取值：<br><br><br>* `true`: 表示需要改写额外标签。<br><br>* `false`：表示无额外标签需要改写。<br><br><br>该参数的默认值是 `false`。 |`true` |
|Tags |String[] |否 |表示除默认标签外，需要对其下分片 URI 进行改写的额外标签列表。<br><br>列表中最多包含 20 个标签，每个标签的长度为 1\-100 个字符，不能包含 `#` 和 `:`。 |`["EXT-X-MAP", "My-TAG"]` |
|AuthAlgorithm |String |否 |表示签名计算使用的算法。该配置有以下取值：<br><br><br>* `md5`：表示 MD5 算法。<br><br>* `sha256`：表示 SHA\-256 算法。<br><br><br>该参数的默认值是 `md5`。 |`md5` |
|DeleteAuthCacheAndOrigin |Boolean |否 |表示 CDN 是否在回源请求和缓存键中包含用户请求中的签名参数，仅当 `URLAuthType` 是 `typee` 时有效。<br><br>该参数有以下取值：<br><br><br>* `true`：表示回源请求和缓存键中均不包含签名参数。<br><br>* `false`：表示回源请求和缓存键中均包含签名参数。<br><br><br>该参数的默认值是 `false`。 |`false` |
|AuthRulesF |Object[] |否 |表示 Type\-F 配置，包含一个规则列表。列表中可以包含最多 5 条规则。列表中第一条规则的优先级最高。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|ArgumentRule |Object |否 |表示回源参数相关的配置。 | |
|KeepOriginArg |Boolean |否 |表示是否在回源请求中包含基于 `AuthTokenCalRule` 计算的令牌。该参数有以下取值：<br><br><br>* `true`：表示在回源请求中包含令牌。回源请求中令牌出现的位置与 `SignCapRule` 中的设置相同。<br><br>* `false`：表示不在回源请求中包含令牌。 |`true` |
|GeneralParamRule |Object |否 |表示 CDN 设置视频分片 URI 中查询参数的方式。 | |
|ParentLinkParamInherit |String |否 |表示改写后的视频分片 URI 是否包含用户请求 URL 中除表示令牌和令牌时间戳的参数之外的所有查询参数。该参数有以下取值：<br><br><br>* `not_inherit`：表示改写后的分片 URI 不会包含这些查询参数。<br><br>* `inherit`：表示改写后的分片 URI 会包含这些查询参数。 |`not_inherit` |
|SubLinkParamRule |Object |否 |该结构体包含额外的查询参数设置。该结构体包含额外的查询参数设置。 | |
|InheritMode |String |否 |表示当视频分片 URI 和用户请求 URL 中存在相同的查询参数时，CDN 如何设置视频分片 URI 中该参数的值。当 `ParentLinkParamInherit` 为 `inherit` 时，您可以设置该参数。<br><br>该参数有以下取值：<br><br><br>* `sub_link_first`：表示使用视频分片 URI 中该参数的值。<br><br>* `inherit_first`：表示使用用户请求 URL 中该参数的值。 |`inherit_first` |
|KeepSubLinkArg |String |否 |表示改写后的视频分片 URI 是否保留 URI 中原有的查询参数。该参数有以下取值：<br><br><br>* `delete`：表示改写后的分片 URI 不会保留这些查询参数。<br><br>* `keep`：表示改写后的分片 URI 会保留这些查询参数。 |`delete` |
|AuthTokenCalRule |Object |否 |表示令牌计算的设置。请参考 示例代码 在客户端部署令牌计算逻辑，将生成的令牌包含在用户请求中。<br><br>CDN 使用 `SignJoinSymbol` 将 `SignParam` 中的各对象进行拼接，然后对拼接后的对象应用 `ParamCalRules` 中指定的算法计算令牌，用于与用户请求中包含的令牌进行比较。 | |
|ParamCalRules |String[] |否 |表示计算令牌所使用的算法列表，列表中最多包含 5 个算法。CDN 按列表中算法的出现顺序生成令牌的计算公式。<br><br>该参数有以下取值：`md5_bin`、`base64url`、`sha256`、`md5`、`base64_encode`、`sha1`、`sha224`、`sha384`、`sha512`、`sha3_224`、`sha3_256`、`sha3_384`、`sha3_512`、`upper_case`、`lower_case`。<br><br>说明<br><br>如果您指定了 `md5_bin`，您必须指定下一个算法为 `base64url`。<br><br><br>* 正确配置：`sha1`、`md5_bin`、`base64url`<br><br>* 错误配置：`sha1`、`md5_bin`、`base64url`、`base64url`、`md5_bin` |`["sha1"、"md5_bin"、"base64url"]` |
|SignJoinSymbol |String |否 |表示拼接 `SignParam` 中各对象而使用的拼接符。该参数的默认值为空（""）。 |`00` |
|SignParam |Object[] |否 |表示 CDN 在计算令牌时使用的对象列表。每个对象由 `ParamType` 和相关配置组成。例如，以下示例表示对象是一个字符串，字符串的值是 `str-for-token-calc`。<br><br>```json```<br>```{```<br>```    "ParamType": "SupString",```<br>```    "SupContent": "str-for-token-calc"```<br>```}```<br> | |
|CookieToken |String |否 |当 `ParamType` 是 `Cookie` 时，您必须指定该参数。该参数表示您要指定的 cookie 的 key。CDN 会获取该 cookie 的 value。 |`mycookiekey` |
|ParamSource |String |否 |当 `RewriteMPD` 或者 `RewriteM3U8` 为启用，并且对象的 `ParamType` 是 `URI`、`URLParam` 或者 `FullURI` 时，您可以指定该参数。<br><br>对于添加到 Manifest 中的令牌，该参数表示 CDN 在使用该对象计算令牌时，该对象的来源。<br><br>该参数有以下取值：<br><br><br>* `ParentLink`：表示该对象来自用户请求中的 URL。<br><br>* `ChildLink`：表示该对象来自 Manifest 中视频分片的 URI。<br><br><br>该参数的默认值是 `ChildLink`。 |`ParentLink` |
|ParamType |String |否 |表示对象的类型。该参数有以下取值：<br><br><br>* `SecretKey`：表示 `SecretKey` 结构体中的 `MasterSecretKey` 或者 `BackupSecretKey`。当鉴权失败时，CDN 会使用 `BackupSecretKey` 计算令牌，重新对用户请求进行鉴权。<br><br>* `SupString`：表示一个字符串。相关配置在 `SupContent` 中指定。<br><br>* `URI`：表示请求路径中的连续片段。路径不包含查询字符串。相关配置在 `UriParamSup` 与 `ParamSource` 中指定。<br><br>* `URLParam`：表示请求 URL 中的某类对象。对象可以是一个查询参数或者某个目录。相关配置在 `UriParam` 与 `ParamSource` 中指定。<br><br>* `ClientDomain`：表示请求域名。<br><br>* `Referer`：表示用户请求中 Referer 头部的值。<br><br>* `Origin`：表示用户请求中 Origin 头部的值。<br><br>* `ClientIP`：表示发送用户请求的客户端 IP 地址。<br><br>* `UA`：表示用户请求中 Use\-Agent 头部的值。<br><br>* `ReqHeader`：表示用户请求中某个头部的值。相关配置在 `RequestHeader` 中指定。<br><br>* `Cookie`：表示请求中的一个 cookie。相关配置在 `CookieToken` 中指定。<br><br>* `FullURI`：表示请求的完整路径，不包含查询字符串。相关配置在 `ParamSource` 中指定。 |`URI` |
|RequestHeader |String |否 |当 `ParamType` 是 `ReqHeader` 时，您必须指定该参数。该参数表示您要指定的请求头。 |`myheader2` |
|SupContent |String |否 |当 `ParamType` 是 `SupString` 时，您必须指定该参数。该参数表示您要指定的字符串。 |`123abc` |
|UriParamSup |Object |否 |表示从请求路径中获取连续片段的方式。当 `ParamType` 是 `URI` 时，您必须指定该参数。<br><br>该参数是一个结构体，包含以下配置：<br><br><br>* 拆分请求路径所使用的分隔符。<br><br>* 所需连续路径片段的开始层级和结束层级。<br><br>* 拼接这些路径片段所使用的拼接符。拼接后的路径片段用于计算令牌。 | |
|JoinSymbol |String |否 |表示拼接这些路径片段所使用的拼接符，要求如下：<br><br><br>* 长度为 1 个字符，可以是字母、数字、下划线（_）、连字符（\-）、反斜杠（/）、感叹号（!）。<br><br><br>该参数的默认值是空（""）。 |`00` |
|SplitSymbol |String |否 |表示拆分请求路径所使用的分隔符，要求如下：<br><br><br>* 长度为 1 个字符，可以是字母、数字、下划线（_）、连字符（\-）、反斜杠（/）、感叹号（!）。 |`-` |
|StartLevel |Long |否 |表示起始片段所在的层级，要求如下：<br><br><br>* 必须是一个正整数。<br><br>* 不能大于层级总数。<br><br>* `StartLevel` 所表示的路径片段不能在 `TermLevel` 所表示的路径片段右侧。 |`2` |
|TermLevel |Long |否 |表示结束片段所在的层级，要求如下：<br><br><br>* 只能是非 0 的整数。<br><br>* 绝对值不能大于层级总数。<br><br><br>如果 `TermLevel` 是负整数，表示从最右边的片段开始向左计数。 |`3` |
|UrlParam |Object |否 |表示从 URL 中获取所需对象的方式。当 `ParamType` 是 `URLParam` 时，您必须指定该参数。<br><br>该参数是一个结构体，包含对象的来源以及相关配置。 | |
|ArgSegment |Object |否 |表示基于 `ParamName` 或者 `UriLevel` 获取的内容是否需要被拆分，以提取某个层级的片段。该片段才是您需要获取的对象。 | |
|Level |Long |否 |表示将获取到的内容拆分为多个层级的片段后，您需要的对象所在的层级。该参数的要求如下：<br><br><br>* 层级是非 0 的整数。<br><br>* 层级的绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从最右边层级的片段开始向左计数。<br><br>当 `Switch` 为 `true` 时，您必须指定该参数。 |`2` |
|SplitSymbol |String |否 |表示用于拆分内容而使用的分隔符。<br><br>当 `Switch` 为 `true` 时，您必须指定该参数。 |`-` |
|Switch |Boolean |否 |表示获取到的内容是否需要被拆分。该参数有以下取值：<br><br><br>* `true`：表示内容需要被拆分。<br><br>* `false`：表示内容无需被拆分。<br><br><br>该参数的默认值是 `false`。 |`true` |
|CapMode |String |否 |表示对象的来源。该参数有以下取值：<br><br><br>* `name`：表示查询参数。相关配置在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示请求路径中指定的目录。相关配置在 `UriLevel` 和 `ArgSegment` 中指定。 |`uri` |
|ParamName |String |否 |当 `ParamType` 是 `name` 时，您必须指定该参数。该参数表示您要指定的查询参数。 |`myparam3` |
|UriLevel |Long |否 |当 `ParamType` 是 `uri` 时，您必须指定该参数。该参数表示您要指定的目录层级。<br><br>该参数的要求如下：<br><br><br>* 层级是非 0 的整数。<br><br>* 绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从最右边的目录开始向左计数。 |`2` |
|CustomRewrite |Object |否 |表示视频 Manifest 的扩展改写配置。该配置启用后，CDN 使用 [特殊改写逻辑](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn#%E8%A7%86%E9%A2%91-manifest-%E7%9A%84%E7%89%B9%E6%AE%8A%E6%94%B9%E5%86%99%E9%80%BB%E8%BE%91) 覆盖 [默认改写逻辑](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn#%E8%A7%86%E9%A2%91-manifest-%E7%9A%84%E9%BB%98%E8%AE%A4%E6%94%B9%E5%86%99%E9%80%BB%E8%BE%91)。 | |
|RewriteParam |Object[] |否 |表示一个对象列表。CDN 将这些对象拼接而生成令牌，添加到视频分片的 URL 中。 | |
|ParamType |String |否 |表示对象的类型。该参数有以下取值：<br><br><br>* `ParentLinkUrlParam`：表示用户请求 URL 中的某类对象。对象可以是一个查询参数或者某个层级的路径目录。相关配置在 `ParentLinkUrlParam` 结构体中指定。<br><br>* `SupString`：表示一个字符串。相关配置在 `SupContent` 中指定。<br><br>* `ParentLinkURI`：表示用户请求路径中的连续片段。路径不包含查询字符串。相关配置在 `ParentLinkUriParamSup` 中指定。<br><br>* `ParentLinkExpire`：表示用户请求中令牌的时间戳。参见 `ExpireTimeRule` 下 `Duration` 参数的说明。<br><br>* `AuthToken`：表示基于 `AuthTokenCalRule` 计算的令牌。<br><br>* `ParentFullURI`：表示用户请求的完整路径，不包含查询字符串。 |`ParentLinkURI` |
|SupContent |String |否 |当 `ParamType` 是 `SupString` 时，您必须指定该参数。该参数表示您要指定的字符串。 |`abc-13343` |
|ParentLinkUriParamSup |Object |否 |表示从用户请求路径中获取对象的方式。当 `ParamType` 是 `ParentLinkURI` 时，您必须指定该参数。<br><br>该参数是一个结构体，包含以下配置：<br><br><br>* 拆分请求路径所使用的分隔符。<br><br>* 连续路径片段的开始层级和结束层级。<br><br>* 拼接这些路径片段所使用的拼接符。拼接后的路径片段用于生成令牌。 | |
|JoinSymbol |String |否 |表示拼接这些路径片段所使用的拼接符，要求如下：<br><br><br>* 长度为 1 个字符，可以是字母、数字、下划线（_）、连字符（\-）、反斜杠（/）、感叹号（!）。 |`00` |
|SplitSymbol |String |否 |表示拆分请求路径所使用的分隔符，要求与 `JoinSymbol` 相同。 |`-` |
|StartLevel |Long |否 |表示起始片段所在的层级，要求如下：<br><br><br>* 必须是正整数。<br><br>* 不能大于层级总数。<br><br>* `StartLevel` 所表示的路径片段不能在 `TermLevel` 所表示的路径片段右侧。 |`1` |
|TermLevel |Long |否 |表示结束片段所在的层级，要求如下：<br><br><br>* 只能是非 0 的整数。<br><br>* 绝对值不能大于层级总数。<br><br><br>如果 `TermLevel` 是负整数，表示从最右边的片段开始向左计数。 |`3` |
|ParentLinkUrlParam |Object |否 |表示从 URL 中获取对象的方式。当 `ParamType` 是 `ParentLinkUrlParam` 时，您必须指定该参数。<br><br>该参数是一个结构体，包含对象的来源以及相关配置。 | |
|ArgSegment |Object |否 |表示基于 `ParamName` 或者 `UriLevel` 获取的内容是否需要被拆分，以提取某个层级的片段。该片段才是您需要获取的对象。 | |
|Level |Long |否 |表示将获取的内容拆分为多个层级的片段后，您需要的片段所在的层级。该参数的要求如下：<br><br><br>* 层级是非 0 的整数。<br><br>* 绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从最右边的片段开始向左计数。<br><br>当 `Switch` 为 `true` 时，您必须指定该参数。 |`2` |
|SplitSymbol |String |否 |表示用于拆分内容的分隔符。<br><br>当 `Switch` 为 `true` 时，您必须指定该参数。 |`-` |
|Switch |Boolean |否 |表示获取的内容是否需要被拆分。该参数有以下取值：<br><br><br>* `true`：表示内容需要被拆分。<br><br>* `false`：表示内容无需被拆分。<br><br><br>该参数的默认值是 `false`。 |`true` |
|CapMode |String |否 |表示对象的来源。该参数有以下取值：<br><br><br>* `name`：表示查询参数。相关配置在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示请求路径中指定的目录。相关配置在 `UriLevel` 和 `ArgSegment` 中指定。 |`name` |
|ParamName |String |否 |当 `CapMode` 是 `name` 时，您必须指定该参数。该参数表示您要指定的查询参数。 |`myparam5` |
|UriLevel |Long |否 |当 `CapMode` 是 `uri` 时，您必须指定该参数。该参数表示您要指定的目录层级。<br><br>该参数的要求如下：<br><br><br>* 层级是非 0 的整数。<br><br>* 绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从最右边的目录开始向左计数。 |`4` |
|RewriteRule |Object |否 |表示 CDN 在视频分片 URI 中添加令牌的方式。 | |
|CapMode |String |否 |表示 CDN 如何在视频分片 URI 中添加生成的令牌。该参数有以下取值：<br><br><br>* `name`：表示将 URI 中指定的查询参数设置为令牌。相关配置在 `ParamName` 中指定。<br><br>* `uri`：表示在 URI 中指定的目录层级插入一个目录，并将该目录设置为令牌。相关配置在 `UriLevel` 中指定。 |`name` |
|ParamName |String |否 |当 `CapMode` 是 `name` 时，您必须指定该参数。该参数表示您要指定的查询参数。 |`myparam4` |
|UriLevel |Long |否 |当 `CapMode` 是 `uri` 时，您必须指定该参数。该参数表示您要指定的目录层级。<br><br>该参数的要求如下：<br><br><br>* 层级是非 0 的整数。<br><br>* 绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从最右边层级的目录开始向左计数。 |`2` |
|SignJoinSymbol |String |否 |表示拼接 `RewriteParam` 中各对象而使用的拼接符。 |`00` |
|Switch |Boolean |否 |表示是否启用扩展改写配置。该参数有以下取值：<br><br><br>* `true`：表示启用扩展改写配置。<br><br>* `false`：表示不启用扩展改写配置。<br><br><br>该参数的默认值是 `false`。 |`true` |
|ExpireTimeRule |Object |否 |表示令牌过期时间的相关设置。 | |
|Duration |Long |否 |表示令牌的有效时长（TTL），单位是秒，取值范围是 0\-315,360,000，默认值是 `0`。<br><br><br>* 令牌过期时间 = 基于 `ExpTimeCapRule` 获取的令牌时间戳 + `Duration` |`20` |
|ExpTimeCapRule |Object |否 |表示令牌时间戳的获取方式。令牌时间戳是一个 Unix 时间戳。 | |
|ArgSegment |Object |否 |表示基于 `ParamName` 或者 `UriLevel` 获取的内容是否需要被拆分，以提取某个层级的片段。该层级的片段才是您需要获取的令牌时间戳。 | |
|Level |Long |否 |表示将内容拆分为多个层级的片段后，令牌时间戳所在的层级，要求如下：<br><br><br>* 层级是非 0 的整数。<br><br>* 层级的绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从最右边的片段开始向左计数。<br><br>当 `Switch` 为 `true` 时，您必须指定该参数。 |`2` |
|SplitSymbol |String |否 |表示用于拆分内容的分隔符。<br><br>当 `Switch` 为 `true` 时，您必须指定该参数。 |`-` |
|Switch |Boolean |否 |表示获取到的内容是否需要被拆分。该参数有以下取值：<br><br><br>* `true`：表示内容需要被拆分。<br><br>* `false`：表示内容无需被拆分。<br><br><br>该参数的默认值是 `false`。 |`true` |
|CapMode |String |否 |表示令牌时间戳的来源。该参数有以下取值：<br><br><br>* `name`：表示查询参数。相关配置在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示请求路径中的一个目录。相关配置在 `UriLevel` 和 `ArgSegment` 中指定。<br><br>* `header`：表示请求中的一个头部。相关配置在 `CustomValue` 中指定。<br><br>* `cookie`：表示请求中的一个 cookie。相关配置在 `CustomValue` 中指定。 |`header` |
|CustomValue |String |否 |该参数的含义如下：<br><br><br>* 当 `CapMode` 是 `header` 时，您必须指定该参数。该参数表示您要指定的请求头。<br><br>* 当 `CapMode` 是 `cookie` 时，您必须指定该参数。该参数表示您要指定的 cookie 的 key，CDN 会获取相应的 value。 |`myheader1` |
|ParamName |String |否 |当 `ParamType` 是 `ReqHeader` 时，您必须指定该参数。该参数表示您要指定的查询参数。 |`myparm1` |
|UriLevel |Long |否 |当 `ParamType` 是 `uri` 时，您必须指定该参数。该参数表示您要指定的目录层级。<br><br>该参数的要求如下：<br><br><br>* 层级是非 0 的整数。<br><br>* 层级的绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从路径最右边的目录开始向左计数。 |`2` |
|TimeFormat |String |否 |表示令牌时间戳的格式。<br><br><br>* `octal`：表示八进制。例如 `14751410031`。<br><br>* `decimal`：表示十进制。例如 `1738936345`。<br><br>* `heximal`：表示十六进制。例如 `67a61019`。 |`heximal` |
|RewriteM3U8 |Object |否 |表示 HLS Manifest 改写的配置，也就是配置如何在 Manifest 中的视频分片 URI 中添加令牌。<br><br>如果 `SignCapRule` 下的 `CapMode` 是 `header` 或 `cookie`，您不能设置该参数。 | |
|RewriteM3U8Tag |Object |否 |表示额外的标签。对于 `Tags` 中包含的标签，CDN 会将令牌添加到这些标签下的 URL 中。参见 [该设置的示例](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn#m3u8-%E9%A2%9D%E5%A4%96%E6%A0%87%E7%AD%BE%E7%9A%84%E6%94%B9%E5%86%99%E7%A4%BA%E4%BE%8B)。 | |
|Switch |Boolean |否 |表示是否需要设置额外的标签。该参数有以下取值：<br><br><br>* `true`：表示需要设置额外的标签。<br><br>* `false`：表示无需设置额外的标签。<br><br><br>该参数的默认值是 `false`。 |`true` |
|Tags |String[] |否 |表示额外标签的列表。 |`["tag1","tag2","tag3"]` |
|Switch |Boolean |否 |表示是否需要改写 HLS Manifest。该参数有以下取值：<br><br><br>* `true`：表示需要改写 Manifest。<br><br>* `false`：表示无需改写 Manifest。<br><br><br>默认情况下，CDN 仅对 Manifest 中 `EXTINF` 标签下的视频分片 URI 添加令牌。 |`true` |
|RewriteMPD |Object |否 |表示 DASH Manifest 改写的配置，也就是配置如何在 Manifest 中的视频分片 URI 中添加令牌。<br><br>如果 `SignCapRule` 下的 `CapMode` 是 `header` 或 `cookie`，您不能设置该参数。 | |
|MpdVarExpand |Boolean |否 |表示是否要将 `SegmentTemplate` 下 URI 中的变量替换为实际值。该参数有以下取值：<br><br><br>* `true`：表示启用该配置。该配置启用后，CDN 会先将视频分片 URI 中的变量替换为实际值，然后基于包含实际值的 URI 生成令牌，最后将令牌添加到 URI 中。<br><br>* `false`：表示不启用该配置。变量名本身会作为固定字符串用于生成令牌。<br><br><br>该参数的默认值是 `false`。<br><br>该配置启用后，当前只有满足以下所有条件的变量才会被替换为实际值：<br><br><br>* 变量为 `$RepresentationID$`。<br><br>* `SegmentTemplate` 下存在至少一个 URI 符合以下条件：<br><br>   * 在该 URI 中，至少有一个 `$RepresentationID$` 出现的位置不是 URI 路径中的最后一段。<br><br>* `<SegmentTemplate ... />` 和 `<Representation .../>` 之间不能出现其他内容。<br><br><br>另外，在改写后的 DASH Manifest 中，原始的 `SegmentTemplate` 会被保留。<br><br>参见 [示例](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn#dash-mpd-%E5%8F%98%E9%87%8F%E6%89%A9%E5%B1%95-%E7%A4%BA%E4%BE%8B)。 |`true` |
|Switch |Boolean |否 |表示是否需要改写 DASH Manifest。该参数有以下取值：<br><br><br>* `true`：表示需要改写 Manifest。<br><br>* `false`：表示无需改写 Manifest。 |`true` |
|SecretKey |Object |否 |表示用于计算令牌的密钥。包含一个主密钥和一个备密钥。 | |
|BackupSecretKey |String |否 |表示备密钥，长度在 6\-40 个字符之间。 |`secondary-key-456` |
|MasterSecretKey |String |否 |表示主密钥，长度在 6\-40 个字符之间。 |`primary-key-123` |
|SignCapRule |Object |否 |表示从用户请求中获取令牌的方式。 | |
|ArgSegment |Object |否 |表示基于 `ParamName` 或者 `UriLevel` 获取的内容是否需要被拆分，以提取某个层级的片段。该层级的片段才是您需要获取的令牌。 | |
|Level |Long |否 |表示将内容拆分为多个层级的片段后，令牌所在的层级，要求如下：<br><br><br>* 层级是非 0 的整数。<br><br>* 层级的绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从最右边的片段开始向左计数。<br><br>当 `Switch` 为 `true` 时，您必须指定该参数。 |`2` |
|SplitSymbol |String |否 |表示用于拆分内容的分隔符。<br><br>当 `Switch` 为 `true` 时，您必须指定该参数。 |`//` |
|Switch |Boolean |否 |表示获取到的内容是否需要被拆分。该参数有以下取值：<br><br><br>* `true`：表示内容需要被拆分。<br><br>* `false`：表示内容无需被拆分。<br><br><br>该参数的默认值是 `false`。 |`true` |
|CapMode |String |否 |表示令牌的来源。该参数有以下取值：<br><br><br>* `name`：表示查询参数。相关配置在 `ParamName` 中指定。<br><br>* `uri`：表示请求路径中的一个目录。相关配置在 `UriLevel` 中指定。<br><br>* `header`：表示请求中的一个头部。相关配置在 `CustomValue` 中指定。<br><br>* `cookie`：表示请求中的一个 cookie。相关配置在 `CustomValue` 中指定。 |`name` |
|CustomValue |String |否 |该参数的含义如下：<br><br><br>* 当 `CapMode` 是 `header` 时，您必须指定该参数。该参数表示您要指定的请求头。<br><br>* 当 `CapMode` 是 `cookie` 时，您必须指定该参数。该参数表示您要指定的 cookie 的 key，CDN 会获取相应的 value。 |`myheader` |
|ParamName |String |否 |当 `CapMode` 是 `name` 时，您必须指定该参数。该参数表示您要指定的查询参数。 |`myparam` |
|UriLevel |Long |否 |当 `CapMode` 是 `uri` 时，您必须指定该参数。该参数表示您要指定的目录层级。<br><br>该参数的要求如下：<br><br><br>* 层级是一个非 0 的整数。<br><br>* 绝对值不能大于层级总数。<br><br><br>如果层级是负整数，表示从路径最右边的目录开始向左计数。 |`3` |
|Condition |Object |否 |表示匹配条件的配置。如果一个请求符合匹配条件，CDN 对该请求进行 URL 鉴权。 | |
|ConditionRule |Object[] |是 |表示一个匹配条件列表。列表中最多可以包含 10 个匹配条件。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求文件的扩展名。<br><br>* `directory`：表示请求路径中的某个目录。<br><br>* `path`：表示请求的完整路径，不包含查询字符串。<br><br>* `regex`：表示用于匹配完整路径的正则表达式。 |`directory` |
|Operator |String |是 |表示匹配操作符。该参数有以下取值：<br><br><br>* `match`：表示如果 `Value` 匹配了请求中的 `Object`，则该请求符合这个匹配条件。<br><br>* `not_match`：表示如果 `Value` 不匹配请求中的 `Object`，该请求就符合这个匹配条件。 |`match` |
|Type |String |是 |表示匹配对象的来源。当前，该参数值只能是 `url`，表示请求 URL。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）。<br><br><br>另外，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个文件扩展名，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个路径目录，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个完整路径，不包含查询字符串。完整路径以斜杠（/）开头。另外，每个匹配值中可以包含通配符（\*）用来表示一个或者多个任意字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果 `Object` 是 `regex`，每个匹配值表示一个正则表达式。例如 `/a{1,2}(.*)g`。 |`/chs/foods/;/us/birds/` |
|Connective |String |是 |表示匹配条件之间的关系。该参数有以下取值：<br><br><br>* `OR`：表示关系是 "或"。<br><br>* `AND`：表示关系是 "和"。<br><br><br>该参数的默认值是 `OR`。 |`OR` |
|RuleName |String |否 |表示规则列表中一条规则的名称，长度不能超过 120 个字符。规则名称可以包含汉字、字母、数字、连字符（\-）、下划线（_）和空格。一个汉字占 3 个字符。 |`Authentication rule A` |
|RewriteFormat |String |否 |表示改写后的视频分片 URI 格式。该参数有以下取值：<br><br><br>* `default`：该参数值的含义与 `absolute` 相同。<br><br>* `relative`：保持 URI 的当前格式。需要留意的是，如果 `ExpireTimeRule` 下的 `CapMode` 或者 `SignCapRule` 下的 `CapMode` 为 `uri`，则您不能设置 `RewriteFormat` 为 `relative`。<br><br>* `absolute`：如果 URI 的格式是相对路径，CDN 将格式转换成绝对路径。如果 URI 是绝对路径或者完整 URL，则保持当前格式。<br><br>* `full`：如果 URI 的格式是绝对路径或者相对路径，CDN 将格式转换成完整 URL。<br><br><br>该参数的默认值是 `default`。 |`default` |


<span id="远程鉴权"></span>
### 远程鉴权


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|RemoteAuth |Object |否 |表示 "远程鉴权" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RemoteAuthRules |Object[] |否 |表示一个鉴权规则的列表。当前，列表中只能包含一条规则。该规则包含匹配条件配置和鉴权配置。当 `Switch` 是 `true` 时，该参数为必填。 | |
|Condition |Object |是 |表示匹配条件的配置。如果一个请求满足匹配条件，CDN 对该请求执行 `RemoteAuthRuleAction` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示匹配条件列表。列表中最多可以包含 50 个匹配条件。<br><br>这些匹配条件之间的关系是 "或"，表示如果一个请求满足任意匹配条件，CDN 就对该请求执行 `RemoteAuthRuleAction` 中指定的操作。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。 |`filetype` |
|Operator |String |是 |表示匹配类型。该参数有以下取值：<br><br><br>* `match`：表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。<br><br>* `not_match`：表示如果 `Value` 不匹配请求中的 `Object`，该请求就满足这个匹配条件。<br><br><br>需要留意的是，所有匹配条件中的 `Operator` 必须相同。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>同时，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个 URL 路径，以斜杠（/）开头。每个匹配值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png;jpg` |
|RemoteAuthRuleAction |Object |是 |表示鉴权相关的配置。<br><br>当一个请求满足 `Condition` 中的匹配条件时，CDN 会将其发送至鉴权服务器进行鉴权，并基于鉴权的结果接受或者拒绝该请求。 | |
|AuthModeConfig |Object |是 |表示鉴权服务器的配置。 | |
|MasterRemoteAddr |String |是 |表示鉴权服务器的主地址，长度不能超过 100 个字符。主地址的格式是 `<scheme>://<domain>:<port>` 或 `<scheme>://<ip>:<port>`，其中：<br><br><br>* `<scheme>` 是 `http` 或者 `https`。<br><br>* `<domain>` 不能是 `localhost`。<br><br>* `<ip>` 不能是 `127.0.0.1`。<br><br>* `<port>` 是可选的。 |`https://primary.example.com` |
|PathType |String |是 |表示鉴权请求的路径。鉴权地址和请求路径组成了完整的鉴权 URL。CDN 会把用户的请求转发到该鉴权 URL。该参数有以下取值：<br><br><br>* `constant`：表示鉴权请求中的路径与用户请求中的路径相同。<br><br>* `variable`：表示您需要在 `pathValue` 参数中指定一个鉴权请求中的路径。 |`constant` |
|RequestMethod |String |是 |表示在发送鉴权请求时，CDN 所使用的请求方法。该参数有以下取值：<br><br><br>* `default`：表示鉴权请求所使用的方法与用户的请求相同。<br><br>* `get`：表示鉴权请求使用 GET 方法。<br><br>* `post`：表示鉴权请求使用 POST方法。<br><br>* `head`：表示鉴权请求使用 HEAD 方法。 |`get` |
|BackupRemoteAddr |String |否 |表示鉴权服务器的备地址。地址格式和要求与主地址相同。 |`https://secondary.example.com` |
|PathValue |String |否 |表示一个鉴权请求的路径，长度不能超过 100 个字符。路径必须以斜杠（/）开头，不能包含以下字符：<br><br><br>* 双斜杠（//）、百分号（%）、美元符号（$）、空格、问号（?） |`/auth` |
|AuthResponseConfig |Object |是 |CDN 需要对鉴权服务器返回的鉴权状态码进行处理。该参数表示相关的配置。 | |
|CacheAction |Object |否 |CDN 可以缓存鉴权状态码。该参数表示相关的配置。 | |
|Action |String |是 |表示 CDN 是否缓存鉴权状态码。该参数有以下取值：<br><br><br>* `nocache`：表示 CDN 不缓存鉴权状态码。<br><br>* `cache`：CDN 缓存鉴权状态码。 |`nocache` |
|Ttl |Long |是 |表示鉴权状态码的缓存时间。单位是秒。取值范围是 1\-86400。86400秒表示 24小时。 |`5` |
|CacheKey |String[] |否 |缓存 key 指定了用于区分不同请求 URI 的查询参数。每个参数都必须以 `$` 开头。您也可以指定 [变量字段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-remote-authentication_1-cn#variables)中的参数。 |`[$URI,$host]` |
|ResponseAction |Object |否 |表示鉴权失败时，CDN 如何响应用户。 | |
|StatusCode |String |否 |表示鉴权失败时，CDN 响应用户的状态码。您可以指定范围在 400\-499 中的任意一个状态码。该参数的默认值是 `403`。 |`403` |
|StatusCodeAction |Object |否 |表示 CDN 对鉴权状态码的处理方式。 | |
|DefaultAction |String |是 |表示如果鉴权状态码既不是 `FailCode`，又不是 `SuccessCode` 时，CDN 处理鉴权请求的方式。该参数有以下取值：<br><br><br>* `reject`：表示 CDN 认为鉴权失败。<br><br>* `pass`：表示 CDN 认为鉴权成功。 |`pass` |
|FailCode |String |是 |表示鉴权失败时的鉴权状态码。您可以指定范围在 400\-499 中的一个或者多个状态码。多个状态码使用英文分号（;）分隔。您也可以指定 4xx 表示 400\-499 中的任意一个状态码。 |`403` |
|SuccessCode |String |是 |表示鉴权成功时的鉴权状态码。您可以指定范围在 200\-299 中的一个或者多个状态码。多个状态码使用英文分号（;）分隔。您也可以指定 2xx 表示 200\-299 中的任意一个状态码。 |`200` |
|TimeOutAction |Object |否 |表示鉴权超时后，CDN 如何处理鉴权请求。 | |
|Action |String |是 |表示鉴权超时后，CDN 处理鉴权请求的策略。该参数有以下取值：<br><br><br>* `reject`：表示 CDN 认为鉴权失败。<br><br>* `pass`：表示 CDN 认为鉴权成功。 |`reject` |
|Time |Long |是 |表示鉴权超时的时间，单位是毫秒，取值范围是 200 \- 3600。 |`200` |
|QueryStringRules |Object |是 |表示鉴权请求的参数设置。 | |
|QueryStringComponents |Object |否 |表示鉴权请求参数的设置策略。 | |
|Action |String |否 |表示鉴权请求是否包含用户请求 URL 中的查询参数。该参数有以下取值：<br><br><br>* `exclude`：表示鉴权请求不包含任何查询参数。<br><br>* `include`：表示鉴权请求包含所有查询参数。<br><br>* `includePart`：表示鉴权请求包含指定的查询参数。 |`exclude` |
|Value |String |否 |表示 `Action` 参数所对应的参数值，长度不能超过1,024 个字符。该参数有以下取值：<br><br><br>* 如果 `Action` 是 `exclude` 或 `include`，`Value` 必须是 `*`。<br><br>* 如果 `Action` 是 `includePart`，您需要在 `Value` 参数中指定用户请求 URL 中的一个或者多个查询参数，多个查询参数使用英文分号（;）分隔。您不能指定 `*`。查询参数是区分大小写的，不能包含双引号（"），也不能包含空格。<br><br><br>该参数的默认值是 `*`。 |`*` |
|QueryStringInstances |Object[] |否 |表示鉴权请求中额外的参数设置。您最多可以设置 50 个参数。 | |
|Action |String |否 |表示如何设置鉴权请求参数。当前您只能设置 `Action` 为 `set`。`set` 表示设置参数。您需要在 `Key` 中指定您需要设置的鉴权请求参数。如果您指定的鉴权请求参数不存在，CDN 会在鉴权请求中添加该参数。如果您指定的鉴权请求参数已存在，CDN 会使用 `Value` 的值作为该鉴权请求参数的值。 |`set` |
|Key |String |否 |表示您需要设置的鉴权请求参数，长度不能超过 1,024 个字符，不能包含双引号（"），也不能包含空格。 |`sign` |
|Value |String |否 |表示鉴权请求参数的值，长度不能超过 1,024 个字符，并且区分大小写。`Value`有以下取值：<br><br><br>* 当 `ValueType` 是 `constant` 时，表示鉴权请求参数的值是一个常量。您需要指定该常量值。常量值不能以美元符号（$）开头，也不能包含双引号（"）。<br><br>* 当 `ValueType` 是 `variable` 时，表示鉴权请求参数的值来自一个变量。您可以指定该[变量列表](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-remote-authentication_1-cn#variables)中的变量。<br><br>* 当 `ValueType` 是 `customize` 时，表示鉴权请求参数的值是列表中的变量与固定字符串拼接后的字符串。在拼接的字符串中，变量使用 `${变量名}` 表示。示例值：`bind${request_uri}to${local_ip}done` |`1235565` |
|ValueType |String |否 |表示您在 `Key` 中设置的鉴权请求参数的类型。`ValueType` 有以下取值：<br><br><br>* `constant`：表示鉴权请求参数是一个常量。此时，您需要在 `Value` 中指定该常量的值。<br><br>* `variable`：表示鉴权请求参数的值来自一个变量。参见 `Value` 的说明。<br><br>* `customize`：表示鉴权请求参数的值是一个变量与固定字符串拼接后的字符串。 |`variable` |
|RequestHeaderRules |Object |是 |表示鉴权请求头的设置。您最多可以设置 50 个请求头。 | |
|RequestHeaderComponents |Object |否 |表示鉴权请求头的设置策略。 | |
|Action |String |是 |表示鉴权请求头是否包含用户请求头。该参数有以下取值：<br><br><br>* `exclude`：表示鉴权请求头中不包含任何用户请求头。<br><br>* `include`：表示鉴权请求头中包含所有用户请求头。<br><br>* `includePart`：表示鉴权请求头包含指定的用户请求头。 |`exclude` |
|Value |String |否 |表示 `Action` 参数所对应的参数值，长度不能超过 1,024 个字符。该参数有以下说明：<br><br><br>* 如果 `Action` 是 `exclude` 或 `include`，`Value` 必须是 `*`。<br><br>* 如果 `Action` 是 `includePart`，`Value` 参数的取值是用户请求中的一个或者多个头部。多个头部使用英文分号（;）分隔。其取值不能只是 `*`，不能包含以下字符：<br><br>   * 下划线（_）、空格、双引号（"）<br><br><br>该参数的默认值是 `*`。 |`*` |
|RequestHeaderInstances |Object[] |否 |表示一组鉴权请求头的设置。<br><br>需要留意的是，在 CDN 发起鉴权请求时，请求中可能已经包含了以下头部：<br><br><br>* `X-Forwarded-Protocol`，`X-Forwarded-Proto`，`X-Client-Scheme`：这三个头部都表示用户请求所使用协议，没有区别。<br><br>* `X-Real-IP`：表示用户真实的 IP 地址。该头部的值不会受代理服务器的影响。<br><br>* `X-Forwarded-For`：表示用户的 IP 地址。如果用户的请求经过了代理服务器，该头部的值会变成代理服务器的 IP 地址。<br><br><br>不建议您在该参数中对这些头部进行设置。如果您设置了这些头部，这些头部的原始值会被覆盖。 | |
|Action |String |是 |表示如何设置鉴权请求头。当前您只能设置该参数值为 `set`。`set` 表示设置请求头。此时，您需要在 `Key` 中指定您需要设置的请求头。如果您设置的请求头不存在，CDN 会在鉴权请求中添加该请求头。如果您设置的请求头已存在，CDN 会使用 `Value` 的值作为该请求头的值。 |`set` |
|Key |String |是 |表示您需要设置的请求头。请求头不能是 `host`，长度不能超过 1,024 个字符，并且不区分大小写。<br><br>请求头不能包含以下字符：<br><br><br>* 下划线（_）、空格、双引号（"） |`x-test-header` |
|ValueType |String |是 |表示请求头的类型。该参数有以下取值：<br><br><br>* `constant`：表示请求头的值是一个常量。您需要在 `Value` 参数中指定该常量的值。<br><br>* `variable`：表示请求头的值来自一个变量。参见 `Value` 的说明。<br><br>* `customize`：表示请求头的值是一个变量与固定字符串拼接后的字符串。 |`variable` |
|Value |String |否 |表示请求头的值。该参数有以下取值：<br><br><br>* 当 `ValueType` 是 `constant` 时，您需要指定一个常量值。该常量值的长度不能超过 1,024 个字符，并且区分大小写。同时，该常量值不能以美元符号（$）开头，不能包含双引号（"）。<br><br>* 当 `ValueType` 是 `variable` 时，表示请求头的值来自一个变量。您可以指定该[变量列表](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-remote-authentication_1-cn#variables)中的变量。<br><br>* 当 `ValueType` 是 `customize` 时，表示请求头的值是列表中的变量与固定字符串拼接后的字符串。在拼接的字符串中，变量使用 `${变量名}` 表示。示例值：`my${host}is${referer}great` |`1234fdf` |
|RequestHost |String |否 |表示鉴权请求中 HOST 头部的值。该参数的默认值是 `default`，表示 HOST 头部的值与您的域名相同。 |`www.example.com` |


<span id="下载限速"></span>
### 下载限速


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|DownloadSpeedLimit |Object |否 |表示 "下载限速" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|DownloadSpeedLimitRules |Object[] |否 |表示一个限速规则的列表。当 `Switch` 是 `true` 时，该参数为必填。该参数的其他说明如下：<br><br><br>* 每条规则包含匹配条件配置和限速配置。<br><br>* 列表中最多可以包含 50 条规则。<br><br>* 列表中规则的出现顺序表示规则的优先级排序。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|DownloadSpeedLimitAction |Object |是 |表示限速配置。 | |
|SpeedLimitRate |Long |是 |表示 CDN 在响应单个请求时的最大数据传输速度，单位是 `B/S`，使用的进制是 `1,024`。该参数的取值范围是 1\-1,073,741,824,000,000。`1,073,741,824,000,000` 是 1,000,000 Gbps。 |`500000` |
|SpeedLimitRateAfter |Long |否 |表示一个初始数据量，单位是 `bytes`，使用的进制是 `1,024`。该参数的取值范围是 0\-1,073,741,824,000,000。<br><br>当 CDN 对一个请求开始传输数据时，在传输的数据量达到该初始数据量前，该限速规则不会启用。<br><br>如果该参数值是 `0`，表示在 CDN 对一个请求开始传输第一个字节时，该限速规则就启用了。 |`1000` |
|SpeedLimitTime |Object |否 |表示限速规则启用的日期和时间段。 | |
|DayWeek |String |是 |表示该限速规则启用的日期，有以下取值：`monday`，`tuesday`，`wednesday`，`thursday`，`friday`，`saturday`，`sunday`，`unlimited`。`unlimited` 表示每天。<br><br>您可以指定一个或多个日期，多个日期之间使用分号（;）分隔。 |`monday;friday` |
|BeginTime |String |否 |表示该限速规则启用的开始时间，格式是 `mm:ss`。<br><br>如果 `DayWeek` 是 `unlimited`, `BeginTime` 会被设置为 `00:00`，您无法更改。 |`05:08` |
|EndTime |String |否 |表示该限速规则启用的结束时间，格式是 `mm:ss`。<br><br>如果 `DayWeek` 是 `unlimited`, `EndTime` 会被设置为 `23:59`，您无法更改。 |`16:48` |
|Condition |Object |否 |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `DownloadSpeedLimitAction` 中指定的操作。<br><br>如果不指定该参数，CDN 对所有请求执行 `DownloadSpeedLimitAction` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示匹配条件列表。当前，列表中只能包含一个匹配条件。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示完整的请求路径。<br><br>* `unlimited`：表示域名下的所有文件。<br><br>* `regex`：表示完整的请求路径，通过正则表达式匹配。 |`filetype` |
|Operator |String |是 |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>同时，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个 URL 路径，以斜杠（/）开头。每个匹配值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果 `Object` 是 `unlimited`，该参数值必须为空（""）。<br><br>* 如果 `Object` 是 `regex`，表示一个或者多个正则表达式。多个正则表达式使用分号（;）分隔。例如 `/a/*.jpg`。 |`/www/img/f1/;/www/doc/` |


<span id="ip-访问限频"></span>
### IP 访问限频


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|IpFreqLimit |Object |否 |表示 "IP 访问限频" 特性的配置模块。该特性默认为禁用。要使用该特性，[提交工单](https://console.byteplus.com/workorder/create)。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|IpFreqLimitRules |Object[] |否 |表示一组限频的规则。当 `Switch` 为 `true` 时，该参数为必填。当前您只能指定一条规则。 | |
|IpFreqLimitAction |Object |是 |表示限频操作的配置。 | |
|Action |String |是 |表示当一个 IP 地址的 QPS 达到 `FreqLimitRate` 时，CDN 的行为。当前，您只能指定该参数值为 `deny`，表示 CDN 拒绝来自该 IP 地址的新请求。 |`deny` |
|FreqLimitRate |Long |是 |指定 IP 的 QPS 阈值。该参数的取值范围是 1\-1,000,000。 |`5000` |
|StatusCode |String |是 |表示当 CDN 拒绝来自某个 IP 地址的请求时， CDN 的响应状态码。当前，该参数值只能为 `403`。 |`403` |


<span id="缓存配置"></span>
## 缓存配置

<span id="缓存键值"></span>
### 缓存键值


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|CacheKey |Object[] |否 |表示 "缓存键值" 特性的配置。在该配置中，您可以创建一个规则列表，说明如下：<br><br><br>* 每条规则包含匹配条件配置和操作配置。<br><br>* 列表中最多可以包含 50 条规则。<br><br>* 规则在列表中出现的顺序表示规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。<br><br><br>您**必须**在规则列表的最后添加以下默认规则。该默认规则用于匹配任何未能匹配其他规则的用户请求。在默认规则中，您可以调整 `CacheKeyAction` 的设置，但不能调整 `Condition` 的配置。<br><br>```json```<br>```{```<br>```            "CacheKeyAction": {```<br>```                "CacheKeyComponents": [```<br>```                    {```<br>```                        "Action": "include",```<br>```                        "IgnoreCase": true,```<br>```                        "Object": "queryString",```<br>```                        "Subobject": "*"```<br>```                    }```<br>```                ]```<br>```            },```<br>```            "Condition": {```<br>```                "ConditionRule": [```<br>```                    {```<br>```                        "Name": "",```<br>```                        "Object": "directory",```<br>```                        "Operator": "match",```<br>```                        "Type": "url",```<br>```                        "Value": "/"```<br>```                    }```<br>```                ]```<br>```            }```<br>```        }```<br> | |
|CacheKeyAction |Object |是 |当一个请求满足 `Condition` 中的匹配条件时，CDN 会为请求文件设置缓存键。该参数表示缓存键的配置。 | |
|CacheKeyComponents |Object[] |是 |缓存键是由请求中的 host、路径和查询字符串等部分组成。该参数表示其中各组成部分的配置。当前，您只能对缓存键中包含的查询字符串进行配置。 | |
|Action |String |是 |表示 CDN 如何在请求文件的缓存键中设置查询字符串。该参数有以下取值：<br><br><br>* `exclude`：表示缓存键不包含请求中的任何查询参数。<br><br>* `include`：表示缓存键包含请求中所有的查询参数。缓存键中查询参数的顺序与请求 URL 中的顺序相同。<br><br>* `includePart`：表示缓存键仅包含 `Subobject` 中指定的查询参数。CDN 对包含在缓存键中的查询参数按字母顺序排序后生成缓存键。<br><br>* `excludePart`：表示缓存键包含请求中除了 `Subobject` 中指定的查询参数之外的所有查询参数。CDN 对包含在缓存键中的查询参数按字母顺序排序后生成缓存键。<br><br><br>说明<br><br>缓存键中查询参数的顺序影响缓存匹配。如果请求 URL 中查询参数的顺序与缓存键中的查询参数的顺序不同，则 CDN 判定请求未命中缓存。 |`excludePart` |
|IgnoreCase |Boolean |是 |表示 `Subobject` 是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。<br><br><br>该参数的默认值为 `false`，并且仅当 `Action` 是 `includePart` 或 `excluePart` 时有效。 |`true` |
|Object |String |是 |表示缓存键中的一个组成部分。当前该参数值只能是 `querystring`，表示查询字符串。 |`queryString` |
|Subobject |String |是 |该参数对应于 `Action`，表示 CDN 在缓存键中包含的具体查询参数。该参数的说明如下：<br><br><br>* 如果 `Action` 是 `include` 或者 `exclude`，`Subobject` 必须是 `*`，表示请求中的全部查询参数。<br><br>* 如果 `Action` 是 `includePart` 或者 `excludePart`，表示需要保留或者不保留的查询参数。多个查询参数之间使用分号（;）分隔。您指定的查询参数不能是 `*`，也不能包含双斜杠（//）、百分号（%）、空格。 |`sign;testParams` |
|Condition |Object |是 |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `CacheKeyAction` 中指定的操作。<br><br>`CacheKey` 中最后一条规则的 `Condition` 必须是以下设置。参见 请求示例。<br><br>```json```<br>```"Condition": {```<br>```  "ConditionRule": [```<br>```    {```<br>```      "Object": "directory",```<br>```      "Operator": "match",```<br>```      "Type": "url",```<br>```      "Value": "/"```<br>```    }```<br>```  ]```<br>```}```<br> | |
|ConditionRule |Object[] |是 |表示匹配条件列表。列表中只能包含一个匹配条件。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。<br><br>* `regex`：表示请求 URL 中的路径，通过正则表达式匹配。 |`directory` |
|Operator |String |是 |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>同时，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个 URL 路径，以斜杠（/）开头。每个匹配值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |
|IgnoreCase |Boolean |否 |表示 `Value` 是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。<br><br><br>该参数的默认值为 `false`。 |`true` |


<span id="节点缓存规则"></span>
### 节点缓存规则


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Cache |Object[] |否 |表示 "缓存规则" 特性的配置。该特性默认为禁用，表示不创建自定义规则。<br><br><br>* 列表中最多可以包含 50 条规则。<br><br>* 列表中规则的顺序定义了规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。<br><br><br>CDN 中有一条 [默认缓存规则](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-caching-rules-cn#%E9%BB%98%E8%AE%A4%E7%BC%93%E5%AD%98%E8%A7%84%E5%88%99)，用于匹配任何未能匹配其他规则的用户请求。该默认规则始终生效，并且优先级最低。您**无需**在配置该特性时指定该默认规则。 | |
|CacheAction |Object |是 |当一个请求满足 `Condition` 中的匹配条件时，CDN 会对请求文件执行指定的操作。该参数定义了该操作相关的配置。 | |
|Action |String |是 |表示 CDN 执行的操作。当前该参数值只能是 `cache`，表示缓存请求的文件。`DefaultPolicy` 中指定了如何缓存请求的文件。 |`cache` |
|IgnoreCase |Boolean |是 |表示 `Value` 是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感<br><br><br>该参数的默认值为 `false`。 |`true` |
|Ttl |Long |是 |表示请求文件的缓存时长，单位为`秒`，范围为 `0-315,360,000`。`315,360,000` 是 10 年。<br><br>如果该参数值为 `0`，CDN 在收到匹配规则的请求时，会按以下方式处理：<br><br><br>* 如果文件尚未被缓存，CDN 不会缓存该文件。<br><br>* 如果文件已被缓存，该文件会立即过期，后续对该文件的请求将触发 [回源校验](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-caching-rules-cn#%E5%9B%9E%E6%BA%90%E6%A0%A1%E9%AA%8C)。这种情况通常发生在您修改缓存规则，将一个已缓存文件的缓存时长从非零值改为 `0` 时。 |`100` |
|DefaultPolicy |String |否 |表示 CDN 对请求文件的缓存行为。该参数有以下取值：<br><br><br>* `force_cache`：对应 CDN 控制台中的 **CDN缓存** + **强制缓存（开）**  的配置组合。<br><br>* `default`：对应 CDN 控制台中的 **CDN缓存** + **强制缓存（关）**  的配置组合。<br><br>* `origin_first`：对应 CDN 控制台中的 **遵循源站** + **补充缓存（开）**  的配置组合。<br><br>* `origin_first_Replenish`：对应 CDN 控制台中的 **遵循源站** + **补充缓存（关）**  的配置组合。<br><br>* `no_cache`：对应 CDN 控制台中的 **不缓存** 配置。<br><br><br>该参数的默认值是 `default`。关于这些缓存策略的描述，参见 [缓存规则](https://docs.byteplus.com/zh-CN/byteplus-cdn/docs/caching-rules)。 |`force_cache` |
|SetCookieNoCache |Boolean |否 |表示是否缓存包含 `Set-Cookie` 头部的源站响应。该参数有以下取值：<br><br><br>* `true`：表示 CDN 会缓存这类响应。<br><br>* `false`：表示 CDN 不会缓存这类响应。<br><br><br>该参数的默认值是 `false`。<br><br>说明<br><br>如果 `DefaultPolicy` 为 `force_cache`，`SetCookieNoCache` 不生效。 |`true` |
|Condition |Object |是 |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `CacheAction` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示匹配条件列表。当前，列表中只能包含一个匹配条件。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。<br><br>* `regex`：表示请求 URL 中的路径，通过正则表达式匹配。 |`directory` |
|Operator |String |是 |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>同时，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个 URL 路径，以斜杠（/）开头。每个匹配值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |


<span id="状态码缓存规则"></span>
### 状态码缓存规则


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|NegativeCache |Object[] |否 |表示 "状态码缓存" 特性的配置。在该配置中，您可以创建一个规则列表，说明如下：<br><br><br>* 每条规则包含过匹配条件配置和操作配置。<br><br>* 列表中最多可以包含 50 条规则。<br><br>* 规则在列表中出现的顺序表示规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|NegativeCacheRule |Object |是 |当一个请求满足 `Condition` 中的匹配条件时，CDN 会对请求文件执行指定的操作。该参数定义了该操作相关的配置。 | |
|Action |String |是 |表示 CDN 执行的操作。当前该参数值只能是 `cache`，表示缓存源站的响应状态码。 |`cache` |
|StatusCode |String |是 |指定一个需要缓存的状态码。状态码的范围是 `400-599`。您也可以指定 `4xx` 或者 `5xx`。`4xx` 表示 400 到 499 之间的所有状态码。`5xx` 表示 500 到 599 之间的所有状态码。 |`404` |
|Ttl |Long |是 |表示状态码的缓存时间。单位是`秒`。时间的范围是 `1-315,360,000`。`315,360,000` 表示 10 年。 |`100` |
|IgnoreCase |Boolean |否 |表示 `Value` 是否是大小写敏感的。<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。<br><br><br>该参数的默认值为 `false`。 |`true` |
|Condition |Object |否 |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `NegativeCacheRule` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示匹配条件列表。当前，列表中只能包含一个匹配条件。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。 |`directory` |
|Operator |String |是 |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>同时，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个 URL 路径，以斜杠（/）开头。每个匹配值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |


<span id="浏览器缓存规则"></span>
### 浏览器缓存规则


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|BrowserCache |Object[] |否 |表示 "浏览器缓存" 特性的配置。在该配置中，您可以创建一个规则列表，说明如下：<br><br><br>* 每条规则包含匹配条件配置和操作配置。<br><br>* 列表中最多可以包含 50 条规则。<br><br>* 规则在列表中出现的顺序表示规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|CacheAction |Object |是 |当一个请求满足 `Condition` 中的匹配条件时，CDN 会对请求文件执行指定的操作。该参数定义了该操作相关的配置。 | |
|Action |String |是 |表示浏览器需要执行的操作。当前该参数值只能是 `cache`，表示缓存请求的文件。`DefaultPolicy` 中指定了如何缓存请求的文件。 |`cache` |
|IgnoreCase |Boolean |是 |表示 `Value` 是否是大小写敏感的。<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。<br><br><br>该参数的默认值为 `false`。 |`true` |
|Ttl |Long |是 |表示浏览器需要缓存请求文件的时长，单位是秒。CDN 会在响应头中包含 `Cache-Control: max-age` 头部，头部值就是该参数值。 |`100` |
|DefaultPolicy |String |否 |表示浏览器该如何缓存请求的文件。该参数有以下取值：<br><br><br>* `cache`：表示需要缓存请求的文件。<br><br>* `origin_first`：表示遵循来自源站的缓存策略。该策略会包含在 CDN 的响应中。<br><br>* `no_cache`：表示不需要缓存请求的文件。<br><br><br>关于浏览器缓存策略的详细信息，参见 [浏览器缓存策略](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-browser-caching-cn)。 |`cache` |
|SetCookieNoCache |Boolean |否 |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |是 |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `CacheAction` 中指定的操作。 | |
|ConditionRule |Object[] |是 |表示匹配条件列表。当前，列表中只能包含一个匹配条件。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。<br><br>* `regex`：表示请求 URL 中的路径，通过正则表达式匹配。 |`directory` |
|Operator |String |是 |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>同时，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个 URL 路径，以斜杠（/）开头。每个匹配值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |


<span id="http-响应头设置"></span>
### HTTP 响应头设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ResponseHeader |Object[] |否 |表示 "HTTP 响应头" 特性的配置。 | |
|ResponseHeaderAction |Object |是 |表示 CDN 在响应用户请求的时候，对响应头的操作。 | |
|ResponseHeaderInstances |Object[] |是 |表示一个响应头的配置规则列表。每个规则都包含一个头部的相关操作设置。您最多可以添加 50 条规则。 | |
|Action |String |是 |指定对响应头的操作。该参数有以下取值：<br><br><br>* `set`：表示设置一个头部。设置操作包括添加与修改。如果源站响应中已包含该头部，该头部的值会被覆盖。如果源站响应中没有包含该头部，该头部会被添加。<br><br>* `delete`，表示删除一个头部。 |`set` |
|Key |String |是 |指定一个头部的名称。名称不能超过 1,024个字符，不区分大小写，不能包含以下字符：<br><br><br>* 下划线（_）、空格、双引号（"）<br><br><br>同时，头部名称不能使用这些 [特定的名称](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cdn-response-headers-cn#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)。 |`Content-Disposition` |
|ValueType |String |是 |指定 `Key` 的取值类型。该参数仅当 `Action` 是 `set` 的时候才有效。如果 `Action` 不是 `set`，该参数无效。该参数有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一个字符串。<br><br>* `variable`：表示 `Key` 的值来自一个变量。<br><br>* `customize`：表示 `Key` 的值是一个变量与字符串拼接后的字符串。 |`constant` |
|AccessOriginControl |Boolean |否 |表示在 CDN 响应用户请求时，是否校验请求中的 Origin 头部。<br><br>该参数有以下取值：<br><br><br>* `true`：表示 CDN 会校验 Origin 头部。如果校验成功，CDN 会在响应中包含 Access\-Control\-Allow\-Origin 头部。头部值与 Origin 头部值相同。如果校验失败，响应中不会包含 Access\-Control\-Allow\-Origin 头部。<br><br>* `false`：表示 CDN 不会校验 Origin 头部。在响应中，CDN 会包含 Access\-Control\-Allow\-Origin 头部。头部值是您配置的 Access\-Control\-Allow\-Origin 的内容。<br><br><br>该参数的默认值是 `false`。<br><br>该参数仅在以下条件都满足的情况下有效：<br><br><br>* `Action` 是 `set`。<br><br>* `Key` 是 `Access-Control-Allow-Origin`。<br><br>* `ValueType` 是 `constant`。 | |
|Value |String |否 |表示 `Key` 的值。该参数仅当 `Action` 是 `set` 的时候才有效。如果 `Action` 不是 `set`，该参数无效。当 `ValueType` 是 `constant` 时，您需要指定一个字符串作为头部的值。头部值的长度不能超过 1,024 个字符，不能包含美元符号（$）。<br><br>当 `ValueType` 是 `variable` 时，`Key` 的值可以是来自 [该列表中的某个变量](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cdn-response-headers-cn#%E5%8F%98%E9%87%8F%E5%88%97%E8%A1%A8)。除了名称包含下划线的变量，列表中的任何一个变量都可以作为 `Key`，并赋予一个字符串来替换其已有的值。也就是说，当您使用任意这些名称不包含下划线的变量作为 `Key` 时，其值是可以被覆盖的。<br><br>当 `ValueType` 是 `customize` 时，表示 `Key` 的值是列表中的变量与字符串拼接后的一个字符串。在拼接的字符串中，变量使用 `${变量名}` 表示。示例值：`${remote_addr}aaa${host}ccc` |`attachment;filename=FileName.xls` |


<span id="自定义错误页面"></span>
### 自定义错误页面


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|CustomErrorPage |Object |否 |表示 "自定义错误页面" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|ErrorPageRule |Object[] |否 |表示一个配置规则的集合。您最多可以添加 50 条规则。 | |
|ErrorPageAction |Object |是 |表示规则的相关配置。 | |
|Action |String |否 |表示实际的操作。当前您只能指定该参数值为 `redirect`。表示对客户端请求进行重定向。 |`redirect` |
|RedirectCode |String |是 |表示重定向的响应状态码。您可以根据需求选择合适的状态码。该参数的取值有 `301`、`302`、`303`、`307`、`308`。<br><br>需要留意的是：<br><br><br>* 对于 301 和 302，如果原请求使用的方法不是 GET，那么客户端向新的URL发送请求时，新请求使用的方法可能变成 GET。<br><br>* 对于 303，新请求使用的方法是 GET。<br><br>* 对于 307 和 308，新请求使用的方法与原请求相同，不会被改变。 |`302` |
|RedirectUrl |String |是 |表示跳转的目标地址，长度不能超过 1,024 个字符。地址必须包含协议，域名以及路径，并且符合 URL 的规范。 |`http://www.test.com/friendlyurl.html` |
|StatusCode |String |是 |表示一个状态码，取值范围是 400\-599。您可以输入 4xx 或者 5xx。4xx 表示 400\-499 之间的所有状态码。5xx 表示 500\-599 之间的所有状态码。 |`4xx` |


<span id="multi-range"></span>
### Multi Range


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|MultiRange |Object |否 |表示 "多重范围（Multi\-range)" 特性的配置。 | |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。该特性启用后，CDN 允许指定了多重范围的 Range 请求。<br><br>* `false`：表示不启用该特性。如果收到一个指定了多重范围的 Range 请求，CDN 会拒绝该请求并返回 416 响应状态码。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="离线缓存"></span>
### 离线缓存


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OfflineCache |Object |否 |表示 "离线缓存" 特性的配置。要使用该功能，请 [提交工单](https://console.byteplus.com/workorder/create)。 | |
|Object |String |否 |表示该特性的触发条件，该参数有以下取值：<br><br><br>* `request_error`：表示回源请求异常。当回源请求出现异常时，没有获得源站响应。<br><br>* `error_code`：表示源站的响应状态码是 5xx。<br><br>* `request_error,error_code`：表示以上两个条件都包含。 |`request_error` |
|StatusCode |String |否 |表示一个或者多个响应状态码，范围是 500\-599。多个状态码之间使用分号（;）分隔。您也可以输入 `5xx`，表示任意以数字 5 开头的状态码。<br><br>当 `Object` 是 `error_code` 或者 `request_error,error_code` 时，该参数才有效。 |`508` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |


<span id="回源配置"></span>
## 回源配置

<span id="range-回源设置"></span>
### Range 回源设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginRange |Boolean |否 |表示 "Range 回源" 特性的配置。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。请求分片大小默认是 1 MB。<br><br>说明<br><br>如果 `Range` 结构体中 `Switch` 为 `true`，则该特性为启用，即使 `OriginRange` 为 `false`。 |`true` |
|Range |Object |否 |表示分片大小的设置。 | |
|RangeSize |Long |否 |表示分片的大小。<br><br><br>* 如果 `Unit` 是 `MB`，该参数的取值范围是 1\-40。<br><br>* 如果 `Unit` 是 `KB`，该参数值只能是 `512`。<br><br><br>该参数的默认值是 `1`。 |`512` |
|Switch |Boolean |否 |表示是否启用该设置。该参数有以下取值：<br><br><br>* `true`：表示启用该设置。<br><br>* `false`：表示禁用该设置。<br><br><br>该参数的默认值是 `false`。 |`true` |
|Unit |String |否 |表示 `RangeSize` 的单位。该参数有以下取值：<br><br><br>* `KB`<br><br>* `MB`<br><br><br>该参数的默认值是 `MB`。 |`KB` |


<span id="回源超时时间设置"></span>
### 回源超时时间设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Timeout |Object |否 |表示 "回源请求超时" 特性的配置。 | |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。此时，TCP 请求和 HTTP 请求的超时时间使用默认值，分别是 2 秒和 60 秒。<br><br><br>该参数的默认值是 `false`。 |`true` |
|TimeoutRules |Object[] |否 |表示一组超时时间的配置。当前您只能指定一个配置。当 `Switch` 是 `true` 时，该参数为必填。 | |
|TimeoutAction |Object |否 |表示超时时间的配置。 | |
|HttpTimeout |Long |否 |表示 CDN 节点收到源站返回的首个响应字节后，持续未收到后续响应正文数据的最长等待时间，单位是秒，取值范围是 1\-900。 |`60` |
|TcpTimeout |Long |否 |表示 CDN 节点向源站建立 TCP 连接的最长等待时间，单位是秒，取值范围是 2\-60。 |`2` |
|HttpFirstByteTimeout |Long |否 |表示 CDN 节点向源站发送 HTTP 请求后，等待源站返回首个响应字节的最长时间，单位是秒，取值范围是 1\-900。 |`90` |


<span id="回源重试设置"></span>
### 回源重试设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginRetry |Object |否 |表示 "回源重试设置" 特性的配置模块。要使用该功能，请 [提交工单](https://console.byteplus.com/workorder/create)。 | |
|StatusCode |String |否 |表示范围在 400\-599 之间的一个或者多个状态码。多个状态码之间使用分号（;）分隔。您可以输入 `4xx` 或者 5xx，表示所有以数字 4 或 数字 5 开头的状态码。 |`404;408;5xx` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`false` |


<span id="回源重定向跟随"></span>
### 回源重定向跟随


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|FollowRedirect |Boolean |否 |表示 "回源重定向跟随" 特性的配置。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="回源-http-请求头设置"></span>
### 回源 HTTP 请求头设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|RequestHeader |Object[] |否 |表示 "回源 HTTP 请求头" 特性的配置。 | |
|RequestHeaderAction |Object |是 |表示一个请求头的配置规则列表。每个规则都包含一个头部的相关操作设置。您最多可以添加 50 条规则。 | |
|RequestHeaderInstances |Object[] |是 |表示一个请求头的配置规则列表。每个规则都包含一个头部的相关操作设置。您最多可以添加 50 条规则。 | |
|Action |String |是 |指定对请求头的操作。该参数有以下取值：<br><br><br>* `set`：表示设置一个头部。设置操作包括添加与修改。如果请求中已包含该头部，该头部的值会被覆盖。如果请求中没有包含该头部，该头部会被添加。<br><br>* `delete`，表示删除一个头部。 |`set` |
|Key |String |是 |指定一个头部的名称。名称的长度不能超过 1,024 个字符，不区分大小写。同时，名称不能包含以下字符：<br><br><br>* 下划线（_）、空格、双引号（"）<br><br><br>另外，头部名称不能使用这些 [特定的名称](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-request-headers-cn#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)。 |`Cdn-provider` |
|ValueType |String |是 |指定 `Key` 的取值类型。该参数仅当 `Action` 是 `set` 的时候才有效。如果 `Action` 不是 `set`，该参数无效。该参数有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一个固定字符串。<br><br>* `variable`：表示 `Key` 的值来自一个变量。<br><br>* `customize`：表示 `Key` 的值是变量与固定字符串拼接后的一个字符串。 |`constant` |
|Value |String |否 |表示 `Key` 的值。该参数仅当 `Action` 是 `set` 的时候才有效。如果 `Action` 不是 `set`，该参数无效。当 `ValueType` 是 `constant` 时，您需要指定一个字符串作为头部的值。该头部值的长度不能超过 1,024 个字符，不能包含美元符号（$）。<br><br>当 `ValueType` 是 `variable` 时，`Key` 的值可以是来自 [该列表中的某个变量](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-request-headers-cn#%E5%8F%98%E9%87%8F%E5%88%97%E8%A1%A8)。除了名称包含下划线的变量，列表中的任何一个变量都可以作为 `Key`，并赋予一个字符串来替换其已有的值。也就是说，当您使用任意这些名称不包含下划线的变量作为 `Key` 时，其值是可以被覆盖的。<br><br>当 `ValueType` 是 `customize` 时，表示 `Key` 的值是列表中的变量与字符串拼接后的字符串。在拼接的字符串中，变量使用 `${变量名}` 表示。示例值：`aaa${http_host}bbb${msec}ccc` |`bp-cdn` |


<span id="回源参数设置"></span>
### 回源参数设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginArg |Object[] |否 |表示 "回源参数" 配置的规则列表。<br><br><br>* 列表中最多可以包含 50 条规则。<br><br>* 每条规则包含一个匹配条件（`Condition`）和 CDN 执行操作（`OriginArgAction`）。<br><br>* 列表中规则的顺序定义了规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。<br><br><br>您**必须**在规则列表的最后添加以下这条默认规则。该默认规则用于匹配任何未能匹配其他规则的用户请求。您不可更改该规则中的 `Condition`，但可以更改 `OriginArgAction` 中的配置。<br><br>```json```<br>```{```<br>```            "Condition": {```<br>```                "ConditionRule": [```<br>```                    {```<br>```                        "Object": "directory",```<br>```                        "Operator": "match",```<br>```                        "Type": "url",```<br>```                        "Value": "/"```<br>```                    }```<br>```                ]```<br>```            },```<br>```            "OriginArgAction": {```<br>```                "OriginArgComponents": [```<br>```                    {```<br>```                        "Action": "include",```<br>```                        "Object": "queryString",```<br>```                        "Subobject": "*"```<br>```                    }```<br>```                ]```<br>```            }```<br>```        }```<br> | |
|Condition |Object |是 |表示匹配条件的配置。如果请求满足该匹配条件，CDN 执行 `OriginArgAction` 中指定的操作。当前您必须且只能指定一个条件。 | |
|ConditionRule |Object[] |是 |表示一个匹配条件的列表。当前，列表中只能包含一个匹配条件。 | |
|Object |String |是 |表示匹配类型。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。<br><br>* `regex`：表示请求 URL 中的完整路径，通过正则表达式匹配。 |`directory` |
|Operator |String |是 |表示匹配类型。当前，该参数值只能是 `match`，表示只有匹配成功才算是满足了匹配条件。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>同时，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个 URL 路径，以斜杠（/）开头。每个匹配值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果 `Object` 是 `regex`，每个匹配值表示一个正则表达式。关于正则表达式的示例，参见 [配置示例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-query-parameters_1-cn#%E5%85%A8%E8%B7%AF%E5%BE%84%E6%AD%A3%E5%88%99%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 |`/` |
|OriginArgAction |Object |是 |表示在请求满足 `Condition` 时 CDN 执行的操作。 | |
|OriginArgComponents |Object[] |是 |表示一个操作列表。这些操作定义了 CDN 如何处理回源请求中的查询参数。<br><br>当前，列表中只能包含一个操作。 | |
|Action |String |是 |表示 CDN 执行的操作。该参数有以下取值：<br><br><br>* `include`: 表示回源请求 URL 中包含用户请求 URL 中的全部查询参数。<br><br>* `exclude`：表示回源请求 URL 中不包含用户请求 URL 中的任何查询参数。<br><br>* `addPart`：表示回源请求 URL 中包含用户请求 URL 中的全部查询参数，并额外包含 `Subobject` 中指定的查询参数。<br><br>* `includePart`：表示如果用户请求 URL 中包含 `Subobject` 中指定的查询参数，那么回源请求 URL 中包含这些指定的查询参数。<br><br>* `excludePart`：表示回源请求 URL 中包含用户请求 URL 中的全部查询参数，除了`Subobject` 中指定的查询参数。<br><br>* `set`：表示回源请求 URL 中包含用户请求 URL 中的全部查询参数。同时，对于您在 `Subobject` 中指定的查询参数和参数值，CDN 会执行以下操作:<br><br>   * 如果这些查询参数在用户请求 URL 中，CDN 会在回源请求 URL 中将这些参数的值设置为您指定的值。<br><br>   * 如果用户请求 URL 中不包含这些查询参数，CDN 会在回源请求 URL 中添加这些查询参数。 |`exclude` |
|Object |String |是 |表示 CDN 对哪个对象执行 `Action`。当前，该参数值只能是 `queryString`，表示请求 URL 中的查询字符串。 |`queryString` |
|Subobject |String |是 |表示一个或者多个查询参数。多个查询参数之间使用分号（;）分隔，总长度不能超过 1,024 个字符。`Subobject` 只能包含字母、数字、下划线（_）、逗号（,）、短横线（\-）、句点（.）和感叹号（!）。<br><br>在匹配请求 URL 中的查询参数时，`Subobject` 中的参数是大小写敏感的。<br><br>`Subobject` 的额外说明如下：<br><br><br>* 当 `Action` 是 `include` 或 `exclude` 时，`Subobject` 必须是 `*`，表示请求 URL 中的所有查询参数。<br><br>* 当 `Action` 是 `includePart` 或 `excludePart` 时，`Subobject` 表示一个或者多个查询参数。例如 `param1;param2`。<br><br>* 当 `Action` 是 `addPart` 或 `set` 时，`Subobject` 表示一个或者多个查询参数和参数值，格式是 `key=value`。例如 `param1=val1;param2=val2;param3=val3`。 |`*` |


<span id="回源-sni-设置"></span>
### 回源 SNI 设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginSni |Object |否 |表示 "回源 SNI" 特性的配置。 | |
|SniDomain |String |否 |指定回源 SNI 的域名。当 `Switch` 是 `true` 时，该参数为必填。该参数值的长度不能超过 1,024 个字符。 |`img.example.com` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="回源-url-改写"></span>
### 回源 URL 改写


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginRewrite |Object |否 |表示 "回源 URL 改写" 特性的配置。要使用该特性，请 [提交工单](https://console.byteplus.com/workorder/create)。 | |
|OriginRewriteRule |Object[] |否 |表示一个规则列表。当 `Switch` 是 `true` 时，该参数为必填。<br><br><br>* 列表中最多可以包含 50 条规则。<br><br>* 列表中规则的顺序定义了规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|OriginRewriteAction |Object |否 |表示 CDN 执行的动作。 | |
|SourcePath |String |否 |表示一个正则表达式，长度不能超过 1,024 个字符，用于匹配用户请求 URL 中的对象。<br><br><br>* 当 `RewriteType` 是 `rewrite_path` 时，该对象指的是请求 URL 中的路径。<br><br>* 当 `RewriteType` 是 `rewrite_url` 时，该对象指的是请求 URL 中的路径和查询字符串。<br><br><br>参见 [配置示例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn?lang=en#%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。<br><br>说明<br><br>假设您在调用该 API 时在 `SourcePath` 中使用 `\?` 表示查询字符串中开头的 `?`。当您调用相应的查询 API（例如 DescribeCdnConfig）查看 `SourcePath` 的值时，您会发现 `\?` 变成了 `\\?`。这个变化是符合预期的，因为 `DescribeCdnConfig` 返回内容是 JSON 格式，内容中的 `\` 被转义成了 `\\`。 |`^/img/food.png$` |
|TargetPath |String |否 |表示改写后，回源请求 URL 中的对象，长度不能超过 1,024 个字符。<br><br><br>* 当 `RewriteType` 是 `rewrite_path` 时，该对象是回源请求 URL 中的路径。<br><br>* 当 `RewriteType` 是 `rewrite_url` 时，该对象是回源请求 URL 中的路径和查询字符串。<br><br><br>您可以在 `TargetPath` 中使用 `$1`、`$2`、`$3` 等捕获 `SourcePath` 中定义的组。<br><br>参见 [配置示例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn?lang=en#%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 |`/png/food.webp` |
|RewriteType |String |否 |表示改写类型。该参数有以下取值：<br><br><br>* `rewrite_path`：表示对请求 URL 中的路径进行改写。<br><br>* `rewrite_url`：表示对请求 URL 中的路径和查询字符串进行改写。<br><br><br>该参数的默认值是 `rewrite_path`。 |`rewrite_path` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="源站响应头设置"></span>
### 源站响应头设置


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginResponseHeader |Object[] |否 |表示 "源站响应头设置" 的配置模块。要使用该功能，请 [提交工单](https://console.byteplus.com/workorder/create)。 | |
|OriginResponseHeaderAction |Object |否 |表示 CDN 在收到源站响应时，对响应头的操作。 | |
|OriginResponseHeaderInstances |Object[] |否 |表示一个响应头的配置规则列表。每个规则都包含一个头部的相关操作设置。您最多可以添加 50 条规则。 | |
|Action |String |否 |表示 CDN 对响应头的操作。该参数有以下取值：<br><br><br>* `set`：表示设置一个头部。设置操作包括添加与修改。如果源站响应中已包含该头部，该头部的值会被覆盖。如果源站响应中没有包含该头部，该头部会被添加。<br><br>* `delete`：表示删除一个头部。 |`set` |
|Key |String |否 |表示一个头部的名称。名称不能超过 1,024 个字符，不区分大小写，不能包含汉字以及以下字符：<br><br><br>* 汉字、下划线（_）、空格、双引号（"）、冒号（:）<br><br><br>参见 [常用头部](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-header-configuration_zh-cn?lang=en#%E5%B8%B8%E7%94%A8%E5%A4%B4%E9%83%A8)。 |`MyHeader` |
|Value |String |否 |表示 `Key` 的值。该参数仅当 `Action` 是 `set` 的时候才有效。如果 `Action` 不是 `set`，该参数无效。<br><br><br>* 当 `ValueType` 是 `constant` 时，您需要指定一个固定字符串作为头部的值。头部值的长度不能超过 1,024 个字符，不能包含美元符号（$）。<br><br>* 当 `ValueType` 是 `variable` 时，`Key` 的值可以是来自 [该列表中的某个变量](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-header-configuration_zh-cn?lang=en#%E5%8F%98%E9%87%8F%E5%88%97%E8%A1%A8)。除了名称包含下划线的变量，列表中的任何一个变量都可以作为 `Key`，并赋予一个固定字符串来替换其已有的值。也就是说，当您使用任意这些名称不包含下划线的变量作为 `Key` 时，其值是可以被覆盖的。<br><br>* 当 `ValueType` 是 `customize` 时，表示 `Key` 的值是列表中的变量与固定字符串拼接后的字符串。在拼接的字符串中，变量使用 `${变量名}` 表示。示例值：`${remote_addr}aaa${host}ccc` |`hello` |
|ValueType |String |否 |表示 `Key` 的取值类型。该参数仅当 `Action` 是 `set` 的时候才有效。如果 `Action` 不是 `set`，该参数无效。该参数有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一个固定字符串。<br><br>* `variable`：表示 `Key` 的值来自一个变量。<br><br>* `customize`：表示 `Key` 的值是一个变量与固定字符串拼接后的字符串。 |`constant` |
|Object |String |否 |表示该规则对哪些用户请求生效。该参数有以下取值：<br><br><br>* `default`：表示该规则仅对源站响应中包含以下响应码的用户请求生效：<br><br>   * 200、201、204、206、301、302、303、304、307、308<br><br>* `all_request`：表示该规则对所有用户请求生效。<br><br><br>该参数的默认值是 `default`。另外，当 `Action` 是 `delete` 时，该参数的值只能是 `all_request`。 |`default` |


<span id="内容优化"></span>
## 内容优化

<span id="智能压缩"></span>
### 智能压缩


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Compression |Object |否 |表示 "智能压缩" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|CompressionRules |Object[] |否 |表示一组规则。每条规则包含匹配条件配置以及操作配置。 | |
|CompressionAction |Object |是 |表示当用户请求满足 `Condition` 时，CDN 对请求文件执行的压缩操作的配置。 | |
|CompressionType |String[] |是 |表示 CDN 使用的压缩算法。该参数有以下取值：<br><br><br>* `br`：表示 Brotli 压缩算法。<br><br>* `gzip`：表示 Gzip 压缩算法。<br><br><br>您可以同时指定这两个算法。<br><br>需要留意的是，CDN 基于用户请求中 `Accept-Encoding` 头部来决定是否对请求文件进行压缩以及使用的压缩算法。 |`["gzip","br"]` |
|CompressionFormat |String |否 |表示 CDN 基于请求中的 `Content-Type` 头部对请求进行匹配。该参数有以下取值：<br><br><br>* `default`：表示如果 `Content-Type` 头部值在下方的默认列表中，CDN 对请求文件执行 `CompressionAction` 中配置的操作。<br><br>* `customize`：表示如果 `Content-Type` 头部值在 `CompressionFormat` 指定的头部值中，CDN 对请求文件执行 `CompressionAction` 中配置的操作。<br><br><br>如果您需要 CDN 基于 `Condition` 中的匹配条件对请求进行匹配，您无需指定 `CompressionFormat` 或者指定 `CompressionFormat` 为 `all`。<br><br>**默认列表**<br><br>text/html、text/xml、text/plain、text/css、application/javascript、application/x\-javascript、application/rss+xml、text/javascript、image/tiff、image/svg+xml、application/json、application/xml、text/plain; charset=utf\-8 |`customize` |
|CompressionTarget |String |否 |表示 `Content-Type` 的过滤值。<br><br><br>* 如果 `CompressionFormat` 为 `default` 或者 `all`，该参数必须为 `*`。<br><br>* 如果 `CompressionFormat` 为 `customize`，您需要指定一个或者多个文件类型。多个文件类型之间以逗号（,）分隔。 |`application/xml,hello/world` |
|MinFileSizeKB |Long |否 |表示文件大小范围的最小值，CDN 仅对大小在 `MinFileSizeKB` 和 `MaxFileSizeKB` 所表示的范围内的文件进行压缩。该参数的取值范围是 0 \- 2,147,483,647，单位是 KB，使用的进制是 1,024。该参数的默认值是 `0`。 |`10` |
|MaxFileSizeKB |Long |否 |表示文件大小范围的最大值，取值范围是 0 \- 2,147,483,647，单位是 KB，使用的进制是 1,024。如果不指定该参数，表示您不限制文件大小的上限。 |`1000` |
|Condition |Object |否 |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `CompressionAction` 中指定的操作。<br><br>需要留意的是，如果您指定了 `CompressionFormat`，`Condition` 必须为 `null` 或者不指定。 | |
|ConditionRule |Object[] |是 |表示匹配条件列表。当前，列表中只能包含一个匹配条件。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。 |`directory` |
|Operator |String |是 |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |是 |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |是 |表示一个或者多个匹配值，总长度不能超过 1,024 个字符。多个匹配值之间使用分号（;）分隔。匹配值不能包含以下字符：<br><br><br>* 双斜杠（//）、空格、美元符号（$）、问号（?）<br><br><br>同时，<br><br><br>* 如果 `Object` 是 `filetype`，每个匹配值表示一个请求 URL 后缀，无需以句点（.）开头，只能包含字母和数字。例如：`png;txt`。<br><br>* 如果 `Object` 是 `directory`，每个匹配值表示一个目录路径，以斜杠（/）开头和结尾。例如 `/chs/foods/;/us/birds/`。<br><br>* 如果 `Object` 是 `path`，每个匹配值表示一个 URL 路径，以斜杠（/）开头。每个匹配值中可以包含通配符（\*）表示一个或者多个字符。例如 `/chs/foods/local*sets;/us/birds/chickadee`。 |`/img/` |


<span id="页面优化"></span>
### 页面优化


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|PageOptimization |Object |否 |表示 "页面优化" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OptimizationType |String[] |是 |表示优化的对象。该参数有以下取值：<br><br><br>* `html`: 表示 HTML 页面。<br><br>* `js`: 表示 Javascript 代码。<br><br>* `css`: 表示 CSS 代码。<br><br><br>该参数的默认值是 `html`。如果您指定了 `js` 或者 `js`，`html` 也必须指定。 |`["html","js"]` |


<span id="视频拖拽"></span>
### 视频拖拽


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|VideoDrag |Object |否 |表示 "视频拖拽" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |


<span id="ai-流量管理"></span>
## AI 流量管理

<span id="html-转-markdown"></span>
### HTML 转 Markdown


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|HTMLToMarkdown |Object |否 |表示 "HTML 转 Markdown" 特性的配置。 | |
|Switch |Boolean |是 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。无 |`true` |


<span id="性能优化"></span>
## 性能优化

<span id="智能路由"></span>
### 智能路由


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|SmartOriginRouting |Object |否 |表示 "智能路由" 特性的配置。 | |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |


<span id="源站预建连"></span>
### 源站预建连


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|OriginPreconnect |Object |否 |表示 "源站预建连" 特性的配置。 | |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |


<span id="高级配置"></span>
## 高级配置

<span id="共享缓存"></span>
### 共享缓存


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|CacheHost |Object |否 |表示 "共享缓存" 特性的配置。要使用该特性，请 [提交工单](https://console.byteplus.com/workorder/create)。<br><br>如果您要对多个域名配置共享缓存，您需要调用该 API 对每个域名配置目标域名。 | |
|CacheHostRule |Object[] |否 |表示一组共享缓存的配置。当前您只能只能创建一个配置。当 `Switch` 是 `true` 时，该参数为必填。 | |
|CacheHostAction |Object |否 |表示配置的详情。 | |
|CacheHost |String |否 |表示目标域名。 该目标域名必须是您账户下的一个域名。该参数指示 `Domain` 共享 `CacheHost` 的 CDN 缓存。 |`www.test.com` |
|Switch |Boolean |否 |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |


<span id="返回参数"></span>
## 返回参数

<span id="资源列表"></span>
## 资源列表

<span id="域名列表"></span>
### 域名列表


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|ResourceIds |String[] |表示创建的域名列表。 |`["www.example.com","docs.example.com"]` |


<span id="请求示例"></span>
## 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=AddCdnDomain&Version=2021-03-01
{
    "Domain": "www.example.com",
    "ResourceTags": [
        {
            "Key": "key1",
            "Value": "value1"
        },
        {
            "Key": "key2",
            "Value": "value2"
        }
    ],
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceType": "web",
    "Project": "default",
    "OriginProtocol": "http",
    "Origin": [
        {
            "OriginAction": {
                "OriginLines": [
                    {
                        "Address": "203.0.113.8",
                        "HttpPort": "80",
                        "HttpsPort": "443",
                        "InstanceType": "ip",
                        "OriginHost": "myorigin.example.com",
                        "OriginType": "primary",
                        "PrivateBucketAccess": false,
                        "Weight": "1"
                    },
                    {
                        "Address": "img.example.com",
                        "HttpPort": "80",
                        "HttpsPort": "443",
                        "InstanceType": "domain",
                        "OriginHost": "myorigin2.example.com",
                        "OriginType": "primary",
                        "PrivateBucketAccess": false,
                        "Weight": "1"
                    },
                    {
                        "Address": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                        "InstanceType": "tos",
                        "OriginHost": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                        "OriginType": "primary",
                        "PrivateBucketAccess": true,
                        "PrivateBucketAuth": {
                            "AuthType": "tos",
                            "Switch": true
                        },
                        "Region": "ap-southeast-3",
                        "Weight": "1"
                    },
                    {
                        "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                        "InstanceType": "tos",
                        "OriginHost": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                        "OriginType": "primary",
                        "PrivateBucketAccess": true,
                        "PrivateBucketAuth": {
                            "AuthType": "oss",
                            "Switch": true,
                            "TosAuthInformation": {
                                "AccessKeyId": "xxxxxxxxxx",
                                "AccessKeySecret": "xxxxxx"
                            }
                        },
                        "Region": "oss-ap-southeast-1",
                        "Weight": "2"
                    },
                    {
                        "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                        "InstanceType": "tos",
                        "OriginHost": "mybucket.cos.ap-singapore.myqcloud.com",
                        "OriginType": "primary",
                        "PrivateBucketAccess": true,
                        "PrivateBucketAuth": {
                            "AuthType": "cos",
                            "Switch": true,
                            "TosAuthInformation": {
                                "AccessKeyId": "xxxxxxxxxxxxxxxxxxx",
                                "AccessKeySecret": "xxxxxxxxxxxx"
                            }
                        },
                        "Region": "ap-singapore",
                        "Weight": "3"
                    },
                    {
                        "Address": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                        "InstanceType": "tos",
                        "OriginHost": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                        "OriginType": "primary",
                        "PrivateBucketAccess": true,
                        "PrivateBucketAuth": {
                            "AuthType": "aws_common",
                            "Switch": true,
                            "TosAuthInformation": {
                                "AccessKeyId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                                "AccessKeySecret": "xxxxxxxxxx"
                            }
                        },
                        "Region": "ap-southeast-1",
                        "Weight": "5"
                    },
                    {
                        "Address": "myazstorage.blob.core.windows.net",
                        "BucketName": "myazstorage",
                        "InstanceType": "tos",
                        "OriginHost": "myazstorage.blob.core.windows.net",
                        "OriginType": "primary",
                        "PrivateBucketAccess": true,
                        "PrivateBucketAuth": {
                            "AuthType": "azure",
                            "Switch": true,
                            "TosAuthInformation": {
                                "AccountKey": "xxxxxxxxxxxxxxxx"
                            }
                        },
                        "Weight": "1"
                    },
                    {
                        "Address": "203.0.113.9",
                        "HttpPort": "80",
                        "HttpsPort": "443",
                        "InstanceType": "ip",
                        "OriginType": "backup",
                        "PrivateBucketAccess": false,
                        "Weight": "1"
                    },
                    {
                        "Address": "img2.example.com",
                        "HttpPort": "80",
                        "HttpsPort": "443",
                        "InstanceType": "domain",
                        "OriginType": "backup",
                        "PrivateBucketAccess": false,
                        "Weight": "1"
                    }
                ]
            }
        }
    ],
    "SignedUrlAuth": {
        "AuthRulesF": [
            {
                "ArgumentRule": {
                    "GeneralParamRule": {
                        "ParentLinkParamInherit": "inherit",
                        "SubLinkParamRule": {
                            "InheritMode": "inherit_first",
                            "KeepSubLinkArg": "keep"
                        }
                    },
                    "KeepOriginArg": true
                },
                "AuthTokenCalRule": {
                    "ParamCalRules": [
                        "md5_bin",
                        "base64url",
                        "sha256",
                        "md5",
                        "base64_encode"
                    ],
                    "SignJoinSymbol": "abc",
                    "SignParam": [
                        {
                            "ParamType": "SecretKey"
                        },
                        {
                            "ParamType": "SupString",
                            "SupContent": "fixstring"
                        },
                        {
                            "ParamSource": "ChildLink",
                            "ParamType": "URI",
                            "UriParamSup": {
                                "JoinSymbol": "/",
                                "SplitSymbol": "-",
                                "StartLevel": 3,
                                "TermLevel": 5
                            }
                        },
                        {
                            "ParamSource": "ParentLink",
                            "ParamType": "URLParam",
                            "UrlParam": {
                                "ArgSegment": {
                                    "Level": 0,
                                    "Switch": false
                                },
                                "CapMode": "uri",
                                "UriLevel": 3
                            }
                        },
                        {
                            "ParamType": "ClientDomain"
                        },
                        {
                            "ParamType": "Referer"
                        },
                        {
                            "ParamType": "Origin"
                        },
                        {
                            "ParamType": "ClientIP"
                        },
                        {
                            "ParamType": "UA"
                        },
                        {
                            "ParamType": "ReqHeader",
                            "RequestHeader": "myheader1"
                        },
                        {
                            "CookieToken": "mycookie1",
                            "ParamType": "Cookie"
                        },
                        {
                            "ParamSource": "ChildLink",
                            "ParamType": "FullURI"
                        }
                    ]
                },
                "Condition": {
                    "ConditionRule": [
                        {
                            "Object": "filetype",
                            "Operator": "match",
                            "Type": "url",
                            "Value": "jpg;png"
                        },
                        {
                            "Object": "directory",
                            "Operator": "not_match",
                            "Type": "url",
                            "Value": "/docs/foods/;/dogs/ragdolls/"
                        },
                        {
                            "Object": "path",
                            "Operator": "match",
                            "Type": "url",
                            "Value": "/docs/file1;/docs/file2"
                        },
                        {
                            "Object": "regex",
                            "Operator": "match",
                            "Type": "url",
                            "Value": "^/a{1,2}(.*)g$"
                        }
                    ],
                    "Connective": "OR"
                },
                "CustomRewrite": {
                    "RewriteParam": [
                        {
                            "ParamType": "ParentLinkUrlParam",
                            "ParentLinkUrlParam": {
                                "ArgSegment": {
                                    "Level": 0,
                                    "Switch": false
                                },
                                "CapMode": "name",
                                "ParamName": "param23"
                            }
                        },
                        {
                            "ParamType": "SupString",
                            "SupContent": "string2"
                        },
                        {
                            "ParamType": "ParentLinkURI",
                            "ParentLinkUriParamSup": {
                                "JoinSymbol": "/",
                                "SplitSymbol": "-",
                                "StartLevel": 4,
                                "TermLevel": 6
                            }
                        },
                        {
                            "ParamType": "ParentLinkExpire"
                        },
                        {
                            "ParamType": "AuthToken"
                        },
                        {
                            "ParamType": "ParentFullURI"
                        }
                    ],
                    "RewriteRule": {
                        "CapMode": "name",
                        "ParamName": "myparam1"
                    },
                    "SignJoinSymbol": "/",
                    "Switch": true
                },
                "ExpireTimeRule": {
                    "Duration": 30,
                    "ExpTimeCapRule": {
                        "ArgSegment": {
                            "Level": 0,
                            "Switch": false
                        },
                        "CapMode": "name",
                        "ParamName": "param1"
                    },
                    "TimeFormat": "heximal"
                },
                "RewriteFormat": "default",
                "RewriteM3U8": {
                    "RewriteM3U8Tag": {
                        "Switch": true,
                        "Tags": [
                            "tag1",
                            "tag2"
                        ]
                    },
                    "Switch": true
                },
                "RewriteMPD": {
                    "MpdVarExpand": true,
                    "Switch": true
                },
                "RuleName": "Authentication rule A",
                "SecretKey": {
                    "BackupSecretKey": "secondarykey",
                    "MasterSecretKey": "primarykey"
                },
                "SignCapRule": {
                    "ArgSegment": {
                        "Level": 2,
                        "SplitSymbol": "-",
                        "Switch": true
                    },
                    "CapMode": "uri",
                    "UriLevel": 2
                }
            },
            {
                "ArgumentRule": {
                    "GeneralParamRule": {
                        "ParentLinkParamInherit": "not_inherit",
                        "SubLinkParamRule": {
                            "InheritMode": "sub_link_first",
                            "KeepSubLinkArg": "keep"
                        }
                    },
                    "KeepOriginArg": false
                },
                "AuthTokenCalRule": {
                    "ParamCalRules": [
                        "base64url"
                    ],
                    "SignJoinSymbol": "45yu",
                    "SignParam": [
                        {
                            "ParamType": "SecretKey"
                        }
                    ]
                },
                "Condition": {
                    "ConditionRule": [
                        {
                            "Object": "directory",
                            "Operator": "match",
                            "Type": "url",
                            "Value": "/"
                        }
                    ],
                    "Connective": "OR"
                },
                "ExpireTimeRule": {
                    "Duration": 67,
                    "ExpTimeCapRule": {
                        "CapMode": "cookie",
                        "CustomValue": "mycookie56"
                    },
                    "TimeFormat": "octal"
                },
                "RewriteFormat": "default",
                "RuleName": "Authentication rule B",
                "SecretKey": {
                    "BackupSecretKey": "sk",
                    "MasterSecretKey": "pk"
                },
                "SignCapRule": {
                    "CapMode": "header",
                    "CustomValue": "myheader56"
                }
            }
        ],
        "Switch": true
    },
    "OriginIPv6": "followclient",
    "OriginCertCheck": {
        "Switch": false
    },
    "OriginHost": "",
    "ConditionalOrigin": {
        "OriginRules": [
            {
                "Actions": {
                    "OriginLines": [
                        {
                            "Address": "203.0.113.6",
                            "HttpPort": "80",
                            "HttpsPort": "443",
                            "InstanceType": "ip",
                            "OriginHost": "",
                            "OriginType": "primary",
                            "Weight": "10"
                        }
                    ]
                },
                "Condition": {
                    "ConditionGroups": [
                        {
                            "Condition": {
                                "Name": "myparam",
                                "Object": "query_name",
                                "Operator": "equal",
                                "Type": "querystring",
                                "Value": [
                                    "myvalue"
                                ]
                            },
                            "IsGroup": false
                        }
                    ],
                    "Connective": "and",
                    "IsGroup": true
                }
            },
            {
                "Actions": {
                    "OriginLines": [
                        {
                            "Address": "mybucket.s3-ap-southeast-1.amazonaws.com",
                            "BucketSource": "aws_common",
                            "HttpPort": "",
                            "HttpsPort": "",
                            "InstanceType": "storage",
                            "OriginHost": "",
                            "OriginType": "primary",
                            "Weight": "10",
                            "PrivateBucketAccess": true,
                            "TosAuthInformation": {
                                "AccessKeyId": "xxxxxxxxxxxxx",
                                "AccessKeySecret": "xxxxx",
                                "Region": "ap-southeast-1"
                            }
                        }
                    ]
                },
                "Condition": {
                    "ConditionGroups": [
                        {
                            "Condition": {
                                "Name": "myheader",
                                "Object": "customize",
                                "Operator": "match",
                                "Type": "request_header",
                                "Value": [
                                    "myvalue"
                                ]
                            },
                            "IsGroup": false
                        }
                    ],
                    "Connective": "and",
                    "IsGroup": true
                }
            },
            {
                "Actions": {
                    "OriginLines": [
                        {
                            "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                            "BucketSource": "cos",
                            "HttpPort": "",
                            "HttpsPort": "",
                            "InstanceType": "storage",
                            "OriginHost": "",
                            "OriginType": "primary",
                            "Weight": "10",
                            "PrivateBucketAccess": true,
                            "TosAuthInformation": {
                                "AccessKeyId": "xxxxxxxxxxxxx",
                                "AccessKeySecret": "xxxxx"
                            }
                        }
                    ]
                },
                "Condition": {
                    "ConditionGroups": [
                        {
                            "Condition": {
                                "Object": "client_ip",
                                "Operator": "belong",
                                "Value": [
                                    "HKG",
                                    "CHE"
                                ]
                            },
                            "IsGroup": false
                        }
                    ],
                    "Connective": "and",
                    "IsGroup": true
                }
            },
            {
                "Actions": {
                    "OriginLines": [
                        {
                            "Address": "banana-health.tos-ap-southeast-1.bytepluses.com",
                            "BucketSource": "tos",
                            "HttpPort": "",
                            "HttpsPort": "",
                            "OriginType": "primary",
                            "Weight": "10",
                            "InstanceType": "storage",
                            "OriginHost": "banana-health.tos-ap-southeast-1.bytepluses.com",
                            "PrivateBucketAccess": true
                        }
                    ]
                },
                "Condition": {
                    "ConditionGroups": [
                        {
                            "Condition": {
                                "Object": "filetype",
                                "Operator": "equal",
                                "Value": [
                                    "png"
                                ]
                            },
                            "IsGroup": false
                        }
                    ],
                    "Connective": "and",
                    "IsGroup": true
                }
            },
            {
                "Actions": {
                    "OriginLines": [
                        {
                            "Address": "www.example.com",
                            "HttpPort": "80",
                            "HttpsPort": "443",
                            "OriginType": "primary",
                            "Weight": "10",
                            "InstanceType": "domain",
                            "OriginHost": "non-img.example.com"
                        }
                    ]
                },
                "Condition": {
                    "ConditionGroups": [
                        {
                            "Condition": {
                                "Object": "directory",
                                "Operator": "not_equal",
                                "Value": [
                                    "/img/"
                                ]
                            },
                            "IsGroup": false
                        }
                    ],
                    "Connective": "and",
                    "IsGroup": true
                }
            },
            {
                "Actions": {
                    "OriginLines": [
                        {
                            "Address": "198.51.100.5",
                            "HttpPort": "80",
                            "HttpsPort": "443",
                            "OriginType": "primary",
                            "Weight": "10",
                            "InstanceType": "ip",
                            "OriginHost": "img.example.com"
                        }
                    ]
                },
                "Condition": {
                    "ConditionGroups": [
                        {
                            "Condition": {
                                "Object": "full_querystring",
                                "Operator": "regex_match",
                                "Value": [
                                    "^/a{1,2}.*g$"
                                ]
                            },
                            "IsGroup": false
                        }
                    ],
                    "Connective": "and",
                    "IsGroup": true
                }
            },
            {
                "Actions": {
                    "OriginLines": [
                        {
                            "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                            "BucketSource": "oss",
                            "HttpPort": "",
                            "HttpsPort": "",
                            "InstanceType": "storage",
                            "OriginHost": "",
                            "OriginType": "primary",
                            "Weight": "10",
                            "PrivateBucketAccess": true,
                            "TosAuthInformation": {
                                "AccessKeyId": "xxxxxxxxxxxxx",
                                "AccessKeySecret": "xxxxx"
                            }
                        }
                    ]
                },
                "Condition": {
                    "ConditionGroups": [
                        {
                            "Condition": {
                                "Object": "path",
                                "Operator": "equal",
                                "Value": [
                                    "/docs/file1",
                                    "/docs/file2/"
                                ]
                            },
                            "IsGroup": false
                        },
                        {
                            "Condition": {
                                "Object": "path",
                                "Operator": "equal",
                                "Value": [
                                    "/docs/file3",
                                    "/docs/file4/"
                                ]
                            },
                            "IsGroup": false
                        }
                    ],
                    "Connective": "or",
                    "IsGroup": true
                }
            }
        ],
        "Switch": true
    },
    "HTTPS": {
        "CertInfo": {
            "CertId": "cert-7fade0eb4f8d4aadbde5dd25f2ffdf35",
            "CertName": "1000011991",
            "EncryType": "inter_cert",
            "ExpireTime": 1763086346,
            "Source": "cert_center"
        },
        "DisableHttp": false,
        "ForcedRedirect": {
            "EnableForcedRedirect": true,
            "StatusCode": "303"
        },
        "HTTP2": true,
        "Hsts": {
            "Subdomain": "include",
            "Switch": true,
            "Ttl": 50
        },
        "OCSP": true,
        "Switch": true,
        "TlsVersion": [
            "tlsv1.1",
            "tlsv1.2"
        ]
    },
    "HttpForcedRedirect": {
        "EnableForcedRedirect": false,
        "StatusCode": "301"
    },
    "AreaAccessRule": {
        "Switch": true,
        "RuleType": "deny",
        "Area": [
            "HKG",
            "MAC",
            "AZE",
            "PNG"
        ]
    },
    "RequestBlockRule": {
        "Switch": true,
        "BlockRule": [
            {
                "RuleName": "rule2",
                "Condition": {
                    "ConditionRule": [
                        {
                            "Name": "",
                            "Object": "filetype",
                            "Operator": "equal",
                            "Type": "url",
                            "Value": "png;jpg"
                        }
                    ],
                    "Connective": "AND"
                },
                "RequestBlockAction": {
                    "Action": "redirect",
                    "StatusCode": "302",
                    "ResponseBody": "default",
                    "ErrorPage": null,
                    "RedirectURL": "http://www.example.com/redir"
                },
                "BlockAction": {
                    "Action": "redirect",
                    "StatusCode": "302",
                    "RedirectUrl": "http://www.example.com/redir"
                }
            },
            {
                "RuleName": "rule1",
                "Condition": {
                    "ConditionRule": [
                        {
                            "Name": "",
                            "Object": "path",
                            "Operator": "equal",
                            "Type": "url",
                            "Value": "/abc/file1;/eff/file2"
                        },
                        {
                            "Name": "",
                            "Object": "directory",
                            "Operator": "equal",
                            "Type": "url",
                            "Value": "/eee/;/eef/"
                        }
                    ],
                    "Connective": "AND"
                },
                "RequestBlockAction": {
                    "Action": "refuse",
                    "StatusCode": "400",
                    "ResponseBody": "default",
                    "ErrorPage": null,
                    "RedirectURL": null
                },
                "BlockAction": {
                    "Action": "refuse",
                    "StatusCode": "400",
                    "RedirectUrl": null
                }
            }
        ]
    },
    "DownloadSpeedLimit": {
        "Switch": true,
        "DownloadSpeedLimitRules": [
            {
                "Condition": {
                    "ConditionRule": [
                        {
                            "Type": "url",
                            "Object": "unlimited",
                            "Operator": "match",
                            "Value": ""
                        }
                    ]
                },
                "DownloadSpeedLimitAction": {
                    "SpeedLimitRate": 102400,
                    "SpeedLimitRateAfter": 157286400,
                    "SpeedLimitTime": {
                        "DayWeek": "thursday",
                        "BeginTime": "00:00",
                        "EndTime": "23:59"
                    }
                }
            },
            {
                "Condition": {
                    "ConditionRule": [
                        {
                            "Type": "url",
                            "Object": "directory",
                            "Operator": "match",
                            "Value": "/abc/;/eff/"
                        }
                    ]
                },
                "DownloadSpeedLimitAction": {
                    "SpeedLimitRate": 10240,
                    "SpeedLimitRateAfter": 104857600,
                    "SpeedLimitTime": {
                        "DayWeek": "monday;wednesday;saturday",
                        "BeginTime": "00:00",
                        "EndTime": "23:59"
                    }
                }
            },
            {
                "Condition": {
                    "ConditionRule": [
                        {
                            "Type": "url",
                            "Object": "filetype",
                            "Operator": "match",
                            "Value": "jpg;jpeg"
                        }
                    ]
                },
                "DownloadSpeedLimitAction": {
                    "SpeedLimitRate": 102400,
                    "SpeedLimitRateAfter": 104857600,
                    "SpeedLimitTime": {
                        "DayWeek": "unlimited",
                        "BeginTime": "00:00",
                        "EndTime": "23:59"
                    }
                }
            }
        ]
    },
    "IPv6": {
        "Switch": true
    },
    "IpAccessRule": {
        "Switch": true,
        "RuleType": "allow",
        "Ip": [
            "192.168.1.2",
            "192.168.1.3"
        ],
        "IpSource": {
            "SourceList": null,
            "Type": "default"
        },
        "DenyStatusCode": 405
    },
    "IpFreqLimit": {
        "Switch": false
    },
    "MethodDeniedRule": {
        "Switch": true,
        "Methods": "POST,DELETE,PUT,PATCH,CONNECT,OPTIONS,GET,HEAD"
    },
    "OriginAccessRule": {
        "Switch": true,
        "RuleType": "deny",
        "Origins": [
            "abc.example.com",
            "edf.example.net"
        ],
        "IgnoreCase": true,
        "AllowEmpty": true
    },
    "ProxyProtocol": {
        "Switch": false
    },
    "RefererAccessRule": {
        "Switch": true,
        "RuleType": "deny",
        "AllowEmpty": true,
        "Referers": [],
        "ReferersType": {
            "CommonType": {
                "Referers": [
                    "www.example.net",
                    "www.example.org"
                ],
                "IgnoreCase": true,
                "IgnoreScheme": true
            },
            "RegularType": {
                "Referers": [
                    "^http\\://a\\.com",
                    "^http\\://b\\.com"
                ]
            }
        }
    },
    "RemoteAuth": {
        "RemoteAuthRules": [
            {
                "Condition": {
                    "ConditionRule": [
                        {
                            "Object": "path",
                            "Operator": "match",
                            "Value": "/aaa/file1;/bbb/file2",
                            "Type": "url",
                            "Name": ""
                        },
                        {
                            "Object": "directory",
                            "Operator": "match",
                            "Value": "/efe/;/abc/",
                            "Type": "url",
                            "Name": ""
                        },
                        {
                            "Object": "filetype",
                            "Operator": "match",
                            "Value": "jpg;png;bin",
                            "Type": "url",
                            "Name": ""
                        }
                    ]
                },
                "RemoteAuthRuleAction": {
                    "AuthModeConfig": {
                        "BackupRemoteAddr": "http://www.example.com:8081",
                        "MasterRemoteAddr": "http://www.example.com:8080",
                        "PathType": "variable",
                        "PathValue": "/auth",
                        "RequestMethod": "default"
                    },
                    "AuthResponseConfig": {
                        "StatusCodeAction": {
                            "SuccessCode": "200",
                            "FailCode": "401",
                            "DefaultAction": "pass"
                        },
                        "TimeOutAction": {
                            "Time": 200,
                            "Action": "pass"
                        },
                        "CacheAction": {
                            "Action": "cache",
                            "Ttl": 100,
                            "CacheKey": [
                                "URI",
                                "X-Forwarded-For"
                            ],
                            "IgnoreCase": false
                        },
                        "ResponseAction": {
                            "StatusCode": "403"
                        }
                    },
                    "QueryStringRules": {
                        "QueryStringComponents": {
                            "Action": "includePart",
                            "Value": "param3;param4"
                        },
                        "QueryStringInstances": [
                            {
                                "Action": "set",
                                "Key": "param2",
                                "Value": "host",
                                "ValueType": "variable"
                            },
                            {
                                "Action": "set",
                                "Key": "param1",
                                "Value": "aaaa",
                                "ValueType": "constant"
                            }
                        ]
                    },
                    "RequestHeaderRules": {
                        "RequestHost": "auth.example.com",
                        "RequestHeaderComponents": {
                            "Action": "includePart",
                            "Value": "header1;header2"
                        },
                        "RequestHeaderInstances": [
                            {
                                "Action": "set",
                                "Key": "auth_header2",
                                "Value": "msec",
                                "ValueType": "variable"
                            },
                            {
                                "Action": "set",
                                "Key": "auth_header",
                                "Value": "111",
                                "ValueType": "constant"
                            }
                        ]
                    }
                }
            }
        ],
        "Switch": true
    },
    "ServerSentEvent": {
        "Switch": true
    },
    "UaAccessRule": {
        "Switch": true,
        "RuleType": "deny",
        "UserAgent": [
            "*curl*",
            "*firefox*"
        ],
        "IgnoreCase": true,
        "AllowEmpty": true
    },
    "UrlNormalize": {
        "Switch": true,
        "NormalizeObject": [
            "back_slashes",
            "successive_slashes",
            "dot_segments"
        ]
    },
    "RedirectionRewrite": {
        "Switch": true,
        "RedirectionRule": [
            {
                "RedirectionAction": {
                    "RedirectCode": "302",
                    "SourcePath": "^/test$",
                    "TargetHost": "www.example.com",
                    "TargetPath": "/target",
                    "TargetProtocol": "followclient",
                    "TargetQueryComponents": {
                        "Action": "includePart",
                        "Value": "param7;param8"
                    }
                }
            }
        ]
    },
    "Websocket": {
        "Switch": true,
        "Timeout": 60
    },
    "BrowserCache": [
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Type": "url",
                        "Operator": "match",
                        "Object": "directory",
                        "Value": "/dafsd/"
                    }
                ],
                "Connective": "OR"
            },
            "CacheAction": {
                "Action": "cache",
                "DefaultPolicy": "origin_first",
                "IgnoreCase": true,
                "Ttl": 0
            }
        },
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Type": "url",
                        "Operator": "match",
                        "Object": "filetype",
                        "Value": "shtml;htm"
                    }
                ],
                "Connective": "OR"
            },
            "CacheAction": {
                "Action": "cache",
                "DefaultPolicy": "cache",
                "IgnoreCase": true,
                "Ttl": 600
            }
        }
    ],
    "CacheKey": [
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Operator": "match",
                        "Type": "url",
                        "Object": "directory",
                        "Value": "/ererer/",
                        "IgnoreCase": true
                    }
                ],
                "Connective": "OR"
            },
            "CacheKeyAction": {
                "CacheKeyComponents": [
                    {
                        "Action": "include",
                        "Object": "queryString",
                        "Subobject": "*",
                        "IgnoreCase": false
                    }
                ]
            }
        },
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Operator": "match",
                        "Type": "url",
                        "Object": "filetype",
                        "Value": "shtml;html",
                        "IgnoreCase": true
                    }
                ],
                "Connective": "OR"
            },
            "CacheKeyAction": {
                "CacheKeyComponents": [
                    {
                        "Action": "includePart",
                        "Object": "queryString",
                        "Subobject": "param1;param2",
                        "IgnoreCase": true
                    }
                ]
            }
        },
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Operator": "match",
                        "Type": "url",
                        "Object": "directory",
                        "Value": "/",
                        "IgnoreCase": false
                    }
                ],
                "Connective": "OR"
            },
            "CacheKeyAction": {
                "CacheKeyComponents": [
                    {
                        "Action": "include",
                        "Object": "queryString",
                        "Subobject": "*",
                        "IgnoreCase": true
                    }
                ]
            }
        }
    ],
    "CustomErrorPage": {
        "Switch": true,
        "ErrorPageRule": [
            {
                "ErrorPageAction": {
                    "StatusCode": "500",
                    "RedirectCode": "301",
                    "RedirectUrl": "http://www.example.com/re-dir1",
                    "Action": "redirect"
                }
            }
        ]
    },
    "HTMLToMarkdown": {
        "Switch": true
    },
    "MultiRange": {
        "Switch": false
    },
    "Cache": [
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Type": "url",
                        "Operator": "match",
                        "Object": "path",
                        "Value": "/efef/file1",
                        "Name": ""
                    }
                ],
                "Connective": "OR"
            },
            "CacheAction": {
                "Action": "cache",
                "DefaultPolicy": "origin_first",
                "IgnoreCase": true,
                "Ttl": 151,
                "SetCookieNoCache": true
            }
        },
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Type": "url",
                        "Operator": "match",
                        "Object": "directory",
                        "Value": "/abcc/;/eeee/",
                        "Name": ""
                    }
                ],
                "Connective": "OR"
            },
            "CacheAction": {
                "Action": "cache",
                "DefaultPolicy": "default",
                "IgnoreCase": false,
                "Ttl": 0,
                "SetCookieNoCache": false
            }
        },
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Type": "url",
                        "Operator": "match",
                        "Object": "filetype",
                        "Value": "png;jpeg",
                        "Name": ""
                    }
                ],
                "Connective": "OR"
            },
            "CacheAction": {
                "Action": "cache",
                "DefaultPolicy": "force_cache",
                "IgnoreCase": true,
                "Ttl": 100,
                "SetCookieNoCache": false
            }
        }
    ],
    "OfflineCache": {
        "Switch": true,
        "Object": "request_error,error_code",
        "StatusCode": "509;507"
    },
    "ResponseHeader": [
        {
            "ResponseHeaderAction": {
                "ResponseHeaderInstances": [
                    {
                        "AccessOriginControl": false,
                        "Action": "set",
                        "Key": "Access-Control-Max-Age",
                        "Value": "http_host",
                        "ValueType": "variable"
                    },
                    {
                        "AccessOriginControl": false,
                        "Action": "delete",
                        "Key": "myheader1",
                        "Value": "",
                        "ValueType": ""
                    },
                    {
                        "AccessOriginControl": false,
                        "Action": "delete",
                        "Key": "Access-Control-Expose-Headers",
                        "Value": "",
                        "ValueType": ""
                    },
                    {
                        "AccessOriginControl": true,
                        "Action": "set",
                        "Key": "Access-Control-Allow-Origin",
                        "Value": "aaaa",
                        "ValueType": "constant"
                    }
                ]
            }
        }
    ],
    "NegativeCache": [
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Operator": "match",
                        "Type": "url",
                        "Object": "filetype",
                        "Value": "jpeg;png"
                    }
                ],
                "Connective": "OR"
            },
            "NegativeCacheRule": {
                "Action": "cache",
                "StatusCode": "400",
                "Ttl": 100,
                "IgnoreCase": true
            }
        }
    ],
    "PageOptimization": {
        "Switch": true,
        "OptimizationType": [
            "html",
            "js",
            "css"
        ]
    },
    "Compression": {
        "Switch": true,
        "CompressionRules": [
            {
                "CompressionAction": {
                    "CompressionFormat": "all",
                    "CompressionTarget": "*",
                    "CompressionType": [
                        "gzip",
                        "br"
                    ],
                    "MinFileSizeKB": 25
                },
                "Condition": {
                    "ConditionRule": [
                        {
                            "Object": "filetype",
                            "Value": "ico;xml",
                            "Operator": "match",
                            "Type": "url"
                        }
                    ],
                    "Connective": "OR"
                }
            },
            {
                "CompressionAction": {
                    "CompressionFormat": "default",
                    "CompressionTarget": "*",
                    "CompressionType": [
                        "gzip",
                        "br"
                    ],
                    "MinFileSizeKB": 488
                }
            }
        ]
    },
    "VideoDrag": {
        "Switch": true
    },
    "FollowRedirect": true,
    "OriginArg": [
        {
            "Condition": {
                "Connective": "",
                "ConditionRule": [
                    {
                        "Type": "url",
                        "Object": "filetype",
                        "Operator": "match",
                        "Value": "shtml;css"
                    }
                ]
            },
            "OriginArgAction": {
                "OriginArgComponents": [
                    {
                        "Object": "queryString",
                        "Action": "includePart",
                        "Subobject": "param10"
                    }
                ]
            }
        },
        {
            "Condition": {
                "Connective": "",
                "ConditionRule": [
                    {
                        "Type": "url",
                        "Object": "directory",
                        "Operator": "match",
                        "Value": "/"
                    }
                ]
            },
            "OriginArgAction": {
                "OriginArgComponents": [
                    {
                        "Object": "queryString",
                        "Action": "include",
                        "Subobject": "*"
                    }
                ]
            }
        }
    ],
    "Range": {
        "Switch": true,
        "RangeSize": 1,
        "Unit": "MB"
    },
    "OriginResponseHeader": [
        {
            "OriginResponseHeaderAction": {
                "OriginResponseHeaderInstances": [
                    {
                        "Action": "delete",
                        "Key": "Access-Control-Allow-Credentials",
                        "Value": "",
                        "ValueType": ""
                    },
                    {
                        "Action": "set",
                        "Key": "Access-Control-Expose-Headers",
                        "Value": "w3erwqr",
                        "ValueType": "constant",
                        "Object": "all_request"
                    },
                    {
                        "Action": "set",
                        "Key": "Access-Control-Allow-Methods",
                        "Value": "aasdf",
                        "ValueType": "constant",
                        "Object": "default"
                    }
                ]
            }
        }
    ],
    "OriginRetry": {
        "Switch": true,
        "StatusCode": "400;5xx"
    },
    "OriginSni": {
        "Switch": true,
        "SniDomain": "sni.example.com"
    },
    "OriginRewrite": {
        "Switch": true,
        "OriginRewriteRule": [
            {
                "OriginRewriteAction": {
                    "SourcePath": "^/a(1,2)(.*)g$",
                    "TargetPath": "/food/$1",
                    "RewriteType": "rewrite_path"
                }
            },
            {
                "OriginRewriteAction": {
                    "SourcePath": "^/aaa/(.*),txt\\?param=(.*)",
                    "TargetPath": "/life/$1?size=$2",
                    "RewriteType": "rewrite_url"
                }
            }
        ]
    },
    "RequestHeader": [
        {
            "RequestHeaderAction": {
                "RequestHeaderInstances": [
                    {
                        "Action": "delete",
                        "Key": "o-header2",
                        "Value": "",
                        "ValueType": ""
                    },
                    {
                        "Action": "set",
                        "Key": "o-header1",
                        "Value": "asdfas",
                        "ValueType": "constant"
                    }
                ]
            }
        }
    ],
    "Timeout": {
        "Switch": true,
        "TimeoutRules": [
            {
                "TimeoutAction": {
                    "TcpTimeout": 20,
                    "HttpTimeout": 888
                }
            }
        ]
    },
    "OriginPreconnect": {
        "Switch": true
    },
    "SmartOriginRouting": {
        "Switch": true
    },
    "OriginRange": true
}
```


<span id="返回示例"></span>
## 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2025081906410106F4CE0C4C8141A3CBF2",
        "Action": "AddCdnDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ResourceIds": [
            "www.example.com"
        ]
    }
}
```
