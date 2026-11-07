---
title: "Set bill consumption warning"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/bill_consumption_warning"
---

<span id="feature-overview"></span>
# Function introduction

You can set up billing consumption warning on demand. When the accumulated consumption amount of the postpaid daily bill of the product or account is greater than the warning threshold, the user will be reminded by text message.


* Warning rules:

   * The statistical range is the amount payable by the bill at 0\-24 o'clock on the day of the transaction.Currently, we support up to 30 warning items. When there are many warning items that meet the warning conditions, you may not be able to receive SMS due to channel frequency control restrictions. Please set warning items as needed. You can go to [Message center](https://console.byteplus.com/message/setting?_vtm_=a8529.0.0_0.0_0.0.74_7654426319179056693) to adjust the account contact person for bill consumption warning notifications.

   * A warning item is reminded once a day. The notification time is the morning of the next day, the recipient is the account contact, and the default notification channel is SMS. You can go to the [Message center](https://console.byteplus.com/message/setting?_vtm_=a8529.0.0_0.0_0.0.74_7654426319179056693) to adjust the contacts and notification channels of the bill consumption warning notification.


<span id="KKDWcI6J"></span>
# Operation steps


1. Access to [Bill details](https://console.byteplus.com/finance/bill/detail):


Click the "Bill Consumption Warning" button to expand the setting warning item drawer page.


2. Add warning items:

* Click "Create alert", you can set the early warning dimension, early warning object, and early warning threshold on demand in the pop\-up window. Currently supports early warnings for three dimensions: Product, Payer, and Owner.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260623061443-1032184603640.png) </span>

3. Check the warning items:


In the list of drawer pages, you can view added alerts, edit to adjust the contents of alerts, or delete alerts as needed.


4. Receive early warning notifications:


The content of the channel notification is as follows. After the alarm, you can choose to go to the [Bill details](https://console.byteplus.com/finance/bill/detail) to view the complete billing data.
