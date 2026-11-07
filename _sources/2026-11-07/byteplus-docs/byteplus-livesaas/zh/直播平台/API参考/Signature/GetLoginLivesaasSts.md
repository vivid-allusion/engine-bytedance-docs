---
title: "GetLoginLivesaasSts"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetLoginLivesaasSts-zh-CN"
---

获取 BytePlus Live 中指定账号的 STS 签名，然后可以通过 iframe 将 BytePlus Live 控制台的功能模块嵌入到您的页面中。更多信息，请参见 [使用 iframe 嵌入控制台](https://docs.byteplus.com/en/docs/byteplus-livesaas/using-iframe-to-embed-the-console)。

## 要求

* 限速：每个账号每分钟最多 120 次请求

* 前提条件：需拥有 BytePlus 账号或具备超级管理员角色的 IAM 用户。关于如何添加 IAM 用户的更多信息，请参见 [管理用户、组织和角色](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。

## HTTP 请求

* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetLoginLivesaasSts&Version=2024\-01\-01

## 请求参数

### 通用参数

以下表格未包含所有通用请求参数。完整列表请参见 [通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

### Query

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetLoginLivesaasSts` |API 操作。 |
|Version |String |是 |`2024-01-01` |本 API 操作的版本。当前版本：`2024-01-01`。 |
|FollowerUserName |String |否 |`example@gmail.com` |IAM 用户的账号。支持传递 IAM 用户的邮箱地址。<br><br><br>* 若未指定该参数，则获取 BytePlus 账号的 STS 签名。<br><br>* 若指定该参数，则获取 IAM 用户的 STS 签名。 |
|DurationSeconds |Long |否 |`6000` |签名的过期时间。默认值：7200。单位：秒。取值范围：[900,172800]。 |

## 返回调用结果参数

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|StsMsg |[StsMsg](https://docs.byteplus.com/en/docs/11/113521#stsmsg) 对象 |`-` |STS 签名信息。 |
|LoginLivesaasToken |String |`49e0***Y` |BytePlus Live token。 |

### StsMsg

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|AccessKeyId |String |`AKTPODg0MzV****2ZDcxMDg` |临时 AccessKey ID（AK）。 |
|SecretAccessKey |String |`TVRNNVlqRmxPR1****mRoTkdWbE1ESQ==` |临时 Secret Access Key（SK）。 |
|SessionToken |String |`STSeyJBY2NvdW50SW****mNlc2hpYXNzdW1lIn0=` |使用临时凭证时所需的 Token。 |
|ExpiredTime |String |`2024-07-16T16:14:30+08:00` |过期时间，采用 RFC3339 格式，时区为 UTC+8，精确到秒。 |

## 示例

### 请求示例

```json
GET https://livesaas.byteplusapi.com/?Action=GetLoginLivesaasSts&Version=2024-01-01&FollowerUserName=+86188xxxxx1234&DurationSeconds=6000
```

### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetLoginLivesaasSts",
        "Version": "2024-01-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "StsMsg": {
            "AccessKeyId": "AKTPODg0MzV****2ZDcxMDg",
            "SecretAccessKey": "TVRNNVlqRmxPR1****mRoTkdWbE1ESQ==",
            "SessionToken": "STSeyJBY2NvdW50SW****mNlc2hpYXNzdW1lIn0=",
            "ExpiredTime": "2024-07-16T16:14:30+08:00"
        },
        "LoginLivesaasToken": "49e0***Y"
    }
}
```

## 错误码

常见错误码列表请参见 [常见错误码和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
