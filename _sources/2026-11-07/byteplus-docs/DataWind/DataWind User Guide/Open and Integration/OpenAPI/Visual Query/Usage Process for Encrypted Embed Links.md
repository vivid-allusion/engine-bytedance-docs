---
title: "Usage Process for Encrypted Embed Links"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Usage_Process_for_Encrypted_Embed_Links"
---

The on\-premises deployment version of this product supports encrypting chart or dashboard embed links into short links. Users can use OpenAPI to add, delete, update, query, apply, and perform other operations on encrypted links. The following section provides a detailed introduction to the usage process for encrypted embed links.

<span id="7d9b6c13"></span>
# Prerequisites

Before using the interfaces described in this document, please first understand how to invoke them and complete the **Token application** step. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="6275d989"></span>
# Perform CRUD operations on encrypted links

<span id="e98cec08"></span>
## Generate a short link

<span id="cfbfd734"></span>
### **Request description**


* Request method: POST

* Request URL: `{{domain}}/aeolus/api/v3/open/embedUrl/shortUrl`


<span id="1ce480fb"></span>
### **Request parameters**


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|fullUrl |string |Yes |"https://xxx.com/#/dashboard/123?appId=456" |The complete chart or dashboard link address. For how to obtain, see [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding) |
|zone |array |Yes |["z1", "z2"] |The allowed network segments for access. Cannot be empty. If none, fill in an empty array. |
|descr |string |Yes |“description” |Add description information for the generated short link |


<span id="af13dc62"></span>
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


<span id="4452890e"></span>
### **Response parameters**


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include<br><br>   * `aeolus/embed/domainAdminOnly`: Only system administrators can access<br><br>   * `aeolus/embed/embedUrlMustHasParam`: The embedded link must contain a parameter in the format xxx=xxx<br><br>   * `aeolus/embed/embedUrlOnlySupportDashboardOrReport`: Only dashboard or chart embedding is supported<br><br>   * `aeolus/openapiClient/tokenExpired`: Token expired<br><br>   * `aeolus/parameter/absent`: Missing required parameter, such as `fullUrl` |
|data |object | |Present only on success, includes:<br><br><br>* `id`: Unique ID of the short link (for example, 6)<br><br>* `shortUrl`: The generated short link string |
|msg |string |"Success" |* Displays "Success" on success<br><br>* Displays the corresponding error description on failure |
|extra_msg |object | |Present only on failure; different error types contain different details:<br><br><br>* When a parameter is missing, `params` indicates the missing field (for example, `fullUrl`)<br><br>* For other error types, this parameter is an empty object `{}` |
|queryHistoryId |int |0 |Query history ID, used to identify the query history |


<span id="29944ec4"></span>
### Response example

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


<span id="c9631d29"></span>
## Modify short link configuration

<span id="9b8f1657"></span>
### **Request description**


* Request method: PATCH

* Request URL: `{{domain}} /aeolus/api/v3/open/embedUrl/shortUrl`


<span id="8331eb03"></span>
### **Request parameters**


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|id |int |No<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one of id or shorturl must be provided. If both are provided, they must match; otherwise, the update cannot proceed.</div><br> |1 |Unique short link ID. For how to obtain, see **Get all short links** below |
|shortUrl |string |No |“DPnPSuSPYwnf5tLqGoO19HM48UAuri4h” |Short link. For how to obtain, see **Get all short links** below |
|fullUrl |string |Yes |“https://xxx.com/#/dashboard/123?appId=456” |The complete chart or dashboard link address. For how to obtain, see [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding) |
|zone |array |Yes |["z1", "z2"] |Allowed network segments for access. Cannot be empty; if none, an empty array can be provided |
|descr |string |Yes |“description” |Add description information for the generated short link |


<span id="2c9a7fd8"></span>
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


<span id="5318f623"></span>
### **Response parameters**


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include:<br><br>   * `aeolus/embed/notFound`: The short link does not exist or has been deleted<br><br>   * `aeolus/parameter/absent`: Missing required parameter, such as `id`<br><br>   * `aeolus/openapiClient/tokenExpired`: Token expired<br><br>   * `aeolus/embed/embedUrlMustHasParam`: Must contain a parameter in the format xxx=xxx<br><br>   * `aeolus/embed/embedUrlOnlySupportDashboardOrReport`: Only dashboard or chart embedding is supported<br><br>   * `aeolus/embed/domainAdminOnly`: Only system administrators can access |
|data |object | |Returns an empty object {} on success |
|msg |string |"Success" |* Displays "Success" on success<br><br>* Displays the corresponding error description on failure |
|extra_msg |object | |Present only on failure; different error types contain different details:<br><br><br>* When a parameter is missing, `params` indicates the missing field (for example, `id`)<br><br>* For other error types, this parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify the query history |


<span id="91bf79c1"></span>
### Response example

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


<span id="e33eedba"></span>
## Disable short link

<span id="1c685062"></span>
### **Request description**


* Request method: PATCH

* Request URL: `{{domain}} /aeolus/api/v3/open/embedUrl/disableShortUrl`


<span id="77adab77"></span>
### **Request parameters**


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|id |int |No<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one of id or shorturl must be provided. If both are provided, they must match; otherwise, the update cannot proceed.</div><br> |1 |Unique short link ID. For how to obtain, see **Get all short links** below |
|shortUrl |string |No |“DPnPSuSPYwnf5tLqGoO19HM48UAuri4h” |Short link. For how to obtain, see **Get all short links** below |


<span id="3308fa7c"></span>
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


<span id="7f5a60c5"></span>
### **Response parameters**


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include:<br><br>   * `aeolus/embed/domainAdminOnly`: Accessible only to system administrators<br><br>   * `aeolus/openapiClient/tokenExpired`: Token expired<br><br>   * `aeolus/embed/notFound`: The short link does not exist or has been deleted |
|data |object |{} |Returns an empty object {} when successful |
|msg |string |"Success" |* Displays "Success" when successful<br><br>* Displays the corresponding error description when failed |
|extra_msg |object |{} |Present only when failed; different error types contain different details:<br><br><br>* When parameters are missing, `params` indicates the missing fields (such as `id`)<br><br>* For other error types, this parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify query history |


<span id="6ba1b72a"></span>
### Response example

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


<span id="182dcbff"></span>
## Enable short link

<span id="52e13294"></span>
### Request description


* Request method: PATCH

* Request URL: `{{domain}} /aeolus/api/v3/open/embedUrl/enableShortUrl`


<span id="55bf2cc8"></span>
### **Request parameters**


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|id |int |No<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one of id or shorturl must be provided. If both are provided, they must match; otherwise, the update cannot proceed.</div><br> |1 |Unique ID of the short link. See below **Get all short links** for how to obtain it |
|shortUrl |string |No |“DPnPSuSPYwnf5tLqGoO19HM48UAuri4h” |Short link. See below **Get all short links** for how to obtain it |


<span id="6e5d04d8"></span>
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


<span id="e7d01c09"></span>
### **Response parameters**


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include:<br><br>   * `aeolus/embed/domainAdminOnly`: Accessible only to system administrators<br><br>   * `aeolus/openapiClient/tokenExpired`: Token expired<br><br>   * `aeolus/embed/notFound`: The short link does not exist or has been deleted |
|data |object |{} |Returns an empty object {} when successful |
|msg |string |"Success" |* Displays "Success" when successful<br><br>* Displays the corresponding error description when failed |
|extra_msg |object |{} |Present only when failed; different error types contain different details:<br><br><br>* When parameters are missing, `params` indicates the missing fields (such as `id`)<br><br>* For other error types, this parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify query history |


<span id="6084f53c"></span>
### Response example

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


<span id="3210e146"></span>
## Delete short link

<span id="a3d203fe"></span>
### Request description


* Request method: DELETE

* Request URL: `{{domain}} /aeolus/api/v3/open/embedUrl/shortUrl`


<span id="e0dc86a7"></span>
### **Request parameters**


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|id |int |No<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">At least one of id or shorturl must be provided. If both are provided, they must match; otherwise, the update cannot proceed.</div><br> |1 |Unique ID of the short link. See below **Get all short links** for how to obtain it |
|shortUrl |string |No |“DPnPSuSPYwnf5tLqGoO19HM48UAuri4h” |Short link. See below **Get all short links** for how to obtain it |


<span id="fc8e7bf9"></span>
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


<span id="e8701db9"></span>
### **Response parameters**


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |* The success status code is `aeolus/ok`<br><br>* Failure status codes include:<br><br>   * `aeolus/embed/domainAdminOnly`: Accessible only to system administrators<br><br>   * `aeolus/openapiClient/tokenExpired`: Token expired<br><br>   * `aeolus/embed/notFound`: The short link does not exist or has been deleted |
|data |object |{} |Returns an empty object {} when successful |
|msg |string |"Success" |* Displays "Success" when successful<br><br>* Displays the corresponding error description when failed |
|extra_msg |object |{} |Present only when failed; different error types contain different details:<br><br><br>* When parameters are missing, `params` indicates the missing fields (such as `id`)<br><br>* For other error types, this parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify query history |


<span id="3a18a22a"></span>
### Response example

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


<span id="2a67c850"></span>
## Retrieve all short links

<span id="bee81c3c"></span>
### Request description


* Request method: GET

* Request URL: `{{domain}} /aeolus/api/v3/open/embedUrl/shortUrlList`


<span id="95325a8e"></span>
### **Response parameters**


|Parameter |Type |Example value |Description |
|---|---|---|---|
|code |string |"aeolus/ok" |The success status code is `aeolus/ok`; failure status codes include `aeolus/embed/domainAdminOnly` (accessible only to system administrators) |
|data |array |[{},{}....] |On success, returns a list of short links, with each object containing:<br><br><br>* `ctime`: Creation time (for example, "2023\-07\-21 16:38:00")<br><br>* `descr`: Description (for example, "description")<br><br>* `fullUrl`: Full URL (long URL with parameters)<br><br>* `id`: Unique ID (for example, 3)<br><br>* `mtime`: Last modified time<br><br>* `shortUrl`: Short link string<br><br>* `status`: Status (0 = enabled, 1 = invalid)<br><br>* `zone`: List of valid network segments (for example, ["z1", "z2"]) |
|msg |string |"Success" |* Displays "Success" on success<br><br>* Displays the corresponding error description on failure |
|extra_msg |object |{} |Present only on failure; different error types contain different details:<br><br><br>* When parameters are missing, `params` indicates the missing fields (for example, `id`)<br><br>* For other error types, this parameter is an empty object {} |
|queryHistoryId |int |0 |Query history ID, used to identify the query history |


<span id="00011ffc"></span>
### Response example

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


<span id="6f78f1f4"></span>
# Apply encrypted embed links

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Because some customers have multiple network zones and domain names differ between zones, the domain name part is not included in short link generation to facilitate use in multiple scenarios.</div>


**Detailed operation steps**:


1. Identify the embed link.

   Example:

   * Domain 1: https://www.z1.com/#/dashboard/external/123?appId=456

   * Domain 2: https://www.z2.com/#/dashboard/external/123?appId=456

2. Obtain the short link. Use the Open API to generate an encrypted short link for the complete embed link. For detailed steps, see **Perform CRUD operations on encrypted links** above.

   Example:

   * Short link returned by Domain 1: pgJJ96KV9N91NtosFd5AXViWr1CKf4d4

   * Short link returned by Domain 2: DPnPSuSPYwnf5tLqGoO19HM48UAuri4h

3. Construct the encrypted access link: "Domain" + "bi#/share/" + "short link".

   Example:

   * Domain 1: https://www.z1.com/bi#/share/pgJJ96KV9N91NtosFd5AXViWr1CKf4d4

   * Domain 2: https://www.z2.com/bi#/share/DPnPSuSPYwnf5tLqGoO19HM48UAuri4h


**Example before and after encryption**:


* Before encryption: https://www.z1.com/#/dashboard/external/123?appId=456

* After encryption: https://www.z1.com/bi#/share/pgJJ96KV9N91NtosFd5AXViWr1CKf4d4
