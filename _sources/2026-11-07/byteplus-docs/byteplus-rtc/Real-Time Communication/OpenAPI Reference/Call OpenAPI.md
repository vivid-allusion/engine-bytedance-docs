---
title: "Call OpenAPI"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828"
---

In this section, you learn how to call RTC server\-side OpenAPIs. For specific OpenAPIs, it's necessary to follow their parameter settings, such as input and response parameters.

<span id="preconditions"></span>
## Preconditions


1. Sign up for AK/SK. You can manage your AK/SK via [console-keymanage](https://console.byteplus.com/iam/keymanage).

2. Open the RTC service via the console.

> We highly recommend that you create a user account (sub\-account) with authorization of the master account, and make OpenAPI calls with the user account. To create a user account, select console \> IAM \> user.


<span id="service-address"></span>
### Service Address

`open.byteplusapi.com`

<span id="communications-protocol"></span>
### Communications protocol

You can implement request communication using HTTP and HTTPS. However, we highly recommend that you use HTTPS which is more secure than HTTP.

<span id="request-method"></span>
### Request Method

Get or request based on specific requirements of OpenAPIs.

<span id="request-parameters"></span>
### Request Parameters

Common and specific parameters are needed when you issue a request.

<span id="common-parameters"></span>
#### Common Parameters

see [Common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)

<span id="specific-parameters"></span>
#### Specific Parameters

For specific parameters, see their corresponding OpenAPI documents.

For ID\-related parameters, such as BusinessId, TaskId, RoomId and UserId, you must obey following naming conventions:


* The length of a string is no longer than 128 characters.

* A string can contain following characters:

   * `a~z`

   * `A~Z`

   * `0~9`

   * `@` `.` `_` `-`


<span id="character-encoding"></span>
### Character encoding

Results of the request and return are encoded in UTF\-8.

<span id="signature-mechanism"></span>
### Signature mechanism

See [Signature request](https://docs.byteplus.com/en/byteplus-platform/reference/request-signature).

<span id="response"></span>
## Response

The response's structure of different versions of OpenAPI varies:

<span id="_2023-11-01-2023-07-20"></span>
### 2023\-11\-01 & 2023\-07\-20

When the HTTP response status code is equal to `200`, it indicates a successful call.

When the HTTP response status code is not equal to `200`, it indicates a failed call. You can parse the error reason based on the `Code` and `Message` fields in `BaseResponse.ResponseMetaData` and `BaseResponse.Result` field.

See the example below:


* The call succeeds:


```json
    {
        "ResponseMetadata": {
            "RequestId": "Your_RequestId",
             "Action": "DismissRoom",
            "Version": "2020-12-01",
            "Service": "rtc",
            "Region": "ap-singapore-1"
        },
        "Result":{
            "Message": "success"
        }
    }
```



* The call fails:


```json
    {
         "ResponseMetadata": {
            "RequestId": "Your_RequestId",
            "Action": "DismissRoom",
            "Version": "2020-12-01",
            "Service": "rtc",
            "Region": "ap-singapore-1"
            "Error":{
                "Code": "InvalidParameter.AccountIdMismatch",
                "Message": "Check owner failed"
        }
    }，
        "Result": {}        
    }
```


<span id="_2022-06-01-2020-12-01"></span>
### 2022\-06\-01 & 2020\-12\-01

<span id="acquiring-data-index"></span>
#### Acquiring data index:

When the HTTP response status code is equal to `200`, it indicates a successful call.

When the HTTP response status code is not equal to `200`, it indicates a failed call. You can parse the error reason based on the `Code` and `Message` fields in `BaseResponse.ResponseMetaData` and `BaseResponse.Result` field.

See the example below:


* The call succeeds:


```json
    {
        "ResponseMetadata": {
            "RequestId": "Your_RequestId",
             "Action": "DismissRoom",
            "Version": "2020-12-01",
            "Service": "rtc",
            "Region": "ap-singapore-1"
        },
        "Result":{
            "Message": "success"
        }
    }
```



* The call fails:


```json
    {
         "ResponseMetadata": {
            "RequestId": "Your_RequestId",
            "Action": "DismissRoom",
            "Version": "2020-12-01",
            "Service": "rtc",
            "Region": "ap-singapore-1"
            "Error":{
                "Code": "InvalidParameter.AccountIdMismatch",
                "Message": "Check owner failed"
        }
    }，
        "Result": {}        
    }
```


<span id="apart-from-acquiring-data-index"></span>
#### Apart from acquiring data index:

The response to all HTTP requests is status code `200`. You need to identify whether the call succeeds or not by analysing `ResponseMetaData` in response.

See the example below:


* The call succeeds:

   ```Plain
   {
       "ResponseMetadata": {
           "RequestId": "Your_RequestId",
           "Action": "DismissRoom",
           "Version": "2020-12-01",
           "Service": "rtc",
           "Region": "ap-singapore-1"
       },
       "Result":{
           "Message": "success"
       }
   }
   ```
   

* The call fails:

   ```Plain
   {
       "ResponseMetadata": {
           "RequestId": "Your_RequestId",
           "Action": "DismissRoom",
           "Version": "2020-12-01",
           "Service": "rtc",
           "Region": "ap-singapore-1"
       },
       "Error":{
           "Code": "InvalidParameter.AccountIdMismatch",
           "Message": "Check owner failed"
       }
   }
   ```
   


<span id="error-code"></span>
### Error code

When the call fails, `ResponseMetaData.Error` in the response will contain the error code and error message. To learn detailed descriptions of error codes and how to fix them, see [Error Code](https://docs.byteplus.com/en/docs/12/docs-70426)
