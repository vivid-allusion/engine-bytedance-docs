---
title: "WhatsApp message status delivery notification"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/WhatsApp_message_status_delivery_notification"
---

**WhatsApp Message Status Delivery Report**

In WhatsApp, the messages you send go through multiple intermediate states, such as sent, delivered, or read by the user. These statuses help you track user behavior and make informed decisions for subsequent actions. Using this webhook, you can retrieve these status updates.

**HTTP method**：POST

**Request parameters**：


|**Parameter** |**Type** |**Description** |
|---|---|---|
|account |string |Your BytePlus account. |
|sub_account |string |Message group ID. |
|mobile |string |User Phone number. |
|from_number |string |Waba Phone number |
|channel_type |string |Channel types |
|send_time |int64 |The time when Whatsapp messages are sent. |
|conversation_id |string |Whatsapp conversationID, which could be used for |
|template_id |string |Whatsapp template ID. |
|ext |string |Pass\-through messages.<br><br>***Note***: This parameter refers to the Tag parameter in your requested body. |
|message_id |string |Generated ID numbers and unique identifiers. |
|recv_time |int64 |The time when the delivery receipt is received. |
|status_code |string |Message statuses:<br><br><br>* 0 represents that Whatsapp was sent successfully.<br><br>* Other values represent Whatsapp failed to be sent. |
|error_code |string |The standard error code returned [by META](https://developers.facebook.com/documentation/business-messaging/whatsapp/support/error-codes) |
|status |string |Event:<br><br><br>* delivered: message was delivered successfully<br><br>* submit: message was submitted to meta<br><br>* read: message was read by end users<br><br>* rejected: message was rejected for some reason |
|description |string |Send status description |
|iso_code |string |Country ISO code |
|category |string |Pricing type |


**Example of response payload**

```JSON
[
  {
    "account": "3000000002",
    "sub_account": "10b904d6",
    "mobile": "+861xxxx18169",
    "channel_type": "I18N_WA_AUTH",
    "send_time": 1699962696396,
    "conversation_id": "7655a76687dd492655e98b3a61121339",
    "template_id": "WAT_00001",
    "ext": "123456",
    "message_id": "155a33e9-2a98-4839-bac5-8cd01a5f7371",
    "recv_time": 1699962724893,
    "status_code": "0",
    "error_code": "131049",
    "status": "delivered",
    "description": "DELIVRD",
    "iso_code": "CN",
    "from_number": "861xxxx21374",
    "category": "marketing_lite"
  }
]
```
