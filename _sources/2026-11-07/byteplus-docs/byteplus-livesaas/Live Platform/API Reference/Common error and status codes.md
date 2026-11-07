---
title: "Common error and status codes"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes"
---

This topic documents common error and status codes.

<span id="common-errors-for-byteplus"></span>
## Common errors for BytePlus


|Name |Message |Description |Status Code |
|---|---|---|---|
|MissingParameter |The request is missing %s parameter. |The required key parameter is missing, such as Action and Version. |400 |
|MissingAuthenticationToken |The request is missing an Authentication Token. |The required authentication information is missing. |401 |
|MissingRequestInfo |The request is missing %s information. |The request is missing required information, such as the Access Key, Service, or Region. |400 |
|MissingSignature |The request is missing a signature. |The request signature is missing. |401 |
|InvalidTimestamp |The signature of the request is expired. |The request signature has expired or the signing time is not valid. |400 |
|ServiceNotFound |Service '%s' was not found. |The requested service does not exist, or the specified service name is incorrect. |404 |
|InvalidActionOrVersion |Could not find operation %s for version %s. |The requested API operation does not exist, or the specified operation name is incorrect. |404 |
|InvalidAccessKey |The Access Key [%s] included in the request is invalid. |The Access Key included in the request is not valid. |401 |
|SignatureDoesNotMatch |The request signature we calculated does not match the signature you provided. Check your Secret Access Key and signing method. Consult the service documentation for details. |The generated signature is not valid. |401 |
|LackPolicy |The request was rejected due to insufficient permissions. |The sub\-account does not have the permission to access the resources. |403 |
|AccessDenied |User is not authorized to perform: %s on resource: %s. |The sub\-account does not have the permission to perform the request. |403 |
|InternalError |Service has some internal Error. Pls Contact With Admin. |Internal error. |500 |
|FailToConnect |Top Fail to Connect to Internal Service. |User authorization is verified, but the service connection failed. |502 |
|InternalServiceTimeout |Internal Service is timeout. Pls Contact With Admin. |Internal service timeout. |504 |
|FlowLimitExceeded |Request was rejected because the request speed of this openAPI is beyond the current flow control limit. |Requests exceed the traffic control limit. |429 |
|ServiceUnavailableTemp |Service is busy, please try again later. |The service is busy. Please try again later. |503 |
|MethodNotAllowed |HTTP Method Not Allowed. |The HTTP method is not supported. |405 |
|InternalServiceError |Service has some internal Error. Pls Contact With Admin. |The service has an internal error. Please contact the technical support. |502 |
|InvalidAuthorization |Invalid 'Authorization' header, Pls check authorization header. |The format of the Authorization header is not valid. |400 |
|InvalidCredential |Invalid credential in 'Authorization', Pls check credential in authorization header. |The format of the Credential in the Authorization header is not valid. |400 |
|InvalidSecretToken |Invalid secret token, msg: %s. |The secret token (STS or STS2) is not valid due to incorrect signature or expiry. |401 |


<span id="common-errors-for-byteplus-live"></span>
## Common errors for BytePlus Live


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.%sInvalid |The specified parameter %s is invalid. |The parameter is invalid. Modify the value based on the specifications and try again. |
|400 |InvalidParameter.ActivityHasBeenDeleted |The specified parameter ActivityId is invalid. |The live room has been deleted. Modify the value of the `ActivityId` parameter and try again. |
|400 |InvalidParameter.ActivityNotExist |The specified parameter ActivityId is invalid. |The live room does not exist. Modify the value of the `ActivityId` parameter and try again. |
|500 |InternalError.InternalError |The request has failed due to an unknown error. |An unknown error occurred during the request processing. Contact the technical support for help. |
