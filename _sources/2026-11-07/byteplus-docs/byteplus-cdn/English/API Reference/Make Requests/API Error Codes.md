---
title: "API Error Codes"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-api-error-codes"
---

This document describes common error codes in the BytePlus CDN.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you check the success of an API request, it is recommended that you use the method described in <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/reference-api-request-reponses#determine-whether-the-api-request-is-successful">Determine whether the API request is successful</a>.</div>


<span id="common-error-codes"></span>
## Common error codes

<span id="request-exception"></span>
### Request exception

The following error codes indicate that the API request contains illegal parameters or incorrect signatures. Please check your API request. See [Send API Requests](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-send-api-requests).


|**Code** |**Message** |**Description** |
|---|---|---|
|MissingParameter |The request is missing %s parameter. |One or more required parameters are missing in the request. For example Action, Version. |
|MissingAuthenticationToken |Request is missing Authentication Token. |Information used to authenticate the user is missing or incorrect in the request. |
|MissingRequestInfo |The request is missing %s information. |One or more required parameters are missing in the request. For example: AccessKey, ServiceName. |
|MissingSignature |The request is missing signature. |The request does not contain a signature. |
|InvalidTimestamp |The Signature of the request is expired. |Either the request has expired or the signature time is a time in the future. |
|ServiceNotFound |This service[%s] not found. |The requested service does not exist. |
|InvalidActionOrVersion |Could not find operation %s for version %s. |The requested API does not exist. |
|InvalidAccessKey |The accesskey [%s] included in the request is invalid. |The AccessKey included in the request is invalid. Please visit Key Management to view key information. |
|SignatureDoesNotMatch |The request signature we calculated does not match the signature you provided. Check your Secret Access Key and signing method. Consult the service documentation for details. |The request contained an incorrect signature. |
|MethodNotAllowed |HTTP Method Not Allowed. |The request method is invalid. |
|InvalidAuthorization |Invalid Authorization header, Pls check authorization header. |Authorization request header format error. |
|InvalidCredential |Invalid credential in Authorization, Pls check credential in authorization header. |The Credential parameter in the Authorization request header is malformed. |


<span id="system-error"></span>
### System error

The following error codes are caused by system exceptions. If you encounter such an error, please try again later or [submit a ticket](https://console.byteplus.com/workorder/create).


|**Code** |**Message** |**Description** |
|---|---|---|
|UndefinedError |Undefined Internal Error. Pls Contact With Admin. |The system is abnormal. |
|InternalError |Service has some internal Error. Pls Contact With Admin. |The system is abnormal. |
|FailToConnect |Top Fail to Connect to Internal Service. |The service connection could not be established. |
|InternalServiceTimeout |Internal Service is timeout. Pls Contact With Admin. |Internal Service is timeout. |
|InternalServiceTimeout |Internal Service is timeout. Pls Contact With Admin. |Internal Service is timeout. |
|ServiceUnavailableTemp |Service is busy, please try again later. |The service cannot be accessed. |
|InternalServiceError |Service has some internal Error. Pls Contact With Admin. |Service has failed. |


<span id="business-error-code"></span>
## Business error code

<span id="permission-exception"></span>
### Permission exception

The following error codes indicate that the sub\-user does not have permission to use the API to operate the target resource.


|**Code** |**Message** |**Description** |
|---|---|---|
|NotFound.Domain |There is no such domain name under the account: xxx,xxx |The resource you are trying to access does not belong to this account. |
|AccessDenied.IAMUnauthorized |Depending on the resource accessed, you will receive one of the following error messages:<br><br><br>* You do not have permission to operate the domain name:  *<domain\>* <br><br>* You do not have permission to perform this operation<br><br>* You don't have access to project:  *<project\>*  |The sub\-account does not have permission to access the specified domain, project, or use the API. |


<span id="parameter-exception"></span>
### Parameter exception

The following error codes indicate that the user request does not satisfy the configuration in the CDN.


|**Code** |**Message** |**Parameter description** |
|---|---|---|
|InvalidParameter.<param\> |parameter error |The API parameter is incorrect. Error categories are indicated in `param`. |
|InvalidParameter. Certificate |Certificate content parsing error. |An error occurred while parsing the contents of the certificate. |
|InvalidParameter.Certificate.KeyNotMatch |The certificate does not match the private key. |The public key of the certificate you uploaded does not match the private key. |
|InvalidParameter.Https.CertInfo.ChainMissing |The domain name configuration failed, the certificate chain is incomplete. |The domain name cannot be configured because the certificate chain in the certificate file is incomplete. |
|InternalError.<param\> |Internal error, please try again later or contact an engineer for further consultation. |The system is abnormal. The question category is indicated in `param`. Please [submit a ticket](https://console.byteplus.com/workorder/create). |
|InvalidParameter.BillingCode |Parameter error: BillingCode content is invalid. |Parameter error: `BillingCode` value is invalid. |
|InvalidParameter.BillingRegion |Incorrect parameter: BillingRegion. |Parameter error: `BillingRegion` value is invalid. |


<span id="obsolete-error-codes"></span>
## Obsolete error codes

The error codes in the following list are obsolete. These error codes no longer appear in CDN.


|**Code** |**Message** |
|---|---|
|CDN.ResourceNotFound |There is no such domain name under the account: xxx,xxx |
|CDN.PermissionDenied |You do not have permission to perform this operation. |
|CDN.PermissionDenied |You do not have permission to perform this operation. |
|CDN.InvalidParameters |Parameter error |
|CDN.InvalidParam.Certificate |Certificate parameter error |
|CDN.InvalidParam.PrivateKey |PrivateKey parameter error |
|CDN.InvalidParam.Source |Source parameter error |
|CDN.InvalidParam.CertificateChainError |The certificate chain cannot be completed |
|CDN.InternalError |Unknown error, please contact technical support |
|CDN.InvalidParam.CertificateExpired |The certificate has expired |
|CDN.InvalidParam.BillingCode |BillingCode parameter error |
|CDN.InvalidParam.BillingRegion |BillingRegion parameter error |
|CDN.InvalidParam.ExportType |ExportType parameter error |
