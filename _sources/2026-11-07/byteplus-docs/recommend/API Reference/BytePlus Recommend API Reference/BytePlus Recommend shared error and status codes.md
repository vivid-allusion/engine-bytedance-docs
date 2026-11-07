---
title: "BytePlus Recommend shared error and status codes"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-shared_error_and_status_codes"
---

This topic documents shared error and status codes. Refer to the specific API documentation for error codes related to API business logic.

<span id="61e8b797"></span>
# Error code descriptions

The following are the error codes related to the current interface.


|**Error Code** |**Description** |
|---|---|
|4XX |Codes in the 400 range detail all the errors a developer could encounter while using the API. 4XX indicates a user error. |
|5XX |Codes in the 500 range are error responses from the system. If an error occurs during the execution of a resource not due to user input, a 500 response will be returned with a corresponding JSON error body. That body contains a message detailing what went wrong. |
|1XXX |The error is related to Import calls. |
|2XXX |The error is related to Predict calls. |


<span id="8fd12370"></span>
# Write API error codes

This topic details the specific error codes relevant to the Write APIs.


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|400 |BadRequest |Data is empty. |The request parameters input by the user are not correct. |
|401 |Unauthorized |Auth fail, xxx |The authentication signature verification failed. |
|409 |Conflict |Duplicate submission with request\-id: xxx. |Multiple API requests with the same request_id have been sent within a short period of time. |
|413 |RequestEntityTooLarge |The count of write items max to 2000. |Reduce the amount of data sent in a single request. The Write APIs support at most 2,000 data records in one request. |
|429 |TooManyRequests |Your request is blocked because there is an excessive amount of data waiting to be processed. Try again and consider reducing the data count in your request. |Too many concurrent requests were made. |
|500 |InternalServerError |Internal error encountered. |Internal server error occurred. |
|1001 |PartDataOccurError |An error occurred, and there was a failure in handling either partial or all of the data. |Handling of either partial or all of the data has encountered failures. |
|1003 |InternalErrorNeedRetry |A temporary internal error has occurred. Please attempt your action again. |A temporary internal error occurred. Try the request at a later time. |


<span id="a009b3ca"></span>
# AckServerImpression and Predict API error codes

This topic details the specific error codes relevant to the AckServerImpressions and Predict APIs.


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|400 |BadRequest |The failure to unmarshal the request body suggests an issue with the correctness of the specified path. Ensure that the path is accurate. |The request was incomplete or had incorrect parameter values. |
|500 |InternalServerError |Internal error encountered. |Internal server error. |
