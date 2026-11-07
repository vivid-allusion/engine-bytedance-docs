---
title: "Sending bulk text messages"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/Sending_bulk_text_messages1"
---

Send text messages in bulk to a list of recipients, saving time and effort.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">WhatsApp does not support bulk messaging or online sending.</div>


* <div data-tips="true" data-tips-type="warning">The bulk messaging feature only supports MKT messages that are sent to areas outside mainland China.</div>



<span id="ae59479a"></span>
# Prerequisites


* SMS template has been ready for use.

* You have a quota for SMS messages.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For new users, you can submit a request <a href="https://www.byteplus.com/contact">here</a> for purchasing quota. For existing users, you can contact your customer support or salesperson to increase the quota.</div>


<span id="afcf30ec"></span>
# Context

Bulk messaging is a one\-to\-many approach that allows you to reach and engage a large number of recipients at once. You can easily send bulk text messages by leveraging the bulk messaging feature in the BytePlus SMS console. You can also schedule future text messages to be sent.

<span id="79795413"></span>
# Procedure

<span id="b633739e"></span>
## **Creating a group task**


1. Go to [BytePlus Messaging console](https://console.byteplus.com/sms).

2. In the left navigation pane, click **Messaging** \> **Bulk Messaging**.

3. Click  **+ Create a group task**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a8bd0054b2a4cd7839b3347d4444209~tplv-goo7wpa0wc-image.image) </span>


4. On the page that appears, fill in the blank fields by referring to the following table.



|**Field** |**Description** |
|---|---|
|Message group |Select a message group that you would like to use to send bulk messages. |
|Task name |Create a name for the bulk messaging task. |
|Sender ID |We offer you only one option of BytePlus so far. |
|Template |Select a valid SMS template with MKT message as the template type.<br><br>If you haven't created a template yet, create a template first by referring to [Creating text message templates](https://docs.byteplus.com/en/docs/byteplus-sms/docs-creating-signature-and-templates). |
|Send method |We offer you two options:<br><br><br>* Upload file: Upload bulk phone numbers and variable content via .csv or .xlsx file formats. You can go to the [Create a group task page of SMS console](https://console.byteplus.com/sms/create-task/sms) to download the file template. Note that:<br><br>   * You can upload up to 1 million mobile numbers for a group task.<br><br>   * Please upload files with .csv or .xlsx extension, with the size within 50MB.<br><br>   * To prevent formatting errors, set the cell format to "Text".<br><br>* Manual input: Enter up to 100 phone numbers, separated by an English comma (,). |
|Upload |Click to upload mobile number list. Supports .csv or .xlsx files. |
|Schedule for later |Select to send the text message now or schedule to send it later.<br><br>You are allowed to schedule the text message to send automatically on a particular date and time within a month.<br><br>The default server time is UTC+0. So, based on your time zone, you need to calculate the time when you want to run the timer. |
|Mobile number to receive the demo |Only supports one phone number at one time.<br><br>The test message will also be charged. |



5. Click **Create task**.


<span id="bdb0dc75"></span>
## **Canceling a group task**

After the group task is created, you can cancel it 20 minutes before the scheduled time.

To cancel the group task, go to the **Bulk Messaging** page and click **Revocation**.

<span id="b4bd9ceb"></span>
## **Viewing a group task**

After the group task is created, you can go to the **Bulk Messaging** page and view basic information. Additionally, you can:


1. Click **View Details** to view more detailed information, including delivery results.

2. Click **Download File** to view recipients' phone numbers and variables included in the text message.
