---
title: "UpdateCustomizationViewPermissionAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatecustomizationviewpermissionapi-zh-CN"
---

调用此 API 可更新直播活动的登录链接，使您能够使用自己的账号系统管理观看和评论权限。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`UpdateCustomizationViewPermissionAPI`

* 请求方式：POST

* 请求 URI：`https://livesaas.byteplusapi.com/?Action=UpdateCustomizationViewPermissionAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|ActivityId |是 |整数 |直播活动的 ID。 |
|CustomUrl |是 |字符串 |指向您账号系统的自定义登录链接。 |
|CustomApp |否 |字符串 |自定义观看应用的名称。 |
|ErrorRedirectUrl |否 |字符串 |自定义认证失败时用于重定向的 URL。该 URL 必须包含协议。默认情况下，用户会被重定向到直播服务的默认认证失败页面。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateCustomizationViewPermissionAPI&Version=2020-06-01
{
     "ActivityId":123,
     "CustomUrl":"www.example.com" }
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|SecretKey |字符串 |用于验证观众身份的账号系统密钥。 |


<span id="Sample response"></span>
### 返回示例

```JSON
{
   "ResponseMetadata":{
     "RequestId": "201806041104200100100232280022D30",
     "Action":"UpdateCustomizationViewPermissionAPI",
     "Version":"2020-06-01",
     "Service":"livesaas",
     "Region":"ap-singapore-1" 
  },
   "Result":{
       "SecretKey":"qw***" 
  }
}
```
