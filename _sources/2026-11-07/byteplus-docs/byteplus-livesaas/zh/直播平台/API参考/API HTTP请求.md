---
title: "API HTTP请求"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-api-http-request-zh-CN"
---

要调用BytePlus Live API，必须构建标准的HTTP请求。本指南将通过`CreateActivityAPIV2` API作为实际示例，说明API HTTP请求的基本结构，包括请求URL、请求方式和参数。

完整的HTTP请求包含三部分：


* 请求URL

* 请求方式

* 请求参数


<span id="request-url"></span>
## 请求URL

请求URL：`{URI-scheme}://{Endpoint}/?{query-string}`

下表描述了URL的组成部分。


|**组件** |**接口行为** |
|---|---|
|URI\-scheme |支持HTTP和HTTPS。出于安全考虑，建议使用HTTPS。 |
|Endpoint |API接收请求的服务端点。BytePlus Live API的端点为`livesaas.byteplusapi.com`。 |
|query\-string |包含通用请求参数和操作特定参数。<br><br>有关操作特定参数及部分通用请求参数，请参见每个API操作的详细说明。<br><br>完整的通用请求参数列表请参见[Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。 |


例如，`CreateActivityAPIV2`的请求URL如下：

```JSON
http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
```


<span id="request-methods"></span>
## 请求方式

请求方式用于指定对资源执行的操作。BytePlus Live API支持以下请求方式：


|**方式** |**接口行为** |
|---|---|
|GET |获取指定资源。公共数据可以通过请求头和查询字符串参数发送。 |
|POST |向服务器发送请求以添加资源或执行特殊操作。公共数据只能添加到请求头中。 |


`CreateActivityAPIV2`的请求方式为POST。请求行如下：

```JSON
POST http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
```


<span id="request-parameters"></span>
## 请求参数

HTTP请求包含以下类型的参数：


* 通用参数：更多信息请参见[Shared parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters)。

* API请求参数：具体API请参考相关参考主题。


<span id="request-example"></span>
## 请求示例

`CreateActivityAPIV2`的完整请求如下：

```JSON
POST http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
{
    "Name":"Live Room A",
    "LiveTime":1642668850
}
```
