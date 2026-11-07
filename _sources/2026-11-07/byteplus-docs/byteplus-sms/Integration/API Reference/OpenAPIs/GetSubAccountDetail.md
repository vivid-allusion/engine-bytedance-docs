---
title: "GetSubAccountDetail"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-getsubaccountdetail_1"
---

Use the GetSubAccountDetail OpenAPI to query the name, ID, description, enabled channelType and creation time of a specific message group.

<span id="93a62198"></span>
## Request

**HTTP method**: GET

**URL**: https://sms.byteplusapi.com/sms/openapi/sub_account/detail

**Header parameters**


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Authorization |Basic base64 (username:password). For example: Basic NzQ2VIBlxxxxxXXXXXXXXXXXXXXGF6dDlZSG4xSml6Vjc3NzY= |Find the username and password information on the **Service Settings of Admin Settings** page in the SMS console |Yes |


**Query parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |


**Request example**

https://sms.byteplusapi.com/sms/openapi/sub_account/detail?subAccount=77b3f267

<span id="87561b82"></span>
## Response

**Response parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |ResponseMetadata |The parameter values in your request headers. |
|ResponseMetadata.RequestId |string |ID number of the request. |
|ResponseMetadata.Action |string |Empty string |
|ResponseMetadata.Version |string |Empty string |
|ResponseMetadata.Service |string |Empty string |
|ResponseMetadata.Region |string |The region requested. |
|Result |Result |The result in response. The result returns only when no error occurs. |
|Result.subAccountName |string |Name of the message group. |
|Result.subAccountId |string |ID of the message group. |
|Result.createdTime |int64 |Time when the message group was created. |
|Result.status |int64 |Status of the message group |
|Result.desc |string |Description of the message group |
|Result.enabledChannelType |Array |The enabled message type. |
|enabledChannelType.name |string |The name of the enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|enabledChannelType.value |string |The value of the enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|enabledChannelType.area |string |The supported region: overseas. It means countries or regions outside Mainland China. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240112060305DF5AAB0BAF6E0C08E296",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": "BOE"
    },
    "Result": {
        "subAccountName": "test_message_group",
        "subAccountId": "7axxxx99",
        "createdTime": 1692011918,
        "status": 1,
        "desc": "123",
        "enabledChannelType": [
            {
                "name": "International one-time password message",
                "value": "I18N_OTP",
                "area": "overseas"
            },
            {
                "name": "International marketing message",
                "value": "I18N_MKT",
                "area": "overseas"
            }
        ]
    }
}
```


<span id="328f0ea8"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Description** |**Solution** |
|---|---|---|
|1999 |A system error occurs. |Contact the technical support team for help. |
|1001 |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
