---
title: "UpdateCountryCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCountryCluster"
---

该接口用于修改用于金丝雀发布或完全发布的集群类型。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateCountryCluster&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateCountryCluster`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|FunctionId |String |是 |您想要修改集群类型的函数ID。您可以通过调用接口[ListSparrow](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSparrow)来获取FunctionId。 |`3gyz993****` |
|ClusterType |Integer |是 |集群类型。<br><br><br>* 100：灰度发布集群<br><br>* 200：全量发布集群 |`100` |
|Countries |String[] |是 |集群所在的国家数组。 |`["Singapore"]` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST  https://cdn.byteplusapi.com?Action=UpdateCountryCluster&Version=2021-03-01
{
    "ClusterType": 200,
    "Countries": [
        "Singapore"
    ],
    "FunctionId": "3gyz993****",
}
```
