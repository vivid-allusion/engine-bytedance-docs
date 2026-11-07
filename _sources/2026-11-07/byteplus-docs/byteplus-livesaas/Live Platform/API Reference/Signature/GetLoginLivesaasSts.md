---
title: "GetLoginLivesaasSts"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts"
---

Gets the STS signature for a specific account in BytePlus Live, and then you can use an iframe to embed functional modules of the BytePlus Live console into your own page. For more information, see [Using an iframe to embed the console](https://docs.byteplus.com/en/docs/byteplus-livesaas/using-iframe-to-embed-the-console).

## Requirements

* Rate limit: 120 requests per minute per account

* Prerequisite: A BytePlus account or an IAM user with the super administrator role. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).

## HTTP request

* Method: GET

* Endpoint: https://livesaas.byteplusapi.com/?Action=GetLoginLivesaasSts&Version=2024\-01\-01

## Request parameters

### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetLoginLivesaasSts` |API operation. |
|Version |String |Yes |`2024-01-01` |The version of this API operation. Current version: `2024-01-01`. |
|FollowerUserName |String |No |`example@gmail.com` |The account of an IAM user. Supports passing the email address of the IAM user.<br><br><br>* If this parameter is not specified, you can get the STS signature for the BytePlus account.<br><br>* If this parameter is specified, you can get the STS signature for the IAM user. |
|DurationSeconds |Long |No |`6000` |The expiration time of the signature. Default value: 7200. Unit: seconds. Value range: [900,172800]. |

## Response parameters

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StsMsg |Object of [StsMsg](https://docs.byteplus.com/en/docs/11/47198#stsmsg) |`-` |STS signature information. |
|LoginLivesaasToken |String |`49e0***Y` |BytePlus Live token. |

### StsMsg

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AccessKeyId |String |`AKTPODg0MzV****2ZDcxMDg` |Temporary AccessKey ID (AK). |
|SecretAccessKey |String |`TVRNNVlqRmxPR1****mRoTkdWbE1ESQ==` |Temporary Secret Access Key (SK). |
|SessionToken |String |`STSeyJBY2NvdW50SW****mNlc2hpYXNzdW1lIn0=` |Token required when using temporary credentials. |
|ExpiredTime |String |`2024-07-16T16:14:30+08:00` |Expiration time, which follows the RFC3339 format in the UTC+8 time zone and is accurate to the second. |

## Samples

### Sample request

```json
GET https://livesaas.byteplusapi.com/?Action=GetLoginLivesaasSts&Version=2024-01-01&FollowerUserName=+86188xxxxx1234&DurationSeconds=6000
```

### Sample response

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

## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
