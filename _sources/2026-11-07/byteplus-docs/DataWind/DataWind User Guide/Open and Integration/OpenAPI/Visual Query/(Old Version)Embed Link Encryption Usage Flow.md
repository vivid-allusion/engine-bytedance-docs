---
title: "(Old Version)Embed Link Encryption Usage Flow"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Old_Version_Embed_Link_Encryption_Usage_Flow"
---

The private deployment of this product supports encrypting Chart or Dashboard embedded links into short URLs. Users can add, delete, modify, check, and apply encrypted links through OpenAPI. The following will provide you with a detailed introduction to the use of forward encryption.

<span id="_1-概述"></span>
# Prerequisite

Before you use the interface described in this article, please understand the calling method and complete the **Token application** steps. Please read the details [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_2-open-api对加密链接进行增删改查"></span>
# Add, delete and modify encrypted links

<span id="_2-2-生成短链接"></span>
## Generate short URL

<span id="ca95b07a"></span>
### **Request description**


* Request method: POST

* Request description: `{{domain}}/aeolus/api/v3/open/embedUrl/shortUrl`


<span id="c569a7ed"></span>
### **Request parameters**


|parameter |type |Is it required? |sample value |describe |
|---|---|---|---|---|
|fullUrl |string |Yes |"https://xxx.com/#/dashboard/123?appId=456" |Full Chart or Dashboard link address, get it and view it.[Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding) |
|zone |array |Yes |["z1", "z2"] |The network segment that is allowed to be accessed cannot be empty, such as there is no fillable array |
|descr |string |Yes |“description” |Add descriptive information for the generated short URL |


<span id="7a1c3aa5"></span>
### Request example

```JSON
{
    # 完整链接地址
    "fullUrl": “https://xxx.com/#/dashboard/123?appId=456”,
    # 允许访问的网段，不能为空或者空数组
    "zone": ["z1", "z2"],
    # 描述信息
    "descr": “description”
}
```


<span id="a6baa868"></span>
### **Return parameters**


|parameter |type |sample value |describe |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* The failure status code includes<br><br>   * `Aeolus/embed/domainAdminOnly`: accessible only to system admin<br><br>   * `Aeolus/embed/embedUrlMustHasParam`: The embedded link must contain xxx = xxx format parameters<br><br>   * `Aeolus/embed/embedUrlOnlySupportDashboardOrReport`: Only supports Dashboard/Chart<br><br>   * `Aeolus/openapiClient/tokenExpired`: token expires<br><br>   * `Aeolus/parameter/absent`: Missing necessary parameters, such as `fullUrl` |
|data |object | |Exists only when successful, including:<br><br><br>* `ID`: short URL followed by a unique ID (e.g. 6)<br><br>* `ShortUrl`: generated short URL followed by string |
|msg |string |"Success." |* Shows "success" when successful.<br><br>* Display the corresponding error description on failure |
|extra_msg |object | |It only exists when it fails, and different error types contain different details.<br><br><br>* Missing parameters `params`mark missing fields (such as `fullUrl`)<br><br>* Other error types This parameter is an empty object `{}` |
|queryHistoryId |int |0 |Query history ID, used to identify the Query history |


<span id="55d7a00e"></span>
### Back to example

```json
# 请求成功
{
    "code": "aeolus/ok",
    "data": {
        # 短链接唯一id
        "id": 6,
        # 短链接
        "shortUrl": "pgJJ96KV9N91NtosFd5AXViWr1CKf4d4"
    },
    "msg": "成功"
}
# 请求失败（当code不为"aeolus/ok"，请求就认为失败）
{
    "code": "aeolus/embed/domainAdminOnly",
    "extra_msg": {},
    "msg": "只有系统管理员才能访问",
    "queryHistoryId": 0
}
{
    "code": "aeolus/embed/embedUrlMustHasParam",
    "extra_msg": {},
    "msg": "嵌出链接需要包含xxx=xxx形式的配置参数",
    "queryHistoryId": 0
}
{
    "code": "aeolus/embed/embedUrlOnlySupportDashboardOrReport",
    "extra_msg": {},
    "msg": "嵌出链接只支持仪表盘或仪表盘中的图表",
    "queryHistoryId": 0
}
{
    "code": "aeolus/openapiClient/tokenExpired",
    "extra_msg": {},
    "msg": "token已过期",
    "queryHistoryId": 0
}
{
    "code": "aeolus/parameter/absent",
    "extra_msg": {
        "params": "fullUrl"
    },
    "msg": "缺少必要参数",
    "queryHistoryId": 0
}
```


<span id="_2-3-修改短链接配置"></span>
## Modify short URL connection configuration

<span id="4aab3bdf"></span>
### **Request description**


* Request method: PATCH

* Request description: `{{domain}} /aeolus/api/v3/open/embedUrl/shortUrl`


<span id="99335d17"></span>
### **Request parameters**


|parameter |type |Is it required? |sample value |describe |
|---|---|---|---|---|
|id |int |No<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one id and shorturl are passed. If both are passed, you need to ensure that they match, otherwise they cannot be updated.</div><br> |1 |The short URL is connected to the unique id. For the way to get it, see **Generate a short URL** |
|shortUrl |string |No |“DPnPSuSPYwnf5tLqGoO19HM48UAuri4h” |For short URL connection, see **Generating short URL connection** |
|fullUrl |string |Yes |“https://xxx.com/#/dashboard/123?appId=456” |Full Chart or Dashboard link address, get it and view it.[Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding) |
|zone |array |Yes |["z1", "z2"] |The network segment that is allowed to be accessed cannot be empty, such as there is no fillable array |
|descr |string |Yes |“description” |Add descriptive information for the generated short URL |


<span id="2188c3c0"></span>
### Request example

```JSON
{
    # 短链接唯一id
    "id": 1,
    # 短链接
    "shortUrl": "DPnPSuSPYwnf5tLqGoO19HM48UAuri4h",
    # 以上参数至少有一个，如果两个都传，需要保证能匹配上，否则无法更新
    
    # 完整url
    "fullUrl": "https://xxx.com/#/dashboard/123?appId=789",
    # 允许访问的网段
    "zone": ["z3"],
    # 描述信息
    "descr": "新的描述"
}
```


<span id="6a3415c1"></span>
### **Return parameters**


|parameter |type |sample value |describe |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include:<br><br>   * `Aeolus/embed/notFound`: short URL connection does not exist or has been deleted<br><br>   * `Aeolus/parameter/absent`: missing necessary parameters, such as `id`<br><br>   * `Aeolus/openapiClient/tokenExpired`: token expires<br><br>   * `Aeolus/embed/embedUrlMustHasParam`: need to include xxx = xxx format parameters<br><br>   * `Aeolus/embed/embedUrlOnlySupportDashboardOrReport`: Only supports Dashboard/Chart<br><br>   * `Aeolus/embed/domainAdminOnly`: accessible only to system admin |
|data |object | |Returns empty object {} on success |
|msg |string |"Success." |* Shows "success" when successful.<br><br>* Display the corresponding error description on failure |
|extra_msg |object | |It only exists when it fails, and different error types contain different details.<br><br><br>* Missing parameters `params`mark missing fields (such as `id`)<br><br>* Other error types This parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify Query history exists only when it fails, fixed to 0, used to identify Query history |


<span id="717584fe"></span>
### Back to example

```json
# 请求成功
{
    "code": "aeolus/ok",
    "data": {},
    "msg": "成功"
}
# 请求失败，当code不为"aeolus/ok"，请求就认为失败
{
    "code": "aeolus/embed/notFound",
    "extra_msg": {},
    "msg": "短连接不存在或已被删除",
    "queryHistoryId": 0
}
{
    "code": "aeolus/parameter/absent",
    "extra_msg": {
        "params": "id"
    },
    "msg": "缺少必要参数",
    "queryHistoryId": 0
}
{
    "code": "aeolus/openapiClient/tokenExpired",
    "extra_msg": {},
    "msg": "token已过期",
    "queryHistoryId": 0
}
{
    "code": "aeolus/embed/embedUrlMustHasParam",
    "extra_msg": {},
    "msg": "嵌出链接需要包含xxx=xxx形式的配置参数",
    "queryHistoryId": 0
}
{
    "code": "aeolus/embed/embedUrlOnlySupportDashboardOrReport",
    "extra_msg": {},
    "msg": "嵌出链接只支持仪表盘或仪表盘中的图表",
    "queryHistoryId": 0
}
{
    "code": "aeolus/embed/domainAdminOnly",
    "extra_msg": {},
    "msg": "只有系统管理员才能访问",
    "queryHistoryId": 0
}
```


<span id="_2-4-失效短连接"></span>
## Failed short connection

<span id="2e6b8b79"></span>
### **Request description**


* Request method: PATCH

* Request description: `{{domain}} /aeolus/api/v3/open/embedUrl/disableShortUrl`


<span id="42fe8d23"></span>
### **Request parameters**


|parameter |type |Is it required? |sample value |describe |
|---|---|---|---|---|
|id |int |No<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one id and shorturl are passed. If both are passed, you need to ensure that they match, otherwise they cannot be updated.</div><br> |1 |The short URL is connected to the unique id. For the way to get it, see **Generate a short URL** |
|shortUrl |string |No |“DPnPSuSPYwnf5tLqGoO19HM48UAuri4h” |For short URL connection, see **Generating short URL connection** |


<span id="5ed93754"></span>
### Request example

```JSON
{
    # 短链接唯一id
    "id": 1,
    # 短链接
    "shortUrl": "DPnPSuSPYwnf5tLqGoO19HM48UAuri4h",
    # 以上参数至少有一个，如果两个都传，需要保证能匹配上，否则无法更新
}
```


<span id="9b460353"></span>
### **Return parameters**


|parameter |type |sample value |describe |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include:<br><br>   * `Aeolus/embed/domainAdminOnly`: accessible only to system admin<br><br>   * `Aeolus/openapiClient/tokenExpired`: token expires<br><br>   * `Aeolus/embed/notFound`: short URL connection does not exist or has been deleted |
|data |object |{} |Returns empty object {} on success |
|msg |string |"Success." |* Shows "success" when successful.<br><br>* Display the corresponding error description on failure |
|extra_msg |object |{} |It only exists when it fails, and different error types contain different details.<br><br><br>* Missing parameters `params`mark missing fields (such as `id`)<br><br>* Other error types This parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify Query history exists only when it fails, used to identify Query history |


<span id="47405ecd"></span>
### Back to example

```json
# 请求成功
{
    "code": "aeolus/ok",
    "data": {},
    "msg": "成功"
}
# 请求失败，当code不为"aeolus/ok"，请求就认为失败
{
    "code": "aeolus/embed/domainAdminOnly",
    "extra_msg": {},
    "msg": "只有系统管理员才能访问",
    "queryHistoryId": 0
}
{
    "code": "aeolus/openapiClient/tokenExpired",
    "extra_msg": {},
    "msg": "token已过期",
    "queryHistoryId": 0
}
{
    "code": "aeolus/embed/notFound",
    "extra_msg": {},
    "msg": "短连接不存在或已被删除",
    "queryHistoryId": 0
}
```


<span id="_2-5-生效短连接"></span>
## Active short connection

<span id="4f35723b"></span>
### Request description


* Request method: PATCH

* Request description: `{{domain}} /aeolus/api/v3/open/embedUrl/enableShortUrl`


<span id="8b39d52e"></span>
### **Request parameters**


|name |type |Required |sample value |describe |
|---|---|---|---|---|
|id |int |No<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one id and shorturl are passed. If both are passed, you need to ensure that they match, otherwise they cannot be updated.</div><br> |1 |The short URL is connected to the unique id. For the way to get it, see **Generate a short URL** |
|shortUrl |string |No |“DPnPSuSPYwnf5tLqGoO19HM48UAuri4h” |For short URL connection, see **Generating short URL connection** |


<span id="0267ecfe"></span>
### Request example

```JSON
{
    # 短链接唯一id
    "id": 1,
    # 短链接
    "shortUrl": "DPnPSuSPYwnf5tLqGoO19HM48UAuri4h",
    # 以上参数至少有一个，如果两个都传，需要保证能匹配上，否则无法更新
}
```


<span id="f43896b2"></span>
### **Return parameters**


|parameter |type |sample value |describe |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include:<br><br>   * `Aeolus/embed/domainAdminOnly`: accessible only to system admin<br><br>   * `Aeolus/openapiClient/tokenExpired`: token expires<br><br>   * `Aeolus/embed/notFound`: short URL connection does not exist or has been deleted |
|data |object |{} |Returns empty object {} on success |
|msg |string |"Success." |* Shows "success" when successful.<br><br>* Display the corresponding error description on failure |
|extra_msg |object |{} |It only exists when it fails, and different error types contain different details.<br><br><br>* Missing parameters `params`mark missing fields (such as `id`)<br><br>* Other error types This parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify Query history exists only when it fails, used to identify Query history |


<span id="98921a6d"></span>
### Back to example

```json
# 请求成功
{
    "code": "aeolus/ok",
    "data": {},
    "msg": "成功"
}
# 请求失败（当code不为"aeolus/ok"，请求就认为失败）
{
    "code": "aeolus/embed/domainAdminOnly",
    "extra_msg": {},
    "msg": "只有系统管理员才能访问",
    "queryHistoryId": 0
}
{
    "code": "aeolus/openapiClient/tokenExpired",
    "extra_msg": {},
    "msg": "token已过期",
    "queryHistoryId": 0
}
{
    "code": "aeolus/embed/notFound",
    "extra_msg": {},
    "msg": "短连接不存在或已被删除",
    "queryHistoryId": 0
}
```


<span id="_2-6-删除短连接"></span>
## Delete short connections

<span id="6fef8a4b"></span>
### Request description


* Request method: DELETE

* Request description: `{{domain}} /aeolus/api/v3/open/embedUrl/shortUrl`


<span id="1f1c0d13"></span>
### **Request parameters**


|name |type |Required |sample value |describe |
|---|---|---|---|---|
|id |int |No<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one id and shorturl are passed. If both are passed, you need to ensure that they match, otherwise they cannot be updated.</div><br> |1 |The short URL is connected to the unique id. For the way to get it, see **Generate a short URL** |
|shortUrl |string |No |“DPnPSuSPYwnf5tLqGoO19HM48UAuri4h” |For short URL connection, see **Generating short URL connection** |


<span id="d1620992"></span>
### Request example

```JSON
{
    # 短链接唯一id
    "id": 1,
    # 短链接
    "shortUrl": "DPnPSuSPYwnf5tLqGoO19HM48UAuri4h",
    # 以上参数至少有一个，如果两个都传，需要保证能匹配上，否则无法更新
}
```


<span id="69c243af"></span>
### **Return parameters**


|parameter |type |sample value |describe |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include:<br><br>   * `Aeolus/embed/domainAdminOnly`: accessible only to system admin<br><br>   * `Aeolus/openapiClient/tokenExpired`: token expires<br><br>   * `Aeolus/embed/notFound`: short URL connection does not exist or has been deleted |
|data |object |{} |Returns empty object {} on success |
|msg |string |"Success." |* Shows "success" when successful.<br><br>* Display the corresponding error description on failure |
|extra_msg |object |{} |It only exists when it fails, and different error types contain different details.<br><br><br>* Missing parameters `params`mark missing fields (such as `id`)<br><br>* Other error types This parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify Query history exists only when it fails, used to identify Query history |


<span id="bd9edf56"></span>
### Back to example

```json
# 请求成功
{
    "code": "aeolus/ok",
    "data": {},
    "msg": "成功"
}
# 请求失败（当code不为"aeolus/ok"，请求就认为失败）
{
    "code": "aeolus/embed/domainAdminOnly",
    "extra_msg": {},
    "msg": "只有系统管理员才能访问",
    "queryHistoryId": 0
}
{
    "code": "aeolus/openapiClient/tokenExpired",
    "extra_msg": {},
    "msg": "token已过期",
    "queryHistoryId": 0
}
{
    "code": "aeolus/embed/notFound",
    "extra_msg": {},
    "msg": "短连接不存在或已被删除",
    "queryHistoryId": 0
}
```


<span id="_2-7-获取所有短链接"></span>
## Get all short URLs

<span id="042600ba"></span>
### Request description


* Request method: GET

* Request description: `{{domain}} /aeolus/api/v3/open/embedUrl/shortUrlList`


<span id="e4c0936b"></span>
### **Return parameters**


|parameter |type |sample value |describe |
|---|---|---|---|
|code |string |"aeolus/ok" |Success status code is `aeolus/ok`; failure status code such as `aeolus/embed/domainAdminOnly`(accessible only to system admin) |
|data |array |[{},{}....] |Returns a short URL list on success, each object containing:<br><br><br>* `Ctime`: creation time (e.g. "2023\-07\-21 16:38:00")<br><br>* `Descr`: Description information (e.g. "description")<br><br>* `FullUrl`: full link (long URL with parameters)<br><br>* `ID`: Unique ID (like 3)<br><br>* `Mtime`: Last modified time<br><br>* `ShortUrl`: short URL followed by string<br><br>* `Status`: status (0 = enabled, 1 = invalid)<br><br>* `Zone`: List of active network segments (e.g. ["z1", "z2"]) |
|msg |string |"Success." |* Shows "success" when successful.<br><br>* Display the corresponding error description on failure |
|extra_msg |object |{} |It only exists when it fails, and different error types contain different details.<br><br><br>* Missing parameters `params`mark missing fields (such as `id`)<br><br>* Other error types This parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify Query history exists only when it fails, used to identify Query history |


<span id="0db3ba82"></span>
### Back to example

```json
# 请求成功
{
    "code": "aeolus/ok",
    "data": [
        {
            # 创建时间
            "ctime": "2023-07-21 16:38:00",
            # 描述
            "descr": "description",
            # 完整链接
            "fullUrl": "https://xxx.com/#/external/dashboard/123?inline=true&appId=1&sheetId=2&feature=%7B%22dashboard%22%3A%7B%22showTitle%22%3Afalse%2C%22showOwner%22%3Afalse%2C%22showActions%22%3Afalse%2C%22sheetType%22%3A%22all%22%2C%22sheetList%22%3A%5B%5D%2C%22showHeader%22%3Afalse%2C%22showFavor%22%3Afalse%2C%22actions%22%3A%5B%5D%2C%22report%22%3A%7B%22showTitle%22%3Afalse%2C%22showTips%22%3Afalse%2C%22showToolbar%22%3Afalse%2C%22showHeader%22%3Afalse%7D%2C%22sheet%22%3A%7B%7D%7D%7D",
            # 唯一id
            "id": 3,
            # 最近一次修改时间
            "mtime": "2023-07-21 16:38:12",
            # 短链接
            "shortUrl": "TsouUsnzx0iOCxacDxpldJ6OfshLKPZf",
            # 链接状态，0：启用，1：失效
            "status": 0,
            # 生效网段
            "zone": ["z1"， "z2"]
        },
        {
            "ctime": "2023-07-21 18:06:32",
            "descr": "22222",
            "fullUrl": "https://xxx.com/#/external/dashboard/123/456?inline=true&appId=1&sheetId=2&feature=%7B%22dashboard%22%3A%7B%22report%22%3A%7B%22showTitle%22%3Afalse%2C%22showTips%22%3Afalse%2C%22showToolbar%22%3Afalse%2C%22showHeader%22%3Afalse%7D%7D%7D",,
            "id": 5,
            "mtime": "2023-07-21 18:47:21",
            "shortUrl": "DPnPSuSPYwnf5tLqGoO19HM48UAuri4h",
            "status": 1,
            "zone": ["z3"]
        }
    ],
    "msg": "成功"
}
# 请求失败（当code不为"aeolus/ok"，请求就认为失败）
{
    "code": "aeolus/embed/domainAdminOnly",
    "extra_msg": {},
    "msg": "只有系统管理员才能访问",
    "queryHistoryId": 0
}
```


<span id="_3-对加密链接进行嵌出应用"></span>
# Embedding applications for encrypted links

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Because there are customers set up a multi\-network area, so different <strong>domain names</strong> of the network area is inconsistent, in order to facilitate the use of multiple.</div>


<div data-tips="true" data-tips-type="warning">The domain name part <strong>does not participate in</strong> the generation of short URLs.</div>


**Specific operation steps** :


1. Make sure to embed out links.

   Example:

   * Domain Name 1: https://www.z1.com/#/dashboard/external/123?appId=456

   * Domain Name 2: https://www.z2.com/#/dashboard/external/123?appId=456

2. Get the short URL. Use Open API to generate encrypted short URLs for fully embedded links. For specific steps, see above **to add, delete and modify encrypted links** .

   Example:

   * The short URL returned by domain name 1: pgJJ96KV9N91NtosFd5AXViWr1CKf4d4

   * The short URL returned by domain name 2: DPnPSuSPYwnf5tLqGoO19HM48UAuri4h

3. Splice encrypted accessible links: "domain name" + "bi #/share/" + "short URL".

   Example:

   * Domain Name 1: https://www.z1.com/ bi #/share/pgJJ96KV9N91NtosFd5AXViWr1CKf4d4

   * Domain 2: https://www.z2.com/ bi #/share/DPnPSuSPYwnf5tLqGoO19HM48UAuri4h


**Examples before and after encryption** :


* Before encryption: https://www.z1.com/#/dashboard/external/123?appId=456

* After encryption: https://www.z1.com/ bi #/share/pgJJ96KV9N91NtosFd5AXViWr1CKf4d4
