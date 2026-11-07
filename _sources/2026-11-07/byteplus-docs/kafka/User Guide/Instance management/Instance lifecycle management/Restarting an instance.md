---
title: "Restarting an instance"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/restarting-instance"
---

Message Queue for Kafka allows you to restart Kafka instances. This topic describes how to restart an instance in the console.

<span id="230c5b83"></span>
## Before you begin

Make sure that the Kafka instance is in the **Running** state and has no background tasks in progress.

<span id="f7802c06"></span>
## Precautions


* Initiating an instance restart triggers an immediate rolling restart, potentially leading to short periods of service unavailability.

* We recommend that you perform this operation during scheduled maintenance windows and implement the reconnection mechanisms on the client to prevent the client from failing to reconnect automatically after disconnection.


<span id="9e16cd9d"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the **Instances** page, locate the target instance.

3. In the **Actions** column of the target instance, click **Restart Instance**.

   Alternatively, click the instance name, then click **Restart Instance** on the upper\-right corner of the instance details page.

4. In the pop\-up dialog box, verify the name and ID of the instance you want to restart, and click **OK**.

   The restart process for a Kafka instance takes about 5–20 minutes. While restarting, the instance status displays as **Restarting**. Upon successful restart, the instance status reverts to **Running**.
