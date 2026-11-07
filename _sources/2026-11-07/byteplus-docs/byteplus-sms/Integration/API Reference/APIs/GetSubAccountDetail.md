---
title: "GetSubAccountDetail"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-getsubaccountdetail"
---

Use the GetSubAccountDetail API to query the name, ID, creation time, and message type of a message group. It's recommended you use SDK to call the GetSubAccountDetail API.

<span id="Request"></span>
## Request

**HTTP method**: GET

**URL**: `https://sms.byteplusapi.com?Action=GetSubAccountDetail&Version=2021-01-11`

**Header parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|AccessKey |string |Yes |AKLTNzEzY2\*\*\*\* |The access key ID of your BytePlus account. Click [here](https://console.byteplus.com/iam/keymanage) to obtain it. |
|SecretKey |string |Yes |RGTLuSHvnYxn\*\*\*\* |The secret access key ID of your BytePlus account. Click [here](https://console.byteplus.com/iam/keymanage) to obtain it. |
|ServiceName |string |Yes |volcSMS |The SMS service name. |
|Region |string |Yes |ap\-singapore\-1 |The service region name. |
|Content\-Type |string |Yes |application/json;charset=utf\-8 |The structured format of the request body. The Content\-Type of SMS service is `application/json; charset=utf-8`. |


**Query parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|Action |string |Yes |GetSubAccountDetail |The name of this API. |
|Version |string |Yes |2021\-01\-11 |The version of this API. |
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |


**Request example**

`https://sms.byteplusapi.com?Action=GetSubAccountDetail&Version=2021-01-11&subAccount=6e54bb00`

<span id="Response"></span>
## Response

**Response parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |ResponseMetadata |The parameter values in your request headers. |
|ResponseMetadata.RequestId |string |ID number of the request. |
|ResponseMetadata.Action |string |The HTTP method of the request. |
|ResponseMetadata.Version |string |The version of the request. |
|ResponseMetadata.Service |string |The service requested. |
|ResponseMetadata.Region |string |The region requested. |
|Result |Result |The result in response. The result returns only when no error occurs. |
|Result.subAccountName |string |Name of the message group. |
|Result.subAccountId |string |ID of the message group. |
|Result.createdTime |int64 |Time when the message group was created. |
|Result.enabledChannelType |Array |The enabled message type. |
|enabledChannelType.name |string |The name of the enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|enabledChannelType.value |string |The value of the enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|enabledChannelType.area |string |The supported region: overseas. It means countries or regions outside Mainland China. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```json
 "ResponseMetadata":{
        "RequestId":"a8e0788d-334e-49fc-92e8-61b7878c9735",
        "Action":"GetSubAccountDetail",
        "Version":"2021-01-11",
        "Service":"volcSMS",
        "Region":"ap-singapore-1"
    },
    "Result":{
        "subAccountName":"test_message_group",
        "subAccountId":"6e54bb00",
        "createdTime":1649799715,
        "status":1,
        "desc":"",
        "enabledChannelType":[
            {
                "name":" International one-time password message",
                "value":"I18N_OTP",
                "area":"overseas"
            },
            {
                "name":"International marketing message",
                "value":"I18N_MKT",
                "area":"overseas"
            }
        ]
    }
}
```


<span id="Error messages"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Description** |**Solution** |
|---|---|---|
|1999 |A system error occurs. |Contact technical support team for help. |
|1001 |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
