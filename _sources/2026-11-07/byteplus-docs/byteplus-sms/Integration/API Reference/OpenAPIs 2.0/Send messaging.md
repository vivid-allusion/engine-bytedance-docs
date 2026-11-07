---
title: "Send messaging"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/Send_whatsapp_message"
---

You can invoke the Send message interface to send short messages, whatsapp messages, and Voice messages of the same content to one or multiple mobile phone numbers.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please select the appropriate channel at the time of the request</div>


<span id="56e83a1a"></span>
## Request

**HTTP method：** POST

**Base URL：**  sms.byteplusapi.com/v1/message

**Header parameters：** 


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Content\-Type |application/json;charset=utf\-8 |Fixed value. |Yes |
|Authorization |Basic base64 (username:password). |The username and password information, please connect byteplus team to obtain it.<br><br>PS：Recommend creating 2.0 version of the password |Yes |


**Request body parameters**


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|SmsAccount ||string |049c\*\*\*\* |The message group ID. |yes |
|Tag ||string |123456 |Pass\-through messages This parameter is for you to build the mapping between your request and delivery receipt. For example, if you define the Tag parameter as a unique ID number, the ID number will be displayed in the ext field of delivery receipt. |no |
|To ||array object | | |yes |
| |number |string |+6598XXXX0548 |Also support multiple mobile phone numbers, which are separated by commas in English.<br><br>**Note**: International area codes are required and the format must meet E.164 standards. |yes |
|CallbackUrl | |string |https://webhook.site/#!/c915da22\-5822\-xxxxx |URL to receive delivery receipt for Whatsapp sent. |no |
|ChannelsFlow | |array |Whatsapp |Channel type.<br><br><br>1. Whatsapp<br><br>2. SMS |yes |
|Whatsapp | |object | | |This parameter is mandatory when ChannelsFlow=Whatsapp |
| |From |string |BytePlus |Sender ID, Used to choose the display name of whatsapp business account |no |
| |FromNumber |string | |Whatsapp Business Number for sending message |yes |
| |TemplateLanguage |string |en_US |Language for template message |Yes when sending template message |
| |MessageType |string |Template |Message Type.<br><br><br>1. Template, for template message<br><br>2. Image<br><br>3. Interactive<br><br>4. Video<br><br>5. Audio<br><br>6. Document<br><br>7. Location<br><br>8. Text |yes |
| |TemplateID |string |ST_6050\*\*\*\* |The ID number of template. |yes |
| |ParamType |string |Component |1. Component, for template message<br><br>2. Custom, for other message |yes |
| |ApiType |int |0 |0:cloud api ,1: MMLite api<br><br>It defaults to 0 when no value is passed.<br><br>**Note: MMLite can only be used when sending MKT template messages.**  |No |
| |\*Component |array object[Component] | |Template Components |yes when sending template message |
| |Text |Text object | |Text Message Content |Yes when 'MessageType' is 'text' |
| |Image |Image object | |Image Message Content |Yes when 'MessageType' is 'image' |
| |Video |Video object | |Video Message Content |Yes when 'MessageType' is 'video' |
| |Audio |Audio object | |Audio Message Content |Yes when 'MessageType' is 'audio' |
| |Document |Document object | |Document Message Content |Yes when 'MessageType' is 'document' |
| |Location |Location object | |Location Message Content |Yes when 'MessageType' is 'location' |
| |Interactive |Interactive object | |Interactive Message Content |Yes when 'MessageType' is 'interactive' |
|SMS | |object | | |This parameter is mandatory when ChannelsFlow=SMS |
| |Content |string | |Your verify code is 123456. |Yes |
| |From |string | |YourBrandName |Yes |
| |MessageType |int | |1:OTP.3:MKT |Yes |
| |Extra |Extra | |Placeholder for future parameters | |
| |Extra.DltEntityId |string | |DLT Entity (PE) ID |No |
| |Extra.DltTemplateId |string | |DLT Template ID |No |


\*Component Object:


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|type ||string |header/body/button |Component type, which can be header, body, button<br><br><br>1. When type=header, set the variable information of the template header.<br><br>2. When type=body, set variable information of template content;<br><br>3. When type=button, set the variable information of the template button |yes |
|sub_type ||string |123456 |When type=button, this parameter is required<br><br>It can be a url, quick_reply, copy_code, phone_number. |yes\*\*[only if type=button]\*\*<br><br>no\*\*[type=header/body]\*\* |
|index ||string |0 |The position index of the button.<br><br>When type=button, this parameter is required<br><br>The serial number of the button is 0\-2. |yes\*\*[only if type=button]\*\*<br><br>no\*\*[type=header/body]\*\* |
|\*parameters ||Array object[Parameter] | |Component parameter list |no |


\*Parameters Object:


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|type ||string |text/image/video/document/location/coupon_code/payload/interactive |1. component = header, the value could be text, image, video, document, location<br><br>2. component = body, the value is text<br><br>3. component = button and sub_type=url/otp, the value is text<br><br>4. component = button and sub_type= quick_reply, the value is payload<br><br>5. component = button and sub_type= copy_code, the value is coupon_code |yes |
|text ||string |xxx |When type= payload, this parameter is required<br><br>which could set the payload content of the parameter. |yes\*\*[only if type=payload]\*\*<br><br>no\*\*[type=others]\*\* |
|\*image ||Json object | |When type= image, this parameter is required<br><br>which could set the image content of the corresponding parameter. |yes\*\*[only if type=image]\*\*<br><br>no\*\*[type=others]\*\* |
|\*video ||Json object | |When type= video, this parameter is required<br><br>which could set the video content of the corresponding parameter. |yes\*\*[only if type=video]\*\*<br><br>no\*\*[type=others]\*\* |
|\*document ||Json object | |When type= document, this parameter is required<br><br>which could set the document content of the corresponding parameter. |yes\*\*[only if type=document]\*\*<br><br>no\*\*[type=others]\*\* |
|\*location ||Json object | |When type= location, this parameter is required<br><br>which could set the location content of the corresponding parameter. |yes\*\*[only if type=location]\*\*<br><br>no\*\*[type=others]\*\* |


\*Text Object


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|body ||string | |Text content |yes |


\*Image Object


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|link ||string | |URL link of the image. The value should be HTTP/HTTPS URLs |yes |
|caption ||string | |Image description. The value contains a maximum of 1024 characters |no |


\*Video Object


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|link ||string | |URL link of the video. The value should be HTTP/HTTPS URLs. |yes |
|caption ||string | |Video description. The value contains a maximum of 1024 characters. |no |


\*Audio Object


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|link ||string | |URL link of the Audio. The value should be HTTP/HTTPS URLs. |yes |


\*Document Object


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|link ||string | |URL link of the document. The value should be HTTP/HTTPS URLs. |yes |
|filename ||string | |Document file name |no |


\*Location Object


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|longitude ||float | |longitude |yes |
|latitude ||float | |latitude |yes |
|name ||string | |Name of the location |no |
|address ||string | |Detailed address information of the location |no |


Interactive Object


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|type ||string | |Interactive message type. The value can be<br><br>button（quick reply）<br><br>list（list）<br><br>catalog_message（catalog message）<br><br>product（product）<br><br>product_list（product list）<br><br>cta_url (access URL)<br><br>flow |yes |
|header ||header object | |header |no |
|body ||Body object | |body |no |
|footer ||Footer object | |foot |no |
|action ||Action object | |action |no |


Header Object（If it's an Interactive Object）


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|type ||string |*  |The type of title you want to use. Supported values:<br><br><br>1. text<br><br>2. image<br><br>3. video<br><br>4. documennt |yes |
|text ||string |*  |The text of the title. The format allows emoji,<br><br>Maximum length: 60 characters. If type is set to text, this field is required. | |
|image ||Image object |*  |An image object supports only link<br><br>If type is set to image, this field is required. | |
|video ||Video object |*  |The video object supports only link<br><br>If type is set to video, this field is required. | |
|document ||Document object |*  |The document object supports only link<br><br>If type is set to document, this field is required. | |


Body Object（If it's an Interactive Object）


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|text ||string | |Text body |yes |


Footer Object（If it's an Interactive Object）


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|text ||string | |Text body |yes |


Action Object（If it's an Interactive Object）


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|button ||string | |Used for list messages. Button content. It can't be an empty string,<br><br>And must be unique in the message. Support emoji.<br><br>Maximum length: 20 characters. |yes |
|buttons ||array of JsonObjects | |For the reply button. A button object can contain the following parameters:<br><br>type (the only supported type is reply for the reply button),<br><br>title (button title. It cannot be an empty string and must be unique in the message. Support emoji. Maximum length: 20 characters.<br><br>id (unique identifier for the button. When the user clicks the button, this ID is returned in the webhook. Maximum length: 256 characters. | |
|catalog_id ||string | |For single product messages and multi\-product messages.<br><br>Link to your WhatsApp Business account<br><br>A unique identifier for the Facebook directory.<br><br>This ID can be retrieved through the Meta Commerce Manager. | |
|product_retailer_id ||string | |For single product messages and multi\-product messages.<br><br>A unique identifier for a product in the catalog. | |
|sections ||array of JsonObjects | |Used for list messages and multi\-product messages. Array of section objects.<br><br>Minimum 1, maximum 10. | |
|mode ||string | |Options for processing messages. The current pattern of the process,<br><br>draft or publish. Default: published. | |
|flow_message_version ||string | |Required for process messages. It has to be 3. | |
|flow_token ||string | |An identifier generated by the business to be used as an identifier. | |
|flow_id ||string | |A unique identifier for the process provided by WhatsApp. | |
|flow_cta ||string | |Text on the CTA button, such as "Signup".<br><br>Maximum length: 20 characters (excluding emojis). | |
|flow_action ||string | |Options for process messages. Use navigate predefined<br><br>The first screen of messages. For the first screen by<br><br>An advanced use case provided by your endpoint, using data_exchange.<br><br>Default: navigate. | |
|flow_action_payload ||JsonObject | |Required only if flow_action is navigate.<br><br>An object can contain the following parameters:<br><br>screen (must. The id of the first screen of the process. ,<br><br>data_object (Optional. Input data for the first screen. It must be a non\-empty object. | |


Section Object（If it's an Interactive Object）


|**Parameter** ||**Type** |**Value** |**Description** |**Required** |
|---|---|---|---|---|---|
|product_items ||array of JsonObjects |*  |For multi\-product messaging. Object array, at least 1 product per section,<br><br>Up to 30 products overall. Each product object contains the following fields:<br><br>product_retailer_id (A string, mandatory, that uniquely identifies the product in the directory.<br><br>To get this ID, go to Meta Commerce Manager,<br><br>Select your account and the store you want to use, then click Catalog \> Items,<br><br>Find the item you want to mention. The project ID appears below the project name.) |yes |
|rows ||array of JsonObjects |*  |Used for list messages. A list of objects with multiple rows.<br><br>You can have a total of 10 lines in your section.<br><br>Each line must have a header (maximum length: 24 characters)<br><br>And an ID (maximum length: 200 characters).<br><br>You can add a description (maximum length: 72 characters), but this is optional. |yes |
|title ||string |*  |The title of the option.<br><br>Must if the message has multiple options<br><br>Maximum length: 24 characters. |no |


<span id="fbb29759"></span>
### **Example of SMS request payload**

<span id="01fd8d14"></span>
#### Sending Message:

```Plain
{
    "SmsAccount": "test_message_group",
    "Tag": "test_tag",
    "To": [
        {
            "number": "+65XXXXXXXX"
        }
    ],
    "CallbackUrl": "test_callbacl_url",
    "ChannelsFlow": [
        "SMS"
    ],
    "SMS": {
        "From": "sender_id",
        "MessageType": 1,
        "Content": "Your verify code is 123456",
        "Extra": {
            "DltEntityId": "test_entity_id",
            "DltTemplateId": "test_template_id"
        }
    }
}
```


&nbsp;

<span id="c0243716"></span>
### **Example of Whastsapp request payload**

<span id="c9c50ee0"></span>
#### Sending Template Message:

```JSON
{
    "SmsAccount": "xxxxxx",
    "Tag": "123456",
    "To": [
        {
            "number": "+86xxxxx"
        }
    ],
    "CallbackUrl": "https://webhook.site/5ca58225-2949-4453-a5dc-d7c92448b6f4",
    "ChannelsFlow": [
        "Whatsapp"
    ],
    "Whatsapp": {
        "FromNumber": "xxxxx",
        "MessageType": "Template",
        "ParamType": "Component",
        "TemplateID": "WAT_xxxx",
        "Components": [
            {
                "type": "header",
                "parameters": [
                    {
                        "image": {
                            "link": "xxxx"
                        },
                        "type": "image"
                    }
                ]
            },
            {
                "type": "body",
                "parameters": [
                    {
                        "type": "text",
                        "text": "xxx"
                    }
                ]
            }
        ]
    }
}
```


<span id="3de22310"></span>
#### Sending Custom Message:

```JSON
{
    "SmsAccount": "xxxxx",
    "Tag": "123456",
    "To": [
        {
            "number": "+86xxxx"
        }
    ],
    "CallbackUrl": "https://webhook.site/3890a934-482a-4a73-92bc-c9f55c04c46f",
    "ChannelsFlow": [
        "Whatsapp"
    ],
    "Whatsapp": {
        "FromNumber": "xxxxx",
        "MessageType": "Interactive",
        "ParamType": "Custom",
        "Interactive": {
            "type": "button",
            "body": {
                "text": "could you help me？"
            },
            "action": {
                "buttons": [
                    {
                        "type": "reply",
                        "reply": {
                            "id": "1",
                            "title": "yes"
                        }
                    },
                    {
                        "type": "reply",
                        "reply": {
                            "id": "2",
                            "title": "no"
                        }
                    }
                ]
            }
        }
    }
}
```


<span id="5ff7d04f"></span>
## Response

<span id="96b9594f"></span>
### **Response parameters**


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
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


<span id="1917c675"></span>
### **Example of response payload**

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


<span id="05313c5f"></span>
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
