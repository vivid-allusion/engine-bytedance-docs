---
title: "CheckCdnDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CheckCdnDomain_zh-cn"
---

对指定域名进行所有权校验。在调用此 API 之前，请确保您已按照 CDN 控制台提示在域名 DNS 服务提供商处创建了相应的 TXT 记录。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=CheckCdnDomain&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `CheckCdnDomain`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示一个待校验的域名，可以是泛域名。 |`www.example.com` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Status |String |表示校验结果。该参数有以下取值：<br><br><br>* `fail`：表示校验未通过。<br><br>* `success`：表示校验通过。 |`fail` |
|ErrorMsg |String |表示校验未通过的原因。如果 `Status` 是 `success`，该参数值是空（""）。 |`some reason` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=CheckCdnDomain&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20241206143123375BE43944CA95D1969A",
        "Action": "CheckCdnDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ErrorMsg": "some error",
        "Status": "fail"
    }
}
```


&nbsp;
