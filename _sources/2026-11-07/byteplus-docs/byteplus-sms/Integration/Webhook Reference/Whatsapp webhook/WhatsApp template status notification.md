---
title: "WhatsApp template status notification"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/WhatsApp_template_status_notification"
---

**WhatsApp Template Status Notification via Webhook**

This webhook enables you to receive updates on the status of your WhatsApp message templates. The statuses may include:


* **Under Review**: The template is still under review, which may take up to 24 hours.

* **Rejected**: The template failed the review process or violated one or more policies. Refer to [Appeals](https://developers.facebook.com/docs/whatsapp/message-templates/guidelines/#appeals).

* **Enabled \- Pending Quality**: No customer feedback or read rate information has been received yet. Templates in this status can be sent to customers. Refer to [Quality Rating](https://developers.facebook.com/docs/whatsapp/message-templates/guidelines/#quality-rating) **.** 

* **Enabled \- High Quality**: Little to no negative feedback has been received from customers. Templates in this status can be sent to customers. Refer to [Quality Rating](https://developers.facebook.com/docs/whatsapp/message-templates/guidelines/#quality-rating).

* **Enabled \- Medium Quality**: Multiple customers have provided negative feedback or low read rates, and the template status may soon change to **Paused** or **Disabled**. Templates in this status can still be sent to customers. Refer to [Quality Rating](https://developers.facebook.com/docs/whatsapp/message-templates/guidelines/#quality-rating).

* **Enabled \- Low Quality**: Significant negative feedback or low read rates have been reported. Templates in this status can still be sent to customers but are at high risk of being paused or disabled. It is recommended to resolve issues promptly. Refer to [Quality Rating](https://developers.facebook.com/docs/whatsapp/message-templates/guidelines/#quality-rating).

* **Paused**: The template has been paused due to customer feedback or low read rates. Templates in this status cannot be sent to customers. Refer to [Template Pause](https://developers.facebook.com/docs/whatsapp/message-templates/guidelines/#template-pausing).

* **Disabled**: The template has been disabled due to negative feedback. Templates in this status cannot be sent to customers.

* **Appeal Requested**: An appeal has been initiated. Refer to [Appeals](https://developers.facebook.com/docs/whatsapp/message-templates/guidelines/#appeals).


For detailed guidelines, refer to the META standards: [Message Template Guidelines](https://developers.facebook.com/docs/whatsapp/message-templates/guidelines/).

<span id="7899146a"></span>
## Callback structure

```JSON
{
    "account": "xxx",
    "subAccount": "xxx",
    "templateID": "WAT_xxx",
    "templateLanguage": "en",
    "time": "2024xxx",
    "value": {
        "wabaID": "xxx",
        "changeType": "message_template_status_update",
        "event": "APPROVED",
        "reason": "NONE"
    }
}
```
