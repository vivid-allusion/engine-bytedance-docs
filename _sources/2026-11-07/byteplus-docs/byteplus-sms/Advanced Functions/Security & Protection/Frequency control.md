---
title: "Frequency control"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/Frequency_control"
---

The Frequency Control module in BytePlus Messaging enables you to set limits on how many SMS messages can be sent to a single mobile number within specific time frames (per minute, per hour, and per day). Additionally, you can create an allowlist to exempt certain mobile numbers from these frequency restrictions. This helps balance communication needs with user experience by preventing excessive messaging to individual recipients.

<span id="131b58d3"></span>
## Prerequisite

BytePlus Messaging has been activated.

<span id="6a8537a0"></span>
## Context

Frequency control is applied at the message group level, allowing you to tailor messaging limits to different business scenarios. By setting send frequency thresholds, you can avoid overwhelming users with too many messages, which helps maintain engagement and compliance with messaging best practices. The allowlist feature offers flexibility to ensure critical communications aren’t hindered by general frequency rules.

<span id="7ac9f387"></span>
## Procedure


1. Go to [BytePlus Messaging console](https://console.byteplus.com/sms).

2. In the left navigation pane, under **Security settings** \> **Frequency control**.

3. Use the dropdown menu at the top of the Frequency Control page to choose the relevant message group.

4. In the **Send Frequency** section, define the maximum number of SMS sends per minute, hour, and day for mobile numbers.

5. In **Frequency Control Allowlist**, enter mobile numbers and click **Add** to exempt them from limits.


<span id="ba8fc174"></span>
## Result

The configured send frequency limits will now apply to the selected message group, controlling how many SMS messages each mobile number receives within the defined time periods. If you add numbers to the allowlist, those numbers will bypass the frequency restrictions and can receive messages without being limited by these settings. You can verify the current limits and allowlist entries directly on the Frequency Control page.
