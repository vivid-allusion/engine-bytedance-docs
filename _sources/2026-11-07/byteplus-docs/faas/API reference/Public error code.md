---
title: "Public error code"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Public_error_code"
---

This article lists the error messages that are returned when calling Function Service OpenAPI fails.

For more BytePlus OpenAPI public error codes, refer to [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|**HTTP Status code** |**Error code** |**Error message** |**Processing measures** |
|---|---|---|---|
|400 Bad Request |MissingParameter |The request is missing {paramName} parameter. |Required request parameters are missing. Please confirm request parameters and try again. |
|400 Bad Request |InvalidParameter |The specified parameter {paramName} is not valid. |The request parameter value is invalid. Please check the correctness of the parameter values and try again. |
|400 Bad Request |QuotaExceeded |Number of function Triggers exceeded upper limit |The number of the Triggers of the function exceeded the upper limit. The Triggers need to be created under the name of other functions or submit a ticket to apply for higher quota. |
|400 Bad Request |MalformedParameter |The specified parameter {paramName} is malformed. |The request parameter value is invalid. Please check the correctness of the parameter values and try again. |
|400 Bad Request |InvalidRequest |\- |Request invalid. Please modify and try again. |
|400 Bad Request |TLSError |\- |TLS Trigger creation error. Please try again or submit a ticket. |
|401 Unauthorized |ServiceNotActivated |You need to create a service\-linked role for veFaaS by visiting the main page of veFaaS. |No veFaaS cross\-service role was created. You need to log in to Function Service console to authorize. |
|403 Forbidden |InvalidOperation |This operation is not supported. |Operation invalid. Retry after modification. |
|404 Not Found |ResourceNotFound |The specified resource {paramName} cannot be found. |The specified resource could not be found. Please confirm parameters and try again. |
|409 Conflict |DuplicatedResource |Resource {paramName} already exists. |Resources have been duplicated. Please try again. |
|409 Conflict |StatusConflictError |\- |Status conflict. Please directly retry or submit your ticket. |
|500 Internal Server Error |InternalServiceError |Internal error occurred: {message}. Please retry or open a ticket. |An internal error has occurred. Please try again or submit a ticket. |
|504 Gateway Timeout |TimeoutError |\- |Timeout. Please try again. |
