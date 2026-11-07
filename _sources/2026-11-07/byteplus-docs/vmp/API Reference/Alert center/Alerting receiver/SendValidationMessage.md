---
title: "SendValidationMessage"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/SendValidationMessage"
---

Send an email verification message.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=SendValidationMessage&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |SendValidationMessage |API name. The API name is SendValidationMessage. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|Type |String |Yes |Email |Type of verification. `Email` is the only value for it. |
|Destination |String |Yes |user\-demo@example.com |Contact person email. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=SendValidationMessage&Version=2021-03-03
Content-Type: application/json
{
    "Type": "Email",
    "Destination": "user-demo@example.com"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|SendStatus |String |MessageSucceed.Email |The status returned when sending verification emails:<br><br><br>* **AlreadyActive.Email**: the email address has already been verified<br><br>* **MessageFailed.Email**: failed to send the verification email<br><br>* **LimitExceeded.Email**: email sending is too frequent<br><br>* **MessageSucceed.Email**: verification email has been sent successfully |
|Message |String |\- |The reason for the error that occurred when sending the verification email. This parameter has a value if `SendStatus` is not `MessageSucceed.Email`. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SendValidationMessage",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "SendStatus": "MessageSucceed.Email",
        "Message": ""
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error messages |Description |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|404 |NotFound.Id |The specified Contact/ContactGroup {{Id}} is not found. |The specified contact person/group was not found. |
|429 |LimitExceeded.Email |The same email address should not be validated more than once in 1 minute, please try it later. |Verification of an email address can only be performed once a minute. Please try again later. |
