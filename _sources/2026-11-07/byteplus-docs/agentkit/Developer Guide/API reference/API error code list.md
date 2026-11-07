---
title: "API error code list"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Common_error_codes"
---

This topic describes the common error codes you may encounter when you call AgentKit APIs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For platform error codes, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes">Common error codes</a>.</div>



|**Error code** |**HTTP status code** |**Error message** |**Measure** |
|---|---|---|---|
|MissingParameter |400 |The request is missing %s parameter. |Key parameters, such as the Action and Version parameters, are missing. |
|MissingRequestInfo |400 |The request is missing %s information. |Information required for the request, such as the Accesskey, service, and region, is missing. |
|InnerApiNeedAccountInfo |400 |The inner request should have account info. |Account information is missing when you request internal services by using service AK/SK. |
|InvalidAuthorization |400 |Invalid 'Authorization' header, Pls check authorization header. |The format of the Authorization header is incorrect. Check the Authorization header. |
|InvalidCredential |400 |Invalid credential in 'Authorization', Pls check credential in authorization header. |The format of Credential in the Authorization header is incorrect. Check the format of Credential. |
|MissingAuthenticationToken |401 |Request is missing Authentication Token. |Information required for identity authentication, such as the Auth information, is missing. |
|MissingSignature |401 |The request is missing signature. |The signature result is missing. |
|InvalidAccessKey |401 |The accesskey [%s] included in the request is invalid. |The requested AK is invalid. |
|SignatureDoesNotMatch |401 |The request signature we calculated does not match the signature you provided. Check your Secret Access Key and signing method. Consult the service documentation for details. |The signature result is incorrect. |
|InvalidSecretToken |401 |Invalid secret token, msg: %s. |The incorrect STS or STS2 may stem from various errors, such as signature errors and expiration. |
|LackProjectPolicy |403 |Request was rejected because of lack of project policy. |Project permission verification is required for the request, but the current permission is invalid. |
|InvalidTimestamp |403 |The Signature of the request is expired. |The request has expired or the signature time of the request is in the future. |
|ServiceShouldCallSelfApi |403 |The service(%s) should call self\-api. |Access requests authenticated via service AK/SK can only access your own operations and public service operations. Public services such as IAM. |
|LackPolicy |403 |Request was rejected because of lack of policy. |The request is denied by default because the IAM user lacks the required permission. |
|AccessDenied |403 |User is not authorized to perform: %s on resource: %s. |The IAM user is not authorized to perform the current operation. |
|ServiceNotFound |404 |This service[%s] not found. |The requested service does not exist. |
|InvalidActionOrVersion |404 |Could not find operation %s for version %s. |The requested API does not exist. |
|MethodNotAllowed |405 |HTTP Method Not Allowed. |The HTTP method is invalid. |
|FlowLimitExceeded |429 |Request was rejected because the request speed of this openAPI is beyond the current flow control limit. |Requests are too frequent and exceed the basic rate limit. |
|UndefinedError |500 |Undefined Internal Error. Pls Contact With Admin. |This issue generally does not occur. It is a fallback error message specified during system development. |
|InternalError |500 |Service has some internal Error. Pls Contact With Admin. |An internal error occurred, such as a DB error. |
|FailToConnect |502 |Top Fail to Connect to Internal Service. |The business service cannot be connected. |
|InternalServiceError |502 |Service has some internal Error. Pls Contact With Admin. |The business services are experiencing a fault. In this context, "business" generally refers to specific services such as imagex and vod. |
|ServiceUnavailableTemp |503 |Service is busy, please try again later. |Services in a circuit\-breaking state are temporarily inaccessible. Try again later. |
|InternalServiceTimeout |504 |Internal Service is timeout. Pls Contact With Admin. |Internal service execution timed out. |
