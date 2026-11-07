---
title: "CreateContacts"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/CreateContacts"
---

Create contacts.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A single account can create at most 100 contacts.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=CreateContacts&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateContacts&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateContacts |The name of the API. The current API name is `CreateContacts`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |Yes |user\-demo |The name of the contact.<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can contain only Chinese characters, letters, digits, underscores (`_`), and hyphens (`-`).<br><br>* The name must be 1 to 128 characters in length. |
|Email |String |Yes |user\-demo@example.com |The alert email address.<br><br>Cloud Monitor will send a verification email to the provided email address. You need to click the verification link in the email to complete verification. Once verified, this email address will be activated to receive alert notifications. |
|Phone |String |No |186117\*\*\*\* |The alert phone number.<br><br>Cloud Monitor will send a verification SMS to the provided phone number. You need to tap the verification link in the SMS to complete verification. Once verified, this phone number will be activated to receive alert notifications. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=CreateContacts&Version=2018-01-01
Content-Type: application/json
{
    "Name": "user-demo",
    "Email": "user-demo@example.com",
    "Phone": "186117****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |["157255269369\*\*\*\*\*\*"] |Alert contact ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateContacts",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "157255269369******"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
