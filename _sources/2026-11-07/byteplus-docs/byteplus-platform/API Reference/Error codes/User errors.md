---
title: "User errors"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-user-1"
---

Below are user related error codes.


|**Error** |**Message** |**HTTP Status Code** |
|---|---|---|
|UserNotExist |User '%s' cannot be found. |404 |
|UserAlreadyExists |User '%s' already exists. |409 |
|InvalidUserName |Invalid UserName '%s', err: '%s'. |400 |
|InvalidNewUserName |Invalid NewUserName '%s', err: '%s'. |400 |
|InvalidDisplayName |Invalid DisplayName '%s', err: '%s'. |400 |
|InvalidNewDisplayName |Invalid NewDisplayName '%s', err: '%s'. |400 |
|InvalidMobilePhone |Invalid MobilePhone '%s', err: '%s'. |400 |
|InvalidMobilePhoneIsVerify |Invalid MobilePhoneIsVerify '%s', err: '%s'. |400 |
|InvalidNewMobilePhone |Invalid NewMobilePhone '%s', err: '%s'. |400 |
|InvalidEmail |Invalid Email '%s', err: '%s'. |400 |
|InvalidNewEmail |Invalid NewEmail '%s', err: '%s'. |400 |
|InvalidEmailIsVerify |Invalid EmailIsVerify '%s', err: '%s'. |400 |
|InvalidPassword |Invalid Password '%s', err: '%s'. |400 |
|UserDeleteConflictWithRole |Cannot delete user '%s' which added to role(s). |409 |
|UserDeleteConflictWithPolicy |Cannot delete user '%s' which added to policy(s). |409 |
|UserDeleteConflictWithAccessKey |Cannot delete user '%s' which added to ak(s). |409 |
|AddUserToRoleConflict |User '%s' already be added to the role '%s'. |409 |
|RemoveUserFromRoleConflict |User '%s' not be added to to the role '%s'. |409 |
|LoginProfileAlreadyExist |LoginProfile for User '%s' already exist. |409 |
|LoginProfileNotExist |LoginProfile for User '%s' not exist. |404 |
|PasswordNotMatch |Password you provided donot match password in DB. |403 |
|InvalidLoginIp |Invalid LoginIp '%s', err: '%s'. |400 |
|LoginNotAllowed |User '%s' doesn't have authority to login, please configure by IAM console |403 |
