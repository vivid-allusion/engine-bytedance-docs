---
title: "SendBatchSms"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-sendbatchsms"
---

Use the SendBatchSms API to send messages with different contents to a maximum of 200 phone numbers in one request. It's recommended you use SDK to call the SendBatchSms API.

<span id="Request"></span>
## Request

**HTTP method**: POST

**URL**: `https://sms.byteplusapi.com?Action=SendBatchSms&Version=2021-01-01`

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can add up to 200 phone numbers in one call.</div>


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
|Action |string |Yes |SendBatchSms |The name of this API. |
|Version |string |Yes |2021\-01\-01 |The version of this API. |


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Example of value** |**Description** |
|---|---|---|---|---|
|SmsAccount |string |Yes |049c\*\*\*\* |The message group ID. |
|From |string |Yes |YourBrandName |The brand identifier that appears as the sender name on recipients' devices. Please use your registered and approved brand name.<br><br><br>1. The From field must use your pre\-registered and approved brand name. Please contact BytePlus team for sender ID registration support.<br><br>2. Using unregistered Sender IDs will result in sending failure.<br><br>3. Do not use "BytePlus" as your Sender ID. |
|TemplateID |string |Yes |ST_6050\*\*\*\* |The ID number of text message template. |
|Messages |Json array |Yes |See the example below |The message body. Refer to the following table for details. |
|Tag |string |No |123456 |The pass\-through messages. The maximum length is 512 characters. This parameter is for you to build the mapping between your request and delivery receipt. For example, after you define the Tag parameter as an unique ID number, the ID number will be displayed in the field of the ext field of delivery receipt. |
|ReferenceID |string |No |referenceid1 |Used for an idempotent check. Within 6 hours, for the same RefercenID and SmsAccount, only one message is sent to a PhoneNumber. |


**Messages**


|**Parameter** |**Type** |**Required** |**Example of value** |**Description** |
|---|---|---|---|---|
|PhoneNumber |string |Yes |18800001\*\*\*\* |Recipient's mobile number. Up to 200 phone numbers. Separate them by commas.<br><br>**Note**: International area codes are required. The format must meet E.164 standards. |
|TemplateParam |string |No | |Values of placeholders in the short text message template. |


**Example of request payload**

```json
{
    "SmsAccount":"0f6bfe96",
    "From":"BytePlus",
    "TemplateID":"ST_0f6c5036",
    "Messages":[
        {
            "PhoneNumber":"18800001234",
            "TemplateParam":"{\"code\":\"1234\"}"
        },
        {
            "PhoneNumber":"18800001235",
            "TemplateParam":"{\"code\":\"1234\"}"
        }
    ],
    "Tag":"send return",
    "ReferenceID":"referenceid1"
}
```


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
|Result |Result |The result in response.The result returns only when no error occurs. |
|Result.MessageID |Array |The ID number of the responded messages.<br><br><br>* If the phone numbers are parsed successfully, multiple message IDs are returned. Each message ID represents a request for a phone number, and the display order follows the order of incoming phone numbers.<br><br>* If the phone numbers fail to be parsed, only one message ID is returned. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```json
{
    "ResponseMetadata": {
        "RequestId": "a8e0788d-334e-49fc-92e8-61b7878c9735",
        "Action": "SendSms",
        "Version": "2021-01-01",
        "Service": "volcSMS",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MessageID": [
            "c0603139-2613-4f17-a9e3-e6faa3846eda",
            "38734be4-f31c-4f04-88a2-0f1c3b0bd0d6"
        ]
    }
}
```


<span id="Error messages"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Message** |**Description** |
|---|---|---|
|RE:0000 |Authentication failed |Please check if the parameters are used correctly or refer to the authentication processing in the SDK. |
|RE:0001 |SMS service not activated |Please check if the current AccessKey has already activated SMS service. If the SMS service has been activated, please refer to the SMS service documentation to call the interface. |
|RE:0002 |Account shutdown |Please contact BytePlus customer service for confirmation. |
|RE:0003 |Subaccount not existing |Please fill in the correct SMS Account, which is the message group ID. |
|RE:0004 |Signature error |Please confirm if the signature exists under the corresponding SMS account, or log in to the SMS service console to check if the signature has been approved on the SMS signature page. |
|RE:0005 |Template error |Please check if the template exists under the corresponding SMS account, or log in to the SMS service console to check if the template has been approved on the SMS template page. |
|RE:0006 |Phone number format error |Please pass in the correct format for the parameter PhoneNumbers. |
|RE:0007 |IP verification error |The IP whitelist has been activated. Please contact BytePlus customer service to confirm if the current IP has been whitelisted. |
|RE:0008 |OpenAPI authentication error |Please check if the parameters are used correctly or refer to the authentication processing in the SDK. |
|RE:0009 |Request parameters error |Please check if the parameters are correct according to the interface documentation. |
|RE:0010 |Account charge overdue |Please log in to the expense center of the console to check if the balance is sufficient. |
|RE:0011 |Unsupport area |Please distribute or apply for SMS distribution within the allowed regions. |
|RE:0012 |Unsupport send type |Please log in to the console, click Edit in the message group list, and check if the allowed message types are checked. |
|RE:0013 |Sending volume exceeds threshold |Please check the upper limit setting for sending messages on the console. |
|RE:0014 |Decryption failed |Decryption failed, please check the encryption configuration on the console. |
|RE:0500 |Unknown interaction error |Please try calling the interface again. |
