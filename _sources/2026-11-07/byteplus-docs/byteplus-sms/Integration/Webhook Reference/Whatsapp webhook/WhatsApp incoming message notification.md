---
title: "WhatsApp incoming message notification"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/WhatsApp_incoming_message_notification"
---

If an end user replies to a Whatsapp messaging from their device. It is called inbound Whatsapp messaging.

Here in BytePlus Whatsapp solution, customers can use **webhook** to get inbound event information that takes place in a BytePlus account.

<span id="91eb1bfc"></span>
## Inbound structure

<span id="2d96164b"></span>
### **Response Parameters**

**body**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|account |String |BytePlus account in BytePlus console platform |
|sub_account |string |BytePlus message group ID in BytePlus console platform |
|message_id |string |MessageID of each Whatsapp conversation |
|from |string |End user's phone number |
|\*profile |JsonObject |End user's Whatsapp Info |
|to |string |The number of the Whatsapp business account |
|timestamp |long |The time when the message is received.<br><br>Timestamps in milliseconds since January 1, 1970. |
|type |string |Media resource type：<br><br><br>* TEXT<br><br>* IMAGE<br><br>* VIDEO<br><br>* AUDIO<br><br>* DOCUMENT<br><br>* LOCATION<br><br>* STICKER<br><br>* user_preferences |
|\*message |JsonObject |Message information |


**profile**:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|name |string |User Display Name |


**message**:

**Text parameters**:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|text |string |Message text |


**Image parameters**:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|caption |string |Image caption |
|id |string |ImageID |
|mimetype |string |MIME type of the media file |
|url |string |The url of the image |
|sha256 |string |Checksum signature of the media file |


**Video parameters**:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|caption |string |Video caption |
|id |string |VideoID |
|mimetype |string |MIME type of the media file |
|url |string |The url of the video |
|sha256 |string |Checksum signature of the media file |


**Audio parameters**:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|id |string |AudioID |
|mimetype |string |MIME type of the media file |
|url |string |The url of the audio |
|sha256 |string |Checksum signature of the media file |


**Document parameters**:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|filename |string |Document file name |
|caption |string |Document caption |
|id |string |DocumentID |
|mimetype |string |MIME type of the media file |
|url |string |The url of the document |
|sha256 |string |Checksum signature of the media file |


**Location parameters:** 


|**Parameter** |**Type** |**Description** |
|---|---|---|
|long |float |Longitude information of the location |
|lat |float |Latitude information of the location |
|name |string |The name of the location |
|address |string |Detailed address information of the location |
|url |string |The url of the location |


**Sticker parameters:** 


|**Parameter** |**Type** |**Description** |
|---|---|---|
|id |string |StickerID |
|mimetype |string |MIME type of the media file<br><br>：image、webp |
|animated |boolean |true：animate，<br><br>false：others |
|url |string |The url of the sticker |
|sha256 |string |Checksum signature of the media file |


**Button parameters**:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|text |string |The name of the button: contact us |
|payload |string |Click Button，response the payload value when the messaging delivery：automatic reply messaging |


**User_preferences parameters:** 


|**Parameter** |**Type** |**Description** |
|---|---|---|
|wa_id |string |Whatsapp user id |
|detail |string |Message detail |
|category |string |Message type |
|value |string |User select value |
|timestamp |int |Timestamp |


Example

```JSON
{
    "account": "xxx",
    "sub_account": "xxx",
    "message_id": "xxx",
    "from": "userPhoneNumber",
    "profile": {
        "name": "userName"
    },
    "to": "businessWhatsappNumber",
    "timestamp": 1724923995502,
    "type": "image",
    "image": {
        "caption": "caption",
        "url": "xxx.png",
        "id": "12345"
    }
}
```
