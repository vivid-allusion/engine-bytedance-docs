---
title: "OpenAPI for messaging"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-openapi-overview"
---

Use this OpenAPI to send a text message to a maximum of 200 phone numbers at one time. Text content can be verification, notifications, or marketing messages.

<span id="Prerequisite"></span>
## Prerequisites

Create and find the passwords on the Message Group page in the SMS console for later authorization:


1. Go to the BytePlus SMS console. On the left navigation pane, click **Message Group**.

   The **Message Group** page appears.

2. Find the message group that you want to send messages to. Under the **Operation** column, click **Password**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4bffc0214a14da7a6b6a58ccdc041ed~tplv-goo7wpa0wc-image.image" width="2938px" />   </div>
   

   The **OpenAPI Password** page appears.

3. Click **Create Password**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7ddfe157ba6404ab0558fd992db0f41~tplv-goo7wpa0wc-image.image) </span>

4. The **Create Password** window pops up and you can create OTP and MKT passwords here.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b676a330ff4469e982c76f1c89584ba~tplv-goo7wpa0wc-image.image) </span>

5. Once created, you can find your password here.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27d113e88e694009911d7dcde7730e72~tplv-goo7wpa0wc-image.image) </span>


<span id="d3df6507"></span>
## Request

**HTTP method**: POST

**URL**: https://sms.byteplusapi.com/sms/openapi/send_sms

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To learn more about data centers, contact customer support.</div>


**Header parameters**


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Content\-Type |application/json;charset=utf\-8 |None |Yes |
|Authorization |Basic base64 (username:password). For example: `Basic NzQ2VIBlxxxxxXXXXXXXXXXXXXXGF6dDlZSG4xSml6Vjc3NzY=` |Find the username and password information on the **Message Group Configuration** page in the SMS console. The username is the Message Group ID by default. |Yes |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">One pair of username and password can only be used for one message type, OTP or MKT.</div>


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Value Sample** |**Description** |
|---|---|---|---|---|
|PhoneNumbers |string |Yes |+6598620548,+85296143924 |Multiple phone numbers, which are separated by commas in English. You can enter a maximum of 200 phone numbers at one time. |
|Content |string |Yes |Your verify code is 123456. |Content of short messages. |
|From |string |Yes |YourBrandName |The brand identifier that appears as the sender name on recipients' devices. Please use your registered and approved brand name. |
|Tag |string |No |123456 |Pass\-through messages This parameter is for you to build the mapping between your request and delivery receipt. For example, if you define the Tag parameter as a unique ID number, the ID number will be displayed in the ext field of delivery receipt. |
|CallbackURL |String |No |https://webhook.site/#!/c915da22\-5822\-4ba0 |URL to receive delivery receipt for the message sent. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">For the parameter <code>PhoneNumbers</code>, international area codes are required. The format must meet E.164 standards.</div>


2. <div data-tips="true" data-tips-type="tip">For the parameter <code>From</code></div>


   1. <div data-tips="true" data-tips-type="tip">The From field must use your pre\-registered and approved brand name. Please contact BytePlus team for sender ID registration support.</div>


   2. <div data-tips="true" data-tips-type="tip">Using unregistered Sender IDs will result in sending failure.</div>


   3. <div data-tips="true" data-tips-type="tip">Do not use "BytePlus" as your Sender ID.</div>



**Example of request payload**

```JSON
{
    "PhoneNumbers": "+6586840575,+6586840576",
    "Content":"your verify code is 38208",
    "From": "BytePlus",
    "Tag":"123456",
    "CallbackURL":"https://webhook.site/#!/c915da22-5822-4ba0"
}
```


<span id="Response"></span>
## Response

**Response parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |ResponseMetadata |The parameter values in your request headers |
|ResponseMetadata.RequestId |string |ID number of the request |
|ResponseMetadata.Action |string |The HTTP method of the request |
|ResponseMetadata.Version |string |The version of the request |
|ResponseMetadata.Service |string |The service requested |
|ResponseMetadata.Region |string |The region requested |
|Result |Result |The result in response. The result returns only when no error occurs. |
|Result.MessageID |[]string |The ID number of the responded messages. Each ID number represents a request from a mobile phone number and the numbers are sorted by numbers. |
|ResponseMetadata.Error |Error |The error messages. For details, refer to the Error messages section. |
|ResponseMetadata.Error.Code |string |The codes of error messages. |
|ResponseMetadata.Error.Message |string |The description of the error messages. |


**Example of response payload**

```json
{
    "ResponseMetadata": {
        "RequestId": "a8e0788d-334e-49fc-92e8-61b7878c9735",
        "Action": "",
        "Version": "",
        "Service": "",
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
