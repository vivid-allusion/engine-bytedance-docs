---
title: "Viewing a PLAIN SASL user password"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/viewing-SASLuser-password"
---

If you forget the password for a PLAIN Simple Authentication and Security Layer (SASL) user, you can view the password in the console.

<span id="a74129a6"></span>
## Background information

SASL/PLAIN is a simple security authentication mechanism that uses preset usernames and passwords for authentication in Kafka. If you forget the password for a PLAIN SASL user, you can view it in the console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only passwords for PLAIN SASL users can be viewed online. If you forget the password for a SCRAM SASL user, we recommend that you reset the password. For more information, refer to <a href="https://docs.byteplus.com/en/docs/kafka/resetting-SASLuser-password">Resetting a SASL user password</a>.</div>


<span id="4a3e41b4"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. On the **User Management** tab, locate the user whose **Password type** is **Plain**.

5. Click **View password** in the **Actions** column corresponding to the specified user.

   In the pop\-up dialog box, view and copy the password.
