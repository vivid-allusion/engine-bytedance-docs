---
title: "Enabling webhook"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-receiving-mobile-originated-messages"
---

Enable webhook so that you can receive notification events sent by BytePlus Messaging.

<span id="05f29cf1"></span>
## Context

A Webhook allows web applications to automatically communicate with other web\-apps through the use of custom callbacks. It allows the observer to automatically push data into the subject's system whenever an event occurs.

After you enable a webhook for BytePlus Messaging and send text messages, BytePlus Messaging will send an event notification to your endpoint in the form of an HTTP POST request. This request includes a JSON request body and multiple headers.

<span id="18626cc6"></span>
## Procedure


1. Log in to the [BytePlus Messaging console](https://console.byteplus.com/auth/login).

2. Go to **Settings** \> **Webhook Settings** .

3. Choose the message group in which you want to set up a webhook.

4. In the **Callback address** section, click the edit icon and type URLs in the corresponding fields:



|**Field** |**Description** |
|---|---|
|Default uplink address |Type a URL to receive mobile\-originated messages. |
|Default status report address |Type a URL to receive delivery receipts, also known as delivery reports. |
|Short URL click status callback address |Type a URL to receive the number of clicks that your shortened URL received. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">You are allowed to type only one URL for each type of webhook in one message group. This URL can be served over HTTPs and HTTP.</div>


2. <div data-tips="true" data-tips-type="tip">If you have configured the webhook address and specified the webhook in the interface at the same time, we will first take the address passed in from the interface for callback</div>


5. Save your changes.


<span id="c9ce83b1"></span>
## Result

The URLs you entered are now listed on the **Receipt Address** page. To better familiarize yourself with webhook parameters, visit [Webhook](https://docs.byteplus.com/en/byteplus-sms/docs/receiving-delivery-receipts).
