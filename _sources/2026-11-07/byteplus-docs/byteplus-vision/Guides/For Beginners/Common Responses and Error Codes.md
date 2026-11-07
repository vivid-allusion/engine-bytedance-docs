---
title: "Common Responses and Error Codes"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-responses-and-error-codes"
---

<span id="Overview"></span>
## Overview

The service has a uniform return structure and common error codes.

<span id="Commmon Response Structure"></span>
## Commmon Response Structure

The service will return a JSON structure with the following field descriptions.


|**Field** |**Category** |**Optional** |**Description** |
|---|---|---|---|
|ResponseMetadata |json |True |Gateway layer return value, if this field is returned and the value is not None, no need to pay attention to other fields |
|request_id |String |True，If `ResponseMetadata` is not returned or `None`, `request_id` must be returned. |Service layer return value, representing the unique ID of this request |
|time_elapsed |Int |True，If `ResponseMetadata` is not returned or `None`, `time_elapsed` must be returned. |Service layer return value, the time spent on the entire request in milliseconds |
|code |Int |True，If `ResponseMetadata` is not returned or `None`, `code` must be returned. |Service layer return value, indicating the result status code of this validation. See the `service generic error code` below and the `error code` section of each service interface document for details |
|message |String |True，If `ResponseMetadata` is not returned or `None`, `message` must be returned. |Service layer return value, this string is returned when the request fails, otherwise this field does not exist |
|data |json |True，If `ResponseMetadata` is not returned or `None`, `data` must be returned. |Service layer return value, json structure, which contains the business data of each interface, see the detailed description of each service interface documentation |


<span id="ResponseMetadata Description"></span>
### ResponseMetadata Description


|**Field** |**Category** |**Optional** |**Description** |
|---|---|---|---|
|RequestId |string |False |Unique ID for gateway layer requests |
|Action |string |True |Service name |
|Version |string |True |Version number |
|Service |string |True |Service name |
|Region |string |True |Region |
|Error |ErrorInfo |True |Error message |


<span id="ErrorInfo Description"></span>
### ErrorInfo Description


|**Field** |**Category** |**Optional** |**Description** |
|---|---|---|---|
|Code |string |False |Gateway layer error, please refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes) |
|Message |string |False |Gateway layer error, please refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes) |


<span id="Service Common Errors"></span>
## Service Common Errors


|**http_code** |**code** |**Status type** |**Description** |
|---|---|---|---|
|200 |10000 |ECSuccess |Request succeed |
|400 |50200 |ECReqInvalidArgs |Parameter error |
|400 |50201 |ECReqMissingArgs |Parameter missing |
|400 |50204 |ECParseArgs |Parameter error/Parameter missing |
|400 |50205 |ECImageSizeLimited |Image exceeds size limits |
|400 |50206 |ECImageEmpty |No image in the request data |
|400 |50207 |ECImageDecodeError |Image decoding error: No image was fetched or the image passed through the image_base64 parameter was base64 decoded incorrectly |
|401 |50400 |ECAuth |Permission verification failed |
|404 |50402 |ECReqMethod |Service not exist |
|429 |50429 |ECReqLimit |QPS exceeds limit |
|500 |50500 |ECInternal |Server internal error |
|500 |50501 |ECRPCInternal |Server internal RPC error |
