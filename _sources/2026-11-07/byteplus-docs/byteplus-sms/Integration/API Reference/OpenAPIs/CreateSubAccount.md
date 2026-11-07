---
title: "CreateSubAccount"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-createsubaccount"
---

Use the CreateSubAccount OpenAPI to create a message group under your account

<span id="c502abee"></span>
## Request

**HTTP method**: POST

**URL**: https://sms.byteplusapi.com/sms/openapi/sub_account

**Header parameters**


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Authorization |Basic base64 (username:password). For example: Basic NzQ2VIBlxxxxxXXXXXXXXXXXXXXGF6dDlZSG4xSml6Vjc3NzY= |Find the username and password information on the **Service Settings of Admin Settings** page in the SMS console |Yes |


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Example of value** |**Description** |
|---|---|---|---|---|
|subAccountName |string |Yes |testNamexxxx |The message group Name. |
|desc |string |false |Use for MKT |The description of the message group |


**Example of request payload**

```JSON
{
    "subAccountName":"testSubaccountName",
    "desc":"TestDesc"
}
```


<span id="0d595f5f"></span>
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
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240112064131AD5D1DAB1B009A0B3D39",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": "BOE"
    },
    "Result": ""
}
```


<span id="a7283f87"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Description** |**Solution** |
|---|---|---|
|1999 |A system error occurs. |Contact the technical support team for help. |
|1001 |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
