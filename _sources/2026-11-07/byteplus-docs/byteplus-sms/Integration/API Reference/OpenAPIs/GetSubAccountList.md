---
title: "GetSubAccountList"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-getsubaccountlist_1"
---

Use the GetSubAccountList OpenAPI to query the name, ID, description, enabled channelType and creation time of all the message groups under your account.

<span id="0a4c974b"></span>
## Request

**HTTP method**: GET

**URL**: https://sms.byteplusapi.com/sms/openapi/sub_account/list

**Header parameters**


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Authorization |Basic base64 (username:password). For example: Basic NzQ2VIBlxxxxxXXXXXXXXXXXXXXGF6dDlZSG4xSml6Vjc3NzY= |Find the username and password information on the **Service Settings of Admin Settings** page in the SMS console |Yes |


**Request example**

https://sms.byteplusapi.com/sms/openapi/sub_account/list

<span id="a1d2468c"></span>
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
|Result.list |Array |The list of the name, ID, and creation time of a message group. |
|Result.list.subAccountName |string |Name of the message group. |
|Result.list.subAccountId |string |ID of the message group. |
|Result.list.createdTime |int64 |Time when the message group was created. |
|Result.list.status |int64 |Status of the message group |
|Result.list.desc |string |Description of the message group |
|Result.list.enabledChannelType |Array |The enabled message type. |
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
        "RequestId": "021705026590259fdbddc6100ff00040ad96a22000019865b104b",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": ""
    },
    "Result": {
        "list": [
            {
                "subAccountName": "test_message_group",
                "subAccountId": "7axxxx76",
                "createdTime": 1704703660,
                "status": 1,
                "desc": "descxxx",
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
        ],
        "total": 1
    }
}
```


<span id="1e24aec8"></span>
## **Error messages**

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Description** |**Solution** |
|---|---|---|
|1999 |A system error occurs. |Contact the technical support team for help. |
|1001 |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
