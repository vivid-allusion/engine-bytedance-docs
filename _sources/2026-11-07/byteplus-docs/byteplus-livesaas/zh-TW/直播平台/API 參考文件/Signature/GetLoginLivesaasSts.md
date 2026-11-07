---
title: "GetLoginLivesaasSts"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetLoginLivesaasSts-zh-TW"
---

獲取 BytePlus Live 中特定帳戶的 STS 簽名，然後您可以使用 iframe 將 BytePlus Live 控制台的功能模組嵌入到您自己的頁面中。如需更多資訊，請參見[使用 iframe 嵌入控制台](https://docs.byteplus.com/en/docs/byteplus-livesaas/using-iframe-to-embed-the-console)。

## 需求

* 頻率限制：每個帳戶每分鐘 120 次請求

* 前提條件：擁有 BytePlus 帳戶或具備超級管理員角色的 IAM 使用者。如需新增 IAM 使用者的相關資訊，請參見[管理使用者、組織與角色](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。

## HTTP 請求

* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetLoginLivesaasSts&Version=2024\-01\-01

## 請求參數

### 通用參數

下列表格未包含所有通用請求參數。如需完整清單，請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

### 查詢

|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetLoginLivesaasSts` |API 操作。 |
|Version |String |是 |`2024-01-01` |此 API 操作的版本。當前版本：`2024-01-01`。 |
|FollowerUserName |String |否 |`example@gmail.com` |IAM 使用者的帳戶。支援傳遞 IAM 使用者的電子郵件地址。<br><br><br>* 若未指定此參數，則可獲取 BytePlus 帳戶的 STS 簽名。<br><br>* 若指定此參數，則可獲取 IAM 使用者的 STS 簽名。 |
|DurationSeconds |Long |否 |`6000` |簽名的過期時間。預設值：7200。單位：秒。取值範圍：[900,172800]。 |

## 回應參數

|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|StsMsg |[StsMsg](https://docs.byteplus.com/en/docs/11/113523#stsmsg) 物件 |`-` |STS 簽名資訊。 |
|LoginLivesaasToken |String |`49e0***Y` |BytePlus Live token。 |

### StsMsg

|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|AccessKeyId |String |`AKTPODg0MzV****2ZDcxMDg` |臨時 AccessKey ID（AK）。 |
|SecretAccessKey |String |`TVRNNVlqRmxPR1****mRoTkdWbE1ESQ==` |臨時 Secret Access Key（SK）。 |
|SessionToken |String |`STSeyJBY2NvdW50SW****mNlc2hpYXNzdW1lIn0=` |使用臨時憑證時所需的 Token。 |
|ExpiredTime |String |`2024-07-16T16:14:30+08:00` |過期時間，遵循 RFC3339 格式，時區為 UTC+8，精確到秒。 |

## 範例

### 請求範例

```json
GET https://livesaas.byteplusapi.com/?Action=GetLoginLivesaasSts&Version=2024-01-01&FollowerUserName=+86188xxxxx1234&DurationSeconds=6000
```

### 回應範例

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

## 錯誤碼

如需常見錯誤碼清單，請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
