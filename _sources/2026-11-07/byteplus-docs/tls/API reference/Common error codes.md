---
title: "Common error codes"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/common-error-codes"
---

Below are the common error codes.


|Error |HTTP status code |Message |Description |
|---|---|---|---|
|BadRequest |400 |%s |Request error, check the request parameters. |
|InvalidAccessKeyId |403 |The Access Key Id you provided does not exist in our records. |AccessKeyId is illegal, enter the correct AccessKeyId. |
|SignatureDoesNotMatch |403 |The request signature we calculated does not match the signature you provided. Check your key and signing method. |SecretKey Id is illegal or does not match the AccessKeyId, please enter the correct SecreKeyId. |
|AuthorizationQueryParametersError |403 |/ |Authentication parameter error. |
|ErrInternalServerError |500 |We encountered an unexpected server error, please try again later. |Internal server error. |
