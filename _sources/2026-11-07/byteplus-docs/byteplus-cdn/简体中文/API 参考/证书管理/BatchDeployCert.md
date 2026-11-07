---
title: "BatchDeployCert"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/BatchDeployCert_zh-cn"
---

将指定证书与一个或者多个域名关联。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=BatchDeployCert&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `BatchDeployCert`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示一个需要与 `CertId` 关联的域名列表，列表中最多包含 50 个域名。多个域名之间使用逗号（,）分隔。<br><br>如果列表中的某个域名不在该证书的 SAN 字段中，该域名将无法与该证书关联。 |`www.example.com,img.example.com` |
|CertId |String |是 |表示待关联的证书的 ID。 |`cert-c195f679cecb4f34tj23dd8c54e6c0a2` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|DeployResult |Object[] |表示各域名的关联结果。 | |
|Domain |String |表示 `Domain` 中的一个域名。 |`www.example.com` |
|Status |String |表示关联是否成功。该参数的取值如下：<br><br><br>* `success`：表示关联成功。<br><br>* `fail`：表示关联失败。失败原因在 `ErrorMsg` 参数中描述。 |`success` |
|ErrorMsg |String |表示关联失败的原因。如果 `Status` 是 `success`，该参数值为空（""）。 |`some error` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=BatchDeployCert&Version=2021-03-01
{
    "Domain": "www.example.com,docs.example.com",
    "CertId": "cert-a4827a17f0964010a199e74f6e6b6a52"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2025091106370814AF152ABDC20800D531",
        "Action": "BatchDeployCert",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DeployResult": [
            {
                "Domain": "www.example.com",
                "ErrorMsg": "",
                "Status": "success"
            },
            {
                "Domain": "docs.example.com",
                "ErrorMsg": "",
                "Status": "success"
            }
        ]
    }
}
```


&nbsp;
