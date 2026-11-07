---
title: "UpdateSiteTagAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatesitetagapiv2-zh-CN"
---

调用此 API 可更新你 BytePlus 账号下直播活动的标签信息。

<span id="8baab3a6"></span>
## 请求

<span id="dc5f59cd"></span>
### 详情


* API 接口行为：`UpdateSiteTagAPIV2`

* 请求方式：POST

* 请求 URI：`https://livesaas.byteplusapi.com/?Action=UpdateSiteTagAPIV2&Version=2020-06-01`

* 配额：每个账号每分钟 120 次查询


<span id="6e979a4a"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 接口行为。 |
|Version |String |是 |此 API 接口行为的版本。当前版本：`2020-06-01`。 |


<span id="b23059ea"></span>
### 请求体参数


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|SiteTags |Array of[Tag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2-zh-CN#Tag) |是 |所有分类标签的列表。<br><br>如需更新标签，请先调用[ListSiteTagAPIV2](https://docs.byteplus.com/byteplus-livesaas/docs/listsitetagapiv2)获取当前列表，根据需要修改值后，将完整的更新列表包含在请求中。 |
|TextSiteTags |Array of[TextTag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2-zh-CN#TextTag) |是 |所有文本标签的列表。<br><br>如需更新标签，请先调用[ListSiteTagAPIV2](https://docs.byteplus.com/byteplus-livesaas/docs/listsitetagapiv2)获取当前列表，根据需要修改值后，将完整的更新列表包含在请求中。 |


<span id="7c2f115d"></span>
#### **Tag**


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Name |String |是 |分类标签的名称。名称不能超过 50 个字符，且不能与其他分类标签名称重复。 |
|Value |Array of String |是 |标签的值数组。每个标签值不能超过 50 个字符，且在同一分类标签下必须唯一。 |
|Show |Integer |是 |已废弃。 |
|Index |Integer |是 |分类标签的索引，用于决定在 BytePlus Live 控制台的显示顺序。<br><br>取值范围：[0,19]。 |


<span id="b07ec8d0"></span>
#### **TextTag**


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Name |String |是 |文本标签的名称。名称不能超过 50 个字符，且不能与其他文本标签名称重复。 |
|Index |Integer |是 |文本标签的索引，用于标识在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)的显示顺序。<br><br>取值范围：[0,4]。 |


<span id="b52be3c9"></span>
### 请求示例

```JSON
Post https://livesaas.byteplusapi.com/?Action=UpdateSiteTagAPIV2&Version=2020-06-01
{ 
      "SiteTags":   [ 
            { 
                  "Name": "Label 1", 
                  "Value": [ 
                        "A", 
                        "B" 
                  ], 
                  "Show": 0, 
                  "Index": 0 
            }, 
           { 
                  "Name": "Label 2", 
                  "Value": [ 
                        "C", 
                        "D" 
                  ], 
                  "Show": 0, 
                  "Index": 1 
            } 
      ], 
      "TextSiteTags":   [ 
            { 
                  "Name": "Label 3", 
                  "Index": 0 
            }, 
            { 
                  "Name": "Label 4", 
                  "Index": 1 
            } 
      ] 
} 
```


<span id="be0e1229"></span>
## 返回调用结果

<span id="3e7e53c1"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Status |Boolean |表示更新是否成功。<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |


<span id="7f2c5f49"></span>
### 返回示例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "UpdateSiteTagAPIV2", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": { 
        "Status": true 
    } 
} 
```


<span id="22d08a72"></span>
## 错误码

常见错误码请参见[通用错误码与状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
