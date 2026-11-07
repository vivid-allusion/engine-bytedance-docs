---
title: "BytePlus VOD shared error codes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes"
---

When you encounter an error while calling a BytePlus VOD API, use this guide to look up the error code. This document provides a comprehensive list of shared error codes, including their descriptions and corresponding HTTP status codes, to help you quickly diagnose and resolve issues.

If the API response contains the `Error` field, it indicates that the call to the API interface failed. The `Error.Code` field represents the error code.

<span id="5d8e19db"></span>
## Gateway errors


|**Error Code** |**Description** |**HTTP Code** |
|---|---|---|
|UndefinedError |Unknown error. |500 |
|MissingParameter |A required parameter such as `Action` and `Version` was missing. |400 |
|MissingAuthenticationToken |The authentication parameter such as `Auth` was missing. |401 |
|MissingRequestInfo |A required parameter for the request was missing, such as `Accesskey`, `service`, and`region`. |400 |
|MissingSignature |Missing signature result. |401 |
|InvalidTimestamp |The request has expired or the signature timestamp is in the future. |403 |
|ServiceNotFound |The requested service does not exist. |404 |
|InvalidActionOrVersion |The requested action or version does not exist. |404 |
|InvalidClientTokenId |The access key is invalid. |401 |
|SignatureDoesNotMatch |Incorrect signature result. |401 |
|LackPolicy |The sub\-user does not have the required permissions. |403 |
|AccessDenied |The permissions of the sub\-user do not support the current operation. |403 |
|InternalError |Internal error. |500 |
|FailToConnect |Service connection error. |502 |
|InternalServiceTimeout |Internal service timeout. |504 |
|FlowLimitExceeded |The request frequency is too high, exceeding the basic call rate limit. |429 |
|AccountFlowLimitExceeded |The request frequency is too high, exceeding the account call rate limit. |429 |
|ServiceUnavailableTemp |The service is temporarily unavailable. |503 |
|MethodNotAllowed |The HTTP method is invalid. |405 |
|LackProjectPolicy |Missing project permissions. |401 |
|InternalServiceError |Internal error. |502 |


<span id="6648634a"></span>
## Non\-gateway errors


|**Error Code** |**Description** |**HTTP Code** |
|---|---|---|
|InternalError |Internal error. |500 |
|InvalidAction |The interface does not exist. |404 |
|InvalidVersion |The version does not exist. |404 |
|InvalidParameter |Invalid parameter. |400 |
|InvalidDomain |Invalid domain name. |400 |
|MissingParameter |Missing parameter. |400 |
|UnsupportedProtocol |The request protocol is not supported. |400 |
|UnsupportedRegion |The region is not supported. |400 |
|UnsupportedOperation |The operation is not supported. |400 |
|RequestLimitExceeded |The number of requests exceeded the allowed limit. |429 |
|RequestForbidden |The request is prohibited. |403 |
|OperationDenied |Operation denied, the feature or service is not enabled. |403 |
|ResourceNotFound |The resource does not exist. |404 |
|ResourceInUse |The resource is in use. |409 |
|UnauthorizedOperation |The operation is not authorized. |401 |
|ServiceUnavailable |Service unavailable. |503 |
|ResourceUnavailable |The resource is temporarily unavailable. Possibly due to outstanding payment. |403 |
|ResourceInsufficient |Insufficient resources. |409 |
|QuotaInsufficient |Insufficient quota. |409 |
|ServiceTimeout |Service timeout. |408 |
|ServerIsBusy |Server is busy. |503 |
