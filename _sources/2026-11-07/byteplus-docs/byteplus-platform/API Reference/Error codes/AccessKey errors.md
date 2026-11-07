---
title: "AccessKey errors"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-accesskey-1"
---

Below are AccessKey related error codes.


|**Error** |**Message** |**Http Status Code** |
|---|---|---|
|InvalidAccessKeyId |Invalid accessKeyId '%s', err: '%s' |400 |
|AccessKeyNotExist |The accessKey '%s' can not be found |404 |
|InvalidAccessKeyStatus |Invalid accessKey status: '%s', err: '%s' |400 |
|AccessKeyLimitExceeded |Exceed account accessKey quota: '%d' |409 |
|ErrorCreateAccessKey |Generate accessKey error: '%s' |400 |
|AccessKeyIsExpire |The accessKey '%s' is expired. |400 |
|SessionTokenInvalid |The session\-toke is invalid. |400 |
