---
title: "Common error codes of BytePlus OpenAPI"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For product\-specific error codes, please refer to the API reference documentation of the target product.</div>


The common error codes of BytePlus OpenAPI are as follows:


|**Name** |**CodeN** |**Message** |**Description** |**Status code** |
|---|---|---|---|---|
|MissingParameter |100002 |The request is missing %s parameter. |The required key parameter is missing, such as `Action` and `Version`. |400 |
|MissingAuthenticationToken |100003 |Request is missing Authentication Token. |The required authentication information is missing. |401 |
|MissingRequestInfo |100004 |The request is missing %s information. |The required request information is missing, such as `Access Key`, `Service`, `Region`, etc. |400 |
|MissingSignature |100005 |The request is missing signature. |The request signature is missing. |401 |
|InvalidTimestamp |100006 |The signature of the request is expired. |The request signature has expired or the signing time is not valid. |400 |
|ServiceNotFound |100007 |This service[%s] not found. |The requested service does not exist, or the specified service name is incorrect. |404 |
|InvalidActionOrVersion |100008 |Could not find operation %s for version %s. |The requested API operation does not exist, or the specified operation name is incorrect. |404 |
|InvalidAccessKey |100009 |The accesskey [%s] included in the request is invalid. |The `Access Key` included in the request is not valid. |401 |
|SignatureDoesNotMatch |100010 |The request signature we calculated does not match the signature you provided. Check your Secret Access Key and signing method. Consult the service documentation for details. |The generated signature is not valid. |401 |
|LackPolicy |100012 |Request was rejected because of lack of policy. |The sub\-account does not have the permission to access the resources. |403 |
|AccessDenied |100013 |User is not authorized to perform: %s on resource: %s. |The sub\-account does not have the permission to perform the request. |403 |
|InternalError |100014 |Service has some internal Error. Pls Contact With Admin. |Internal error. |500 |
|FailToConnect |100015 |Top Fail to Connect to Internal Service. |User authorization is verified, but the service connection failed. |502 |
|InternalServiceTimeout |100016 |Internal Service is timeout. Pls Contact With Admin. |Internal service timeout. |504 |
|FlowLimitExceeded |100018 |Request was rejected because the request speed of this openAPI is beyond the current flow control limit. |Requests exceed the traffic control limit. |429 |
|ServiceUnavailableTemp |100019 |Service is busy, please try again later. |The service is busy. Please try again later. |503 |
|MethodNotAllowed |100020 |HTTP Method Not Allowed. |The HTTP method is not supported. |405 |
|InternalServiceError |100023 |Service has some internal Error. Pls Contact With Admin. |The service has an internal error. Please contact the technical support. |502 |
|InvalidAuthorization |100024 |Invalid 'Authorization' header, Pls check authorization header. |The format of the `Authorization` header is not valid. |400 |
|InvalidCredential |100025 |Invalid credential in 'Authorization', Pls check credential in authorization header. |The format of the `Credential` in the `Authorization` header is not valid. |400 |
|InvalidSecretToken |100026 |Invalid secret token, msg: %s. |The secret token (STS or STS2) is not valid due to incorrect signature or expiry. |401 |
