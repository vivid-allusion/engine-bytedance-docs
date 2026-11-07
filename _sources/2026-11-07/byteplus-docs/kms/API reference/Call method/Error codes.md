---
title: "Error codes"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Error_codes"
---


|**Common Error Code** |**Description** |**HTTP Code** |
|---|---|---|
|MissingParameter |A key parameter is missing, such as **Action** or **Version**. |400 |
|InvalidParameter |A key parameter has an error, such as **Action** or **Version**. |400 |
|InvalidKeyStatus |This operation cannot be performed on the customer master key (CMK) in the current state. For example: The [Encrypt](https://docs.byteplus.com/en/docs/6476/71323) API cannot be called for a CMK in the Disable state. |400 |
|Reject.Throttling.CMK |The maximum number of calls to this CMK has been reached. |403 |
|Reject.Throttling.Action |The maximum number of API calls has been reached. |403 |
|Reject.Service.Overdue |The account is in arrears. Please top up and try again. |403 |
|Reject.Service.Opening |This service is being activated. Try again later. |403 |
|Not Found |The resource is not found. For example: The CMK you are searching for does not exist. |404 |
|Conflict |A conflict occurs while creating the resource. For example: This error occurs when you try to create an existing keyring or CMK. |409 |
|UndefinedError |An unknown error occurred. |500 |
