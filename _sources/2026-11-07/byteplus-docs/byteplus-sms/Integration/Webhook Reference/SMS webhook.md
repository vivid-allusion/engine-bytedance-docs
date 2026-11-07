---
title: "SMS webhook"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-receiving-delivery-receipts"
---

You can use webhook to get information on events that take place in a BytePlus SMS account.

Event notifications are sent as HTTP POST requests in JSON to the URL you specify in the BytePlus SMS console. BytePlus SMS would send you the following notifications:


* **Delivery receipt**: BytePlus SMS would send you delivery receipts for text messages sent so that you can determine the delivery outcomes.

* **the number of clicks that your shortened URL received**: BytePlus SMS would send you the number of hits from URLs that are included in your text messages.


<span id="626e1ac0"></span>
## Notification structure

After you enable webhook and send text messages, BytePlus SMS will send an event notification to your endpoint in the form of an HTTP POST request. This request includes a JSON request body and multiple headers.

**Header parameters**

The webhook sent by BytePlus SMS contains the following header parameters:


|**Parameter** |**Value** |
|---|---|
|Content\-Type |application/json; charset=utf\-8 |
|Accept\-Encoding |gzip, deflate |
|Accept | **/**  |


**Request body**

BytePlus SMS has three types of request bodies separately:


* **For delivery receipts**:

   
   |**Parameter** |**Type** |**Description** |
   |---|---|---|
   |account |string |Your BytePlus account. |
   |sub_account |string |Message group ID. |
   |status_code |string |Message statuses:<br><br><br>* 0 represents that the message was sent successfully.<br><br>* Other values represent that the message failed to be sent. For a more detailed description, see the Description of status codes section. |
   |description |string |Description of message statuses. For more details, see the Description of status codes section. |
   |signature |string |Text message signature. |
   |from |string |Sender ID. |
   |template_id |string |Text message template ID. |
   |mobile |string |Phone number. |
   |channel_type |string |Message types, including：<br><br><br>* I18N_OTP<br><br>* I18N_MKT |
   |message_id |string |Generated ID number and unique identifiers. |
   |ext |string |Pass\-through messages.<br><br>***Note***: This parameter refers to the Tag parameter in your request body. |
   |service_id |string |Send channel.<br><br>***Note***: This parameter is only available for text messages sent to phone numbers in mainland China. |
   |msg_count |int |Total number of messages sent. |
   |send_time |int64 |The time when the text message is sent.<br><br>Timestamp in milliseconds since January 1, 1970. |
   |recv_time |int64 |The time when the delivery receipt is received.<br><br>Timestamp in milliseconds since January 1, 1970. |
   |mccmnc |string |Mobile Country Code and Mobile Network Code. Example of value: `46002`, where `460` is the MCC code and `02` is the MNC code. |
   |iso_code |string |ISO 3166\-1 country codes. Example of value: `CN`. |
   |carrier_name |string |Mobile Network. Example of value: DTAC. |
   

* **For the number of clicks that your short URL received**:

   
   |**Parameter** |**Type** |**Description** |
   |---|---|---|
   |account |string |BytePlus account. |
   |sub_account |string |The message group ID. |
   |mobile |string |The mobile phone number. |
   |message_id |string |The generated ID number and the unique identification. |
   |token |string |The token for the short URL. |
   |belong |string |The short URL generator. |
   |target |string |The long URL based on which the short URL is generated. |
   |ip |string |The IP address of the request. |
   |ua |string |The client of the request. |
   |click_time |int64 |The time when the hit of URL occurs. |
   

* **Example：** 


```Plain
[
     {
         "account": "your_account_id_3000123456",
         "sub_account": "message_group_id_8a5b12ab",
         "status_code": "0",
         "description": "DELIVRD",
         "signature": "BytePlus",
         "from": "SENDER123",
         "template_id": "template_001",
         "mobile": "+6512345678",
         "channel_type": "SMS",
         "message_id": "639k86d1-ff2d-4kc1-9fs9-e329fa8058bb",
         "ext": "custom_data_here",
         "service_id": "channel_01",
         "msg_count": 1,
         "send_time": 1718179200000,
         "recv_time": 1718179205000,
         "mccmnc": "52505",
         "iso_code": "SG",
         "carrier_name": "Singtel"
     }
]
```


<span id="6f3910fa"></span>
## Notification delivery

After receiving a notification, your endpoint should respond with HTTP status code `200`. After the code is received, BytePlus SMS considers the notification successfully delivered.

**Unsuccessful delivery**

For any unsuccessful notification deliveries, BytePlus SMS attempts to deliver the event notification nine times. If the `200` HTTP status code is received after any retry attempt, then the event notification has been successfully delivered.

However, if BytePlus SMS does not receive the `200` HTTP status code even after nine attempts, then no further notifications related to that event will be sent to your endpoint.

<span id="4208d6cd"></span>
## Status code description

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the returned code begins with "RE," it indicates that this text message is not subject to charges.</div>



|**Code** |**Message** |**Description** |
|---|---|---|
|NE:0100 |Illegal number |Please try to resend after changing the phone number. |
|NE:0101 |Absent number |Please confirm if the phone number is normal and available. |
|NE:0102 |Number roaming or unavailable |Please suggest the user to activate roaming permissions and try again. |
|NE:0103 |Handset abnormal, such as signal issue, sms function error |Please check if the current receiving status of your phone is normal, or restart your phone to refresh the network and try to retrieve it again. |
|NE:0104 |Unsuscriber SMS |Please confirm if the phone number is in a normal state and if the SMS function is enabled. |
|NE:0105 |Handset shutdown,suspend service |Please confirm if the mobile terminal is turned on and available normally. |
|NE:0106 |Number transferring issue |Please suggest attempting to resend or contacting BytePlus customer service for assistance. |
|CR:0200 |Content block |The content contains control keywords, please optimize the content. |
|CR:0201 |Blacklist block |The user has unsubscribed from this signature or hit the blacklist rule on the operator platform. It is recommended to seek user feedback and contact the operator platform to remove the blacklist. |
|CR:0202 |Frequency control |Please control the distribution frequency. |
|CR:0203 |Service time control |Please stagger the control time period for information distribution. |
|CR:0205 |Audit block |The content does not meet the control requirements, please optimize the content. |
|CR:0206 |Overflow block |Please reduce QPS for SMS submission. |
|CR:0207 |Stress test mode block |The pressure testing mode is not actually issued. If you need to turn off the pressure testing mode, please contact BytePlus customer service. |
|CR:0208 |Over traffic block |Exceeding traffic control limits. |
|CR:0211 |Illegal sender |Please contact BytePlus customer service to apply for sender registration. |
|CR:0212 |Signature block |Please replace the signature and issue it or reapply for a signature that meets the signature specifications. |
|CR:0213 |Repeat sending the same content |Please do not send the same content to the same phone number in the short term. |
|CR:0214 |High risk number |High traffic risk. It may be being swiped (phone number score recognition). |
|CR:0215 |Signature reporting issue （one code one signature） |Please contact BytePlus customer service for registration. |
|CE:0300 |Parameter format issue |Please check if the template variable message format is correct. |
|CE:0301 |Long content or not filled in |Please optimize the length of the SMS content. |
|CE:0302 |Absent long SMS |Please check if the split and submission of long SMS is correct. |
|CE:0305 |Unsupported operator |Please contact BytePlus customer service for confirmation. |
|CE:0307 |Mobile_id error |Please enter the correct mobile ID. |
|SY:0500 |System abnormal |If individual distribution fails, it is recommended to try resending. If a large number of failures occur, please contact BytePlus customer service for confirmation. |
|SY:0501 |Gateway issue |If individual distribution fails, it is recommended to try resending. If a large number of failures occur, please contact BytePlus customer service for confirmation. |
|UN:0900 |Unknown error |If individual distribution fails, it is recommended to try resending. If a large number of failures occur, please contact BytePlus customer service for confirmation. |
|RE:0200 |Content block |The content contains prohibited keywords. Please check and remove them. |
|RE:0201 |Blacklist block |The user has unsubscribed from this signature or triggered the blacklist rule on the operator platform. It is advisable to seek feedback from the user and reach out to the operator platform to remove the entry from the blacklist. |
|RE:0202 |Frequency control |Please control the distribution frequency. |
|RE:0211 |Illegal sender |Please contact BytePlus customer service to apply for sender registration. |
|RE:0212 |Signature block |Please replace the signature and issue a new one or reapply for a signature that meets the signature specifications. |
|RE:0213 |Repeat sending the same content |Please do not send identical content to the same phone number in the short term. |
|RE:0214 |High risk number |High traffic risk. It may be being swiped (phone number score recognition). |
|RE:0215 |Signature reporting issue |Please contact BytePlus customer service for registration. |
|RE:0305 |Unsupported operator |Please contact BytePlus customer service for confirmation. |
|RE:0307 |Mobile_id error |Please enter the correct mobile ID. |
|RE:0500 |System abnormal |If one distribution fails, it is recommended to try again. If a large number of failures occur, please contact BytePlus customer service for confirmation. |
