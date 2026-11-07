---
title: "Federation errors"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-federation"
---

Below are federation related error codes.


|**Error** |**Message** |**HTTP Status Code** |
|---|---|---|
|IdentityProviderNoHandler |IdentityProvider '%s' has no handler function exist. |400 |
|IdentityProviderNoUserInfo |Cannot get userInfo, please try again or please contact with admin. |400 |
|IdentityProviderNotExist |IdentityProvider %s not exist |400 |
|IdentityProviderAlreadyExists |IdentityProvider %s already exist |409 |
|AppAlreadyExists |App %s already exists |409 |
|AppNotExist |App %s not exist |400 |
|AppNameAlreadyExists |AppName %s is already used |409 |
|InvalidAppName |Invalid AppName %s, err: %s |400 |
|InvalidAppID |Invalid AppID %s, err: %s |400 |
|InvalidAppSecret |Invalid AppSecret %s, err: %s |400 |
|InvalidIdpName |Invalid IdpName %s, err: %s |400 |
|InvalidIdpType |Invalid IdpType %s, err: %s |400 |
|InvalidIdpScope |Invalid IdpScope %s, err: %s |400 |
