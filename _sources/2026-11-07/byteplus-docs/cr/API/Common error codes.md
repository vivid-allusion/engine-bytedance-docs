---
title: "Common error codes"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/common-error-codes"
---

This topic describes the messages returned for errors that occur when you call Container Registry (CR) API actions.

For more information on BytePlus API common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|**HTTP Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|400 |InvalidParameter. |The specified %s is invalid. |The parameter is invalid due to its invalid characters or excessive length. Modify the parameter and confirm that it is valid, then try again. |
|400 |MissingParameter. |The required parameter %s is missing. |The required parameter, such as the Action or Version, is missing. Modify the parameter and confirm that it is valid, then try again. |
|400 |IdempotentParameterMismatch |Parameters mismatch the previous request with a same ClientToken. |The request contains the ClientToken. The ClientToken is used in two requests with different parameters. Change the ClientToken and try again. |
|403 |AccessDenied |You are not authorized to perform this action. |The request does not pass the IAM permission verification. Check the IAM policy configured by the user and try again. |
|404 |NotFound. |The specified resource %s is not found. |The specified resource does not exist. Use another desired resource name and try again. |
|409 |AlreadyExists. |The specified resource %s already exist. |The resource already exists. Use another desired resource name and try again. |
|500 |InternalError |The request failed due to an unknown error. |An unknown error occurred when the request was processed. Possible errors are back\-end service timeouts and network fluctuation. Try again. If the error persists, [submit a ticket](https://byteplus.zendesk.com/hc/en-sg/requests/new). |
