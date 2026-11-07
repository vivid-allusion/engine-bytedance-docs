---
title: "Status Codes"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/132486"
---


|Error Code |Error Message |Description |
|---|---|---|
|200 |None |The API request was successful. |
|201 |None |The API request was successful and the resource has been created. |
|400 |Unknown Request<br><br>Invalid RID |Unknown request exception.<br><br>The RID set during subscription does not exist. |
|401 |Token Missing<br><br>Token Illegal<br><br>Token Signature Check Failed<br><br>Token Check Failed |Token is missing.<br><br>The token is invalid.<br><br>The token signature check failed.<br><br>The token check failed. |
|403 |Token Expired |Token has expired. |
|404 |Not Found<br><br>Resource Does Not Exist |The requested service path is incorrect.<br><br>Resource does not exist. Returned when calling the API to destroy publishing/subscription resources. |
|409 |Stream Does Not Exist |Stream does not exist. Returned when calling the API to create subscription resources.<br><br>A `409` error can occur if you subscribe immediately after publishing due to a global data synchronization delay. If this happens, retry the request. |
|415 |Invalid Content\-Type |The request's content type is invalid. |
|500 |Internal Error |Internal service error. |
|503 |Service Temporarily Unavailable |Service temporarily unavailable. |
|504 |Gateway Timeout |Gateway timeout. |
